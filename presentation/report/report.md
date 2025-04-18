---
## Front matter
title: "Методика работы пользователя в сети Linux"
subtitle: "Архитектура компьютеров и операционные системы"
author: "Гашимова Эсма Эльшан кызы"

## Generic otions
lang: ru-RU
toc-title: "Содержание"

## Bibliography
bibliography: bib/cite.bib
csl: pandoc/csl/gost-r-7-0-5-2008-numeric.csl

## Pdf output format
toc: true # Table of contents
toc-depth: 2
lof: true # List of figures
lot: true # List of tables
fontsize: 12pt
linestretch: 1.5
papersize: a4
documentclass: scrreprt
## I18n polyglossia
polyglossia-lang:
  name: russian
  options:
	- spelling=modern
	- babelshorthands=true
polyglossia-otherlangs:
  name: english
## I18n babel
babel-lang: russian
babel-otherlangs: english
## Fonts
mainfont: IBM Plex Serif
romanfont: IBM Plex Serif
sansfont: IBM Plex Sans
monofont: IBM Plex Mono
mathfont: STIX Two Math
mainfontoptions: Ligatures=Common,Ligatures=TeX,Scale=0.94
romanfontoptions: Ligatures=Common,Ligatures=TeX,Scale=0.94
sansfontoptions: Ligatures=Common,Ligatures=TeX,Scale=MatchLowercase,Scale=0.94
monofontoptions: Scale=MatchLowercase,Scale=0.94,FakeStretch=0.9
mathfontoptions:
## Biblatex
biblatex: true
biblio-style: "gost-numeric"
biblatexoptions:
  - parentracker=true
  - backend=biber
  - hyperref=auto
  - language=auto
  - autolang=other*
  - citestyle=gost-numeric
## Pandoc-crossref LaTeX customization
figureTitle: "Рис."
tableTitle: "Таблица"
listingTitle: "Листинг"
lofTitle: "Список иллюстраций"
lotTitle: "Список таблиц"
lolTitle: "Листинги"
## Misc options
indent: true
header-includes:
  - \usepackage{indentfirst}
  - \usepackage{float} # keep figures where there are in the text
  - \floatplacement{figure}{H} # keep figures where there are in the text
---

## Введение

Операционная система Linux является одной из наиболее популярных и мощных платформ для работы в сетевом окружении. Система предоставляет пользователю широкие возможности для настройки, управления и использования сетевых ресурсов. Знание основных методов работы с сетью в Linux является важным навыком для системных администраторов, разработчиков и продвинутых пользователей.

В данном докладе рассматриваются основные методы работы пользователя в сети Linux, включая конфигурацию сетевых интерфейсов, настройку IP-адресов, использование команд для диагностики и мониторинга состояния сети, а также основы безопасности при работе в сети.

## 1. Основы настройки сети в Linux

Linux предоставляет несколько инструментов для работы с сетью. Наиболее важные из них — это утилиты для настройки IP-адресов, маршрутов и имен серверов. Конфигурация сети может быть выполнена как через графические интерфейсы, так и через командную строку.

### 1.1. Настройка IP-адресов

Для настройки сетевого интерфейса в Linux часто используется команда `ip`. Например, для назначения статического IP-адреса на интерфейсе `eth0` можно использовать следующую команду:


sudo ip addr add 192.168.1.100/24 dev eth0mi

Также для включения интерфейса используется команда:

sudo ip link set eth0 up


Для удаления IP-адреса:

sudo ip addr del 192.168.1.100/24 dev eth0


### 1.2. Маршруты и шлюзы

Для настройки маршрутов и шлюзов в Linux используется команда ip route. Для добавления маршрута по умолчанию (шлюза) применяется следующая команда:

sudo ip route add default via 192.168.1.1


Для отображения текущих маршрутов:

ip route show


### 1.3. Конфигурация DNS

Для работы с DNS-серверами в Linux можно редактировать файл /etc/resolv.conf. В нем указываются адреса DNS-серверов:

nameserver 8.8.8.8
nameserver 8.8.4.4


Также настройка DNS может быть выполнена через NetworkManager в графических интерфейсах.

## 2. Утилиты для работы с сетью

### 2.1. ping — проверка доступности узлов

Команда ping используется для проверки доступности сетевых узлов. Например:

ping 192.168.1.1

Эта команда отправляет ICMP-запросы и показывает время отклика от указанного устройства.

### 2.2. netstat — отображение сетевых соединений

Для диагностики сетевых соединений и информации о портах используется утилита netstat. Она позволяет увидеть текущие активные соединения, а также статистику по каждому интерфейсу.

netstat -tuln


Команда отображает все активные TCP/UDP соединения.

### 2.3. ifconfig и ip — информация об интерфейсах

Команда ifconfig предоставляет информацию о сетевых интерфейсах, их состоянии и настройках. В новых версиях Linux утилита ifconfig устарела, и рекомендуется использовать команду ip.

Пример использования:

ifconfig

или

ip addr show


### 2.4. traceroute — трассировка маршрута

Утилита traceroute позволяет отслеживать маршрут до удаленного хоста, показывая все промежуточные узлы на пути передачи данных.

traceroute 8.8.8.8


## 3. Безопасность сети в Linux

Безопасность в сети — важный аспект работы с Linux, особенно при использовании открытых публичных сетей. Для обеспечения безопасности и защиты данных можно использовать следующие методы:

### 3.1. Брандмауэр

В Linux для настройки брандмауэра используется утилита iptables или ее более новая версия nftables. Эти инструменты позволяют создавать правила фильтрации трафика, ограничивать доступ к системным ресурсам и защищать систему от атак.

Пример простого правила для блокировки входящих соединений:

sudo iptables -A INPUT -j DROP

### 3.2. SSH и удаленный доступ

Для безопасного удаленного доступа к системе используется протокол SSH. Убедитесь, что для подключения используется ключевая аутентификация, а не пароль, что значительно повышает безопасность.

### 3.3. VPN

Для защиты соединений в открытых сетях, например в общественных Wi-Fi, рекомендуется использовать VPN (Virtual Private Network). Это гарантирует шифрование трафика и защищает данные от перехвата.

## 4. Заключение

Работа с сетью в Linux включает множество инструментов и методов, которые позволяют эффективно настраивать и управлять сетевыми интерфейсами, проводить диагностику, а также обеспечивать безопасность системы. Знание этих инструментов — это основа для успешной работы в любой сети, будь то локальная или интернет.

# Список литературы{.unnumbered}

@book{nemeth2017linux,
  author = {Nemeth, E. and Snyder, G. and Seebass, B.},
  title = {Linux Administration Handbook},
  year = {2017},
  publisher = {Prentice Hall}
}

@article{williams2020network,
  author = {Williams, S.},
  title = {Network Configuration in Linux: Best Practices and Tools},
  journal = {Linux Journal},
  volume = {2020},
  number = {302},
  pages = {34--45}
}

@manual{redhat2019networking,
  author = {Red Hat},
  title = {Red Hat Linux Networking Guide},
  year = {2019},
  publisher = {Red Hat}
}

@online{linuxfoundation2019,
  author = {The Linux Foundation},
  title = {Networking in Linux: A Beginner's Guide},
  year = {2019},
  url = {https://www.linuxfoundation.org/networking}
}


::: {#refs}
:::
