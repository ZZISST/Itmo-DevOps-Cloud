# Отчёт по лабораторной работе №1*

### Работу выполнили:
* Люсин Дмитрий
* Субботин Александр

### Техническое задание:
Попробовать взломать nginx другой команды. Проверить минимум три уязвимости - например path traversal, перебор страниц через ffuf и/или любые другие на ваш выбор.
Взлом считается успешным, если вы попали туда, куда не планировалось попадать пользователю, даже если там ничего нет

Мы взламывали Nginx команды [ТЕХ](https://github.com/Namil27/itmo_devops_labs/tree/main/lab1). Хоть мы и не первые пытаемся взломать их Nginx, но исходя из задания мы ещё имеем такую возможность, так как мы вторые по счёту.

### Ход работы:
1. **Path Traversal** - произвели попытку получить доступ к системным файлам

![](https://github.com/ZZISST/Itmo-DevOps-Cloud/blob/main/DevOps/lab1/lab1*/Path_Traversal.png)

Ничего не получилось, мы получаем ошибку "404 Not Found"

2. **Fuzz Faster U Fool**

![](https://github.com/ZZISST/Itmo-DevOps-Cloud/blob/main/DevOps/lab1/lab1*/FFUF.png)

Было отправлено 1 273 833 запроса. В результате ни одной директории не было найдено.

3. **Защита от DDoS** - запустили стресс-тесты с использованием "ab"

![](https://github.com/ZZISST/Itmo-DevOps-Cloud/blob/main/DevOps/lab1/lab1*/DDoS.png)

В ходе атаки было отправленно 100 000 запросов, однако все запросы были успешными. В совокупности все эти запросы были обработанны за 119 секунд, что довольно неплохой показатель.

### Итоги:
В ходе выполнения работы мы узнали о различных уязвимостях Nginx и как можно проверять свой Nginx на наличие этих уязвимостях, что несомненно пригодится нам в будущем 