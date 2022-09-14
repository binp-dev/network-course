---
layout: page
title: Задачи
permalink: /tasks/
---

Оценка за курс выставляется на экзамене по теории.

Сдача заданий формирует “промежуточную” оценку за семинарские задания. Для получения оценки “отлично” необходимо набрать не менее 50 баллов, на оценку “хорошо” - не менее 40 баллов, на оценку “удовлетворительно” не менее 30 баллов.

Сдача задания подразумевает также и демонстрацию работоспособности решения. Необходимо умение отвечать на вопросы как по реализации решения, так и по теории. Перед сдачей решения нужно согласовать с семинаристом выбор используемых технических средств, в том числе выбор языка программирования и программных библиотек.

Сдавать задачи можно как на семинарах, так и удалённо. Для удалённой сдачи достаточно завести репозиторий на Github/Gitlab/etc. и дать к нему доступ преподавателю. Желательно, чтобы код в репозитории собирался/запускался стандартным для языка/технологии способом. При нетривиальном использовании должно быть README с кратким описанием.

У каждой задачи в названии указан диапазон максимума получаемых за нее баллов. Бонусы, указанные в тексте задачи как “(+X баллов)”, применяются к нижней границе указанного диапазона.

Поощряется выполнение т.н. “творческих заданий”, условие которых студент формулирует самостоятельно. Максимальная стоимость такого задания определяется преподавателем.

Допускается сдача заданий, выполненных студентом до начала прохождения курса.

За одну из задач, отмеченных звездой, можно получить вдвое больше баллов. Для этого необходимо реализовать ее на языке C с использованием POSIX socket API и корректно обработать все исключительные ситуации. Перед сдачей нужно согласовать с семинаристом свое намерение и архитектуру приложения.

Задачи разбиты на разделы. Сумма баллов за каждый раздел должна быть равна минимум трем.

После 15 октября запрещается сдавать двухбалльные задачи, после 15 ноября – трехбалльные, после 15 декабря – четырехбалльные.

+ Table of contents
{:toc}

## Возня с сокетами

#### Hello world (2 балла)
Написать программу, которая открывает TCP соединение на указанный адрес и порт, отправляет туда строку "Hello, World!" и закрывает его.

#### Ohce (3 балла)
Написать программу, которая ждёт входящее TCP-соединение на любом порту, читает оттуда строки, разделённые переносом строки `\n`, и отправляет их обратно, отражённые зеркально. Например, на "echo\nabcdef\n" программа должна ответить "ohce\nfedcba\n". Повторные соединения принимать не обязательно. После закрытия входящего соединения программа тоже может закрыться.

#### Simple proxy (5 баллов, *)
Написать программу, которая на каждое входящее TCP-соединение на указанный порт порождает исходящее и коммутирует их (данные, поступающие по одному соединению, тут же отправляет по другому и наоборот). Отдельно следует отметить, что программа должна поддерживать несколько одновременных входящих соединений.

#### Hello UDP (2-6 баллов)
Написать две программы, одна из которых отправляет произвольную строку (длиной не более 1000000 байт) через UDP, а вторая принимает её и выводит в stdout. Чем реже вторая программа будет выводить строку, отличающуюся от той, что отправила первая, тем больший балл можно получить за задачу.

#### Простой HTTP-сервер (4–7 баллов, *)
Написать простой HTTP-сервер для отдачи статического содержимого. Сервер должен по запросу отдавать содержимое затребованного файла из определенной директории или ее поддиректорий. (4 балла) Стоимость задачи можно увеличить, реализовав:
+ режим для запуска через inetd (+1 балл);
+ возможность отдачи клиенту не содержимого файла, но результата его исполнения. (+1 – +2 балла).

#### Super-server (inetd) (10 баллов, *)
Написать т. н. super-server: программу, ожидающую соединения на нескольких TCP- или UDP-портах и, при открытии соединения, порождающую соответствующую этому порту дочернюю программу-обработчик, стандартные потоки ввода и вывода которой скоммутированы с сокетом входящего соединения. Другими словами, super-server позволяет “поговорить” по сети со стандартными вводом и выводом “обычной” внешней программы. Соответствие программ портам должно задаваться посредством конфигурационного файла произвольного формата. Обязательно реализовать: выбор типа сокета и номера порта, передачу произвольной команде произвольного набора аргументов, опцию, запрещающую или разрешающую запуск нескольких программ-обработчиков одного типа одновременно.

#### Децентрализованный чат с использованием broadcast (4–8 баллов, *)
Написать программу, позволяющую нескольким пользователям обмениваться текстовыми сообщениями с использованием широковещательных пакетов в одноранговой сети без использования выделенного “сервера” (4 балла). Дополнительно можно реализовать поддержку работы в сети сложной топологии с использованием ретрансляции пакетов на узлах с несколькими интерфейсами (+4 балла).

#### Централизованный чат с использованием TCP (6–8 баллов, *)
Написать программу, позволяющую нескольким пользователям обмениваться текстовыми сообщениями через выделенный сервер. Необходимо придумать свой протокол, реализовать авторизацию, отправку сообщений и передачу информации о статусе клиента (как минимум подключен/отключен) (6 баллов). Дополнительно можно реализовать шифрование соединения посредством TLS (+2 балла).

## Применение готовых библиотек

#### Scraping (3 балла)
Автоматически вычитать большой объём данных с какого-нибудь сайта.

#### HTTP-сервис (5 баллов)
Реализовать простое веб-приложение с использованием какого-либо фреймворка (Flask, Django, ...).

#### Proxy-сервер (3 балла)
Реализовать прокси сервер (SOCKS) и продемонстрировать его работу.

#### Индикатор сетевой активности (7 баллов)
Написать программу, перехватывающую сетевой трафик и графически отображающую временную зависимость сетевой активности (количества захваченных данных в единицу времени). Предполагается использование библиотеки pcap. Также необходимо реализовать возможность задания произвольного фильтра на учитываемый сетевой трафик (см. pcap-filter).
Возможна сдача решений, представляющих собой комбинации готовых утилит; такие решения принимаются на усмотрение преподавателя, оцениваются в первую очередь адекватность подхода и выбранных средств, корректность, краткость и элегантность.

## Администрирование

#### Аналог программы simple proxy, прямо в конфигурационном файле inetd (2 балла)
Реализовать аналог программы simple proxy (см. задачу 1) в одну строку конфигурационного файла классической реализации программы inetd.

#### Настроить iptables и SSH port forwarding (2 балла)
Настроить iptables так, чтобы были запрещены все входящие соединения с внешних интерфейсов, кроме соединений на 22 порт TCP. Запустить и настроить, если это необходимо, SSH-сервер. Продемонстрировать удаленный доступ к локальному ресурсу посредством SSH port forwarding.

#### Загрузка по сети (5 баллов)
Настроить серверы DHCP и TFTP, продемонстрировать бездисковую загрузку ОС по сети посредством PXE.

## Web и контейнеры

#### Контейнеризация (3 балла)
Упаковать какой-либо написаный ранее сервис в контейнер (Docker). При запуске контейнера сервис должен автоматически подниматься и слушать порт 80.

#### Web-сервер (3 балла)
Поднять контейнер с Web-сервером (Nginx или Apache) и настроить его, чтобы он разные пути перенапрвлял на разные сервисы или директории со статичными файлами.

#### HTTPS (3 балла)
Сгенерировать самописный SSL-сертификат и настроить Web-сервер, чтобы он использовал его для HTTPS.

#### Базы данных (5 баллов)
Сделать какой-либо сервис, который работает с какой-либо базой данных (PostgreSQL, MariaDB, ...) (напрямую либо через ORM). Для запуска нескольких связанных контейнеров рекомендуется использовать docker-compose.

#### Websockets (5 баллов)
Сделать простейший сервис, в котором фронтенд и бэкенд общаются через вебсокеты.

#### React (5 баллов)
Написать фронтенд с использованием библиотеки React.

## Организация сетей

#### Настройка Wi-Fi маршрутизатора с NAT и пробросом портов (3 балла)
Настроить обычный Wi-Fi маршрутизатор “потребительского класса”. Необходимо продемонстрировать подмену MAC-адреса внешнего интерфейса, настройку NAT и проброс портов “внутрь” сети. Маршрутизатор может быть предоставлен преподавателем по предварительному запросу.

#### VLAN (3 балла)
Организовать в изначально одноранговой сети несколько изолированных подсетей при помощи подинтерфейсов VLAN.

#### VPN-туннель и маршрутизация (5 баллов)
Поднять VPN (Wireguard, OpenVPN, ...) и настроить маршрутизацию между двумя изолированными подсетями.

#### Peer-to-peer (8 баллов)
Установить прямое соединение (p2p) между двумя клиентами из разных подсетей с NAT. Предлагается использовать rendez-vous сервер и port knocking.

## Перехват и обход

#### Перехват и анализ данных при помощи программы Wireshark (2 балла)
Перехватить трафик, генерируемый браузером при входе на сайт, не использующий шифрование, и вычленить из него логин и пароль пользователя. В самом простом варианте подразумевается применение анализатора сетевого трафика Wireshark “вручную”.

#### Подслушивание изображений (3–8 баллов)
Написать программу, перехватывающую сетевой трафик, вычленяющую из него изображения в одном или нескольких популярных форматах графических файлов и отображающую их на экране по мере обработки. Дополнительные баллы ставятся в зависимости от полноты и обстоятельности решения: приветствуются поддержка нескольких форматов, рекомбинация пакетов и т.п. (+5 баллов)

## Крупные задачи

#### Port knocking daemon, открывающий порты firewall’а (5–8 баллов)
Написать программу, слушающую определенные порты и, в случае получения правильной последовательности подключений или пакетов с одного адреса на разные порты в течение фиксированного промежутка времени, открывающую на некоторое время доступ к “секретному порту” с IP-адреса отправителя. Дополнительный балл можно получить, если на этих же портах при этом принимают и обрабатывают соединения полностью функционирующие и не вызывающие подозрений сервисы (+3 балла).

#### Написать свой fail2ban, закрывающий порты firewall’а (4 балла)
Написать программу, отслеживающую неудачные попытки авторизации посредством чтения log-файла (например, SSH- или HTTP-сервер и, в случае определенного количества неудачных авторизаций с одного и того же IP-адреса, временно закрывающую доступ с этого адреса к порту “атакуемого” сервиса.

#### Распределённое хранилище файлов (10-20 баллов)
Написать программу, реализующую избыточное и распределенное хранилище файлов на нескольких узлах одной сети (10 баллов). Дополнительные баллы можно получить, к примеру, за что-либо из перечисленного далее: отсутствие выделенного сервера; степень избыточности, не равную числу узлов; реализацию избыточности с использованием XOR вместо дублирования; возможность примонтировать хранилище как файловую систему посредством FUSE или аналога; предоставление доступа к данным посредством какого-либо общепринятого протокола передачи файлов (+10 баллов).

#### Блокчейн (10-20 баллов)
Придумать простейший блокчейн (достаточно, чтобы были: валидация блоков, механизм консенсуса и proof-of-work), реализовать ноду для него и продемонстрировать работу сети из нескольких таких узлов. 

#### Голосовое общение (5 баллов)
Написать программу для (одно-)двухсторонней передачи голоса между двумя или более пользователями без выделенного сервера в одноранговой сети. Для компрессии речи необходимо использовать существующий кодек, например Speex, Opus или Vorbis. Использование протоколов SIP и RTP принесет автору дополнительные баллы (сверх 5 баллов).

#### Протокольный демультиплексор (7 баллов, *)
Написать программу, слушающую один TCP-порт и перенаправляющую соединения на другие порты в зависимости от протокола, используемого подключившейся программой-клиентом.

### Написать какой-нибудь существенный патч в upstream open-source сетевой утилиты (по дополнительной договоренности)

### Творческие задания (по дополнительной договоренности)