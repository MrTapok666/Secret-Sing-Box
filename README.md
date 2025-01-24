# Secret Sing-Box (SSB)

[**English version**](https://github.com/BLUEBL0B/Secret-Sing-Box/blob/main/README-ENG.md)

### Прокси с использованием протоколов Trojan и VLESS и терминированием TLS на NGINX или HAProxy
Данный скрипт предназначен для полной и простой настройки защищённого прокси-сервера с ядром [Sing-Box](https://sing-box.sagernet.org) и маскировкой при помощи [NGINX](https://nginx.org/ru/) или [HAProxy](https://www.haproxy.org). Два варианта настройки на выбор:

- Все запросы к прокси принимает NGINX, запросы передаются на Sing-Box только при наличии в них правильного пути (транспорт WebSocket или HTTPUpgrade)

![nginx-ru](https://github.com/user-attachments/assets/ac95ed9f-0d70-4ea9-993f-23633a6715c4)

- Все запросы к прокси принимает HAProxy, пароли Trojan считываются из первых 56 байт запроса с помощью скрипта на Lua, запросы передаются на Sing-Box только при наличии в них правильного пароля Trojan (транспорт TCP) — метод [FPPweb3](https://github.com/FPPweb3)

![haproxy-ru](https://github.com/user-attachments/assets/66cc155c-b4cc-4030-940b-688ccb2895fd)

Оба варианта настройки делают невозможным обнаружение Sing-Box снаружи, что повышает уровень безопасности.

> [!IMPORTANT]
> Рекомендуемая ОС: Debian 11/12 или Ubuntu 22.04/24.04. Для настройки понадобится IPv4 на сервере и свой домен, прикреплённый к аккаунту Cloudflare ([Как настроить?](https://github.com/BLUEBL0B/Secret-Sing-Box/blob/main/cf-settings-ru.md)). Запускайте от имени root на чистой системе. Рекомендуется обновить систему и перезагрузить сервер перед запуском скрипта.
>
> Данный проект создан в образовательных и демонстрационных целях. Пожалуйста, убедитесь в законности ваших действий перед использованием.

> [!NOTE]
> С правилами маршрутизации для России. Открытые порты на сервере: 443 и SSH.
 
### Включает:
1) Настройку сервера Sing-Box
2) Настройку обратного прокси на NGINX или HAProxy на 443 порту, а также сайта-заглушки
3) Мультиплексирование для оптимизации соединений
4) Настройку безопасности (опционально)
5) TLS сертификаты Cloudflare с автоматическим обновлением
6) Настройку WARP
7) Включение BBR
8) Клиентские конфиги Sing-Box с правилами маршрутизации для России
9) Автоматизированное управление конфигами пользователей
10) Возможность настройки цепочек из двух и более серверов
 
### Настройка сервера:

Для настройки сервера запустите эту команду:

```
bash <(curl -Ls https://raw.githubusercontent.com/BLUEBL0B/Secret-Sing-Box/master/Scripts/install-server.sh)
```

Затем просто введите необходимую информацию:

![pic-1-ru](https://github.com/user-attachments/assets/6699b83e-f347-41df-bfce-47613936cad1)

В конце скрипт покажет ссылки на клиентские конфиги, рекомендуется их сохранить.

-----

Чтобы вывести дополнительные настройки, введите команду:

```
sbmanager
```

Далее следуйте инструкциям:

![pic-2-ru](https://github.com/user-attachments/assets/699332f7-62f5-41fd-a5ca-308872762804)

Пункты 5 и 6 синхронизируют настройки в клиентских конфигах всех пользователей, что позволяет не редактировать конфиг каждого пользователя отдельно.

### Ключи WARP+:

Чтобы активировать ключ WARP+, введите эту команду, заменив ключ на свой:

```
warp-cli registration license CMD5m479-Y5hS6y79-U06c5mq9
```

### Настройка клиентов:
[Android и iOS:](https://github.com/BLUEBL0B/Secret-Sing-Box/blob/main/Client-Guidelines/Sing-Box-Android-iOS-ru.md) на некоторых устройствах с Android, особенно старых, может не работать "stack": "system" в настройках tun-интерфейса в клиентских конфигах. В таких случаях рекомендуется заменить его на "gvisor" с помощью пункта 4 в sbmanager.

[Windows:](https://github.com/BLUEBL0B/Secret-Sing-Box/blob/main/Client-Guidelines/Sing-Box-Windows-ru.md) рекомендован данный способ, так как он обеспечивает более полные настройки маршрутизации, но можно также вставить ссылку в клиент [Hiddify](https://github.com/hiddify/hiddify-app/releases/latest).

[Linux:](https://github.com/BLUEBL0B/Secret-Sing-Box/tree/main?tab=readme-ov-file#%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0-%D0%BA%D0%BB%D0%B8%D0%B5%D0%BD%D1%82%D0%BE%D0%B2) запустите команду ниже и следуйте инструкциям. Или используйте клиент [Hiddify](https://github.com/hiddify/hiddify-app/releases/latest).
```
bash <(curl -Ls https://raw.githubusercontent.com/BLUEBL0B/Secret-Sing-Box/master/Scripts/sb-pc-linux-ru.sh)
```

### Вы можете поддержать проект, если он полезен для вас:
- USDT (BEP20): 0xe2FeA540a9F1f85C2bfA3e6949c722393B5d636A
- USDT (TRC20): TFN44R1PnhyX29vBqv9Z4cB5wH7MrVyFoC
- Bitcoin (BIP84): bc1qhn2ghk3pcpsrr6l9ywfryvqfzvyx8gs2wnpz89
- Litecoin (BIP84): ltc1q7quvcq3gtlwf2yuk370vhf2syad8ee4we9huj4
- Toncoin (TON): UQCWmIBsU-EZJSH3rhghbtSOtKQBmb5y74mkjbohpDWZ6l-H

### Звёзды по времени:
[![Stargazers over time](https://starchart.cc/BLUEBL0B/Secret-Sing-Box.svg?variant=adaptive)](https://starchart.cc/BLUEBL0B/Secret-Sing-Box)
