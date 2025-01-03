
# Лаба №3 - Настройка CI/CD 


## Необходимые поинты:

- Написать “плохой” CI/CD файл, который работает, но в нем есть не менее пяти “bad practices” по написанию CI/CD
- Написать “хороший” CI/CD, в котором эти плохие практики исправлены



## Подготовка окружения

Для написания пайплайнов на внешнем уровне репозитория с проектом создаем дерикторию `.github/workflow/` и создаем пайплайн, например `check.yml`

в самом пайплайне расписываем название пайплайна, действия при которых будут запускаться джобы и сами джобы

## Примерный пайплайн с bad pratctices
```yml
name: CI/CD setting with bad practices


on:
    push:
        branches:
            - main
    pull_request:
        branches:
            - main

jobs:
    test:
        runs-on: ubuntu-latest
        steps:
            - name: Checkout repository
              uses: actions/checkout@v3

            - name: Install Docker Compose
              run: |
                  sudo apt-get update
                  sudo apt-get install -y docker-compose

            - name: Build application
              run: docker-compose -f docker-compose.yml up -d --build

            - name: Test application
              run: docker-compose exec FastAPI_app pytest

    deploy:
        needs: test
        runs-on: ubuntu-latest
        steps:
            - name: Checkout repository
              uses: actions/checkout@v3

            - name: Install Docker Compose
              run: |
                  sudo apt-get update
                  sudo apt-get install -y docker-compose

            - name: Deploy application
              run: |
                  docker-compose -f docker-compose.yml down
                  docker-compose -f docker-compose.yml up -d FastAPI_app
```
### Описание пяти плохих практик
1. Использование последней версии тестовой машины - последние версии могут не поддерживать текущий проект, поэтому требуется фиксировать версию для исключения проблем  

2. Отсутствие кеширования слоев Docker - сборка начинается каждый раз по с нуля, что не эффективно при каждом новом пуше/пр.

3. билд без установки докерикс - без него норм не соберется 

4. Нет указание дериктории докер компоуз

5. не заданы переменные окружения -  позволяет эффективно использовать кеширование, работает без рут прав и прочее. В общем используется билд кит

## Примерный пайплайн с best pratctices
```yml
name: CI/CD Pipeline with Best Practices

on:
    push:
        branches:
            - main
    pull_request:
        branches:
            - main

jobs:
    build: 
        runs-on: ubuntu-20.04
        steps: 
            - name: Checkout repository
              uses: actions/checkout@v3

            - name: Start Docker
              run: sudo service docker start

            - name: Grant Permissions to Docker
              run: sudo chmod 666 /var/run/docker.sock

            - name: Check Docker status
              run: docker info

            - name: Cache Docker layers
              uses: actions/cache@v3
              with:
                  path: /tmp/.buildx-cache
                  key: ${{ runner.os }}-buildx
                  restore-keys: |
                    ${{ runner.os }}-buildx

            - name: Build and Test
              run: docker compose -f ./DevOps/lab3/docker-compose.yml up -d --build

    test:
        needs: build
        runs-on: ubuntu-20.04
        steps: 
            - name: Checkout repository
              uses: actions/checkout@v3

            - name: Set up Docker Buildx
              uses: docker/setup-buildx-action@v2

            - name: Cache Docker layers
              uses: actions/cache@v3
              with:
                  path: /tmp/.buildx-cache
                  key: ${{ runner.os }}-buildx-${{ github.run_id }}
                  restore-keys: |
                    ${{ runner.os }}-buildx-

            - name: test application
              run: |
                docker compose -f ./DevOps/lab3/docker-compose.yml up tests -d --build
                

              env:
                  DOCKER_BUILDKIT: 1
                  COMPOSE_DOCKER_CLI_BUILD: 1
```


### В этом пайплайне учтены все недочеты, + добавлено кеширование

## Попытки починить пайплайн
После первого пуша были траблы с настройкой докер <br />
![troubles](/DevOps/lab3/media/screen2.png)
<br />
Починить получилось убрав из пайплайна отдельную установку докер компоус потому что он сразу входит при установке докера (тупая ошибка получилась) <br />

![result](/DevOps/lab3/media/screen1.png)