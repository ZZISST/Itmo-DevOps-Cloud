# Лабораторная работа 2. Сравнение сервисов Amazon Web Services и Microsoft Azure. Создание единой кросс-провайдерной сервисной модели.

# Вариант 7

## Авторы:

- Субботин Александр Станиславович
- Люсин Дмитрий Витальевич


## Цель работы:
 Получение навыков аналитики и понимания спектра публичных облачных сервисов без привязки к вендору. Формирование у студентов комплексного видения Облака. 

## Дано:
1. Данные лабораторной работы 1.


2. Слепок данных биллинга от провайдера после небольшой обработки в виде SQL-параметров. Символ % в начале/конце означает, что перед/после него может стоять любой набор символов.

3. Образец итогового соответствия, что желательно получить в конце. В этом же документе 

## Необходимо:
1. Импортировать файл .csv в Excel или любую другую программу работы с таблицами. Для Excel делается на вкладке Данные – Из текстового / csv файла – выбрать файл, разделитель – точка с запятой.

2. Распределить потребление сервисов по иерархии, чтобы можно было провести анализ от большего к меньшему (напр. От всех вычислительных ресурсов Compute дойти до конкретного типа использования - Выделенной стойка в датацентре Dedicated host usage). При этом сохранять логическую концепцию, выработанную в Лабораторной работе 1.

3. Сохранить файл и залить в соответствующую папку на Google Drive.

## Алгоритм работы:
Сопоставить входящие данные от провайдера с его же документацией. Написать в соответствие колонкам справа значения 5 колонок слева, которые бы однозначно классифицировали тип сервиса. Для столбцов IT Tower и Service Family значения можно выбрать из образца. В ходе выполнения работы не отходить от принципов классификации, выбранных в Лабораторной работе 1. Например, если сервис Машинного обучения был разбит на Вычислительные мощности и Облачные сервисы, то продолжать его разбивать и в новых данных.

## Выолнение работы

1. Знакомимся с данный нам слепком, экспортировали .cvs в .xlsx

![Local](/Clouds/Lab2(Azure)/media/screen1.png)


2. Распределили столбцы в соответствии документации [Azure][1]

3. Результат

[Ссылка на файл в Google Drive][2]

![Result](/Clouds/Lab2(Azure)/media/screen2.png)




### Описание сервисов
При выполнении работы были встречены следующие сервисы:
- Azure SQL Data Warehouse — это облачный аналитический сервис, построенный на базе massively parallel processing (MPP). Он предназначен для обработки больших объемов данных и позволяет масштабировать ресурсы в режиме реального времени, обеспечивая высокую производительность для аналитических запросов.

- Azure Storage - предоставляет масштабируемое, безопасное и надежное хранилище данных в облаке. Оно поддерживает работу с большими объемами структурированных и неструктурированных данных и включает службы, такие как Blob Storage (хранение объектов), File Storage (файловое хранилище), Queue Storage (очереди) и Table Storage (таблицы).

- Azure Backup — это решение для резервного копирования данных в облаке, обеспечивающее защиту от потери информации. Оно поддерживает автоматическое резервное копирование, возможность восстановления данных и интеграцию с локальными системами.

- Azure Recovery Services - предлагает инструменты для обеспечения высокой доступности и восстановления после сбоев. Включает Azure Site Recovery для управления аварийным восстановлением и Azure Backup для защиты данных.

- Azure Compute Storage - предоставляет ресурсы хранения, оптимизированные для облачных вычислительных задач. Эти хранилища интегрируются с вычислительными сервисами, такими как виртуальные машины, обеспечивая низкую задержку и высокую производительность.

- Azure Machine Learning — это платформа для разработки, обучения и развертывания моделей машинного обучения. Она поддерживает интеграцию с инструментами Python и R, а также предлагает автоматизированное машинное обучение (AutoML) и визуальные конвейеры разработки моделей.

- Azure Batch Storage - используется в связке с Azure Batch для организации параллельных вычислений. Хранилище оптимизировано для работы с большими наборами данных, обеспечивая высокую производительность для обработки заданий.

- Virtual Machines - VMAzure предоставляют масштабируемые вычислительные ресурсы в облаке. Они поддерживают запуск различных операционных систем (Windows, Linux) и позволяют гибко настроить конфигурацию для разнообразных задач, включая разработку, тестирование и развертывание приложений.

- Visual Studio — это интегрированная среда разработки (IDE) от Microsoft, которая предоставляет мощные инструменты для написания, отладки и развертывания приложений на различных языках программирования, включая C#, Python и JavaScript. Интеграция с Azure упрощает работу с облачными сервисами.

- Azure App Service (ранее Websites) — это управляемая платформа для хостинга веб-приложений, API и мобильных приложений. Она поддерживает несколько языков программирования, таких как .NET, Java, Node.js и PHP, и обеспечивает высокую доступность и масштабируемость.

- Azure Data Factory v2 — это облачный инструмент для интеграции данных и создания ETL/ELT конвейеров. Он позволяет извлекать, преобразовывать и загружать данные из множества источников, поддерживает гибкое планирование и управление сложными рабочими процессами.


### Вывод:
Azure лучше подходит для компаний, использующих экосистему Microsoft и гибридные облака. AWS же более гибридное и открытое решение 

[1]: https://learn.microsoft.com/en-us/azure/?product=popular "Официальная документация Microsoft Azure"
[2]: https://docs.google.com/spreadsheets/d/1ybb6-cZqzlN6J6u_uH8ysGhPDt7KOpkc/edit?usp=share_link&ouid=113039591834532746399&rtpof=true&sd=true "result"