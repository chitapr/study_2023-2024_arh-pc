---
## Front matter
title: "Отчёт по лабораторной работе 2"
subtitle: "Архитектура компьютера"
author: "Морозова Мария Вячеславовна"

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
mainfont: PT Serif
romanfont: PT Serif
sansfont: PT Sans
monofont: PT Mono
mainfontoptions: Ligatures=TeX
romanfontoptions: Ligatures=TeX
sansfontoptions: Ligatures=TeX,Scale=MatchLowercase
monofontoptions: Scale=MatchLowercase,Scale=0.9
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

# Цель работы

Изучить идеологию и применение средств контроля версий. Приобрести
практические навыки по работе с системой git.

# Задание

1. Создайте отчет по выполнению лабораторной работы в соответствующем каталоге
рабочего пространства (labs>lab02>report).
2. Скопируйте отчеты по выполнению предыдущих лабораторных работ в соответствую-
щие каталоги созданного рабочего пространства.
3. Загрузите файлы на github.

# Теоретическое введение

Системы контроля версий (Version Control System, VCS) применяются при работе
нескольких человек над одним проектом. Обычно основное дерево проекта хранится в
локальном или удалённом репозитории, к которому настроен доступ для участников про-
екта. При внесении изменений в содержание проекта система контроля версий позволяет
их фиксировать, совмещать изменения, произведённые разными участниками проекта,
производить откат к любой более ранней версии проекта, если это требуется.

# Выполнение лабораторной работы

Создаём учётную запись на сайте https://github.com/ и проводим базовую
настройку: (рис. @fig:001).

![Создали учётную запись на сайте github](image/1.png){#fig:001 width=70%}

Указываем имя и email владельца репозитория. (рис. @fig:002).

![Откроем терминал и введём следующие команды](image/2.png){#fig:002 width=70%}

Настроим utf-8 в выводе сообщений git. (рис. @fig:003).

![Проводим настройку](image/3.png){#fig:003 width=70%}

Зададим имя начальной ветки. (рис. @fig:004).

![Ветка master](image/4.png){#fig:004 width=70%}

Задаём параметры autocrlf, safecrlf. (рис. @fig:005).

![Параметры autocrlf, safecrlf.](image/5.png){#fig:005 width=70%}

Сгенерировали пару ключей (приватный и открытый). (рис. @fig:006).

![Генерация ключей](image/6.png){#fig:006 width=70%}

Скопировали из локальной консоли ключ в буфер обмена. (рис. @fig:007).

![Скопировали полученный ключ](image/7.png){#fig:007 width=70%}

Создали SSH ключ на github. (рис. @fig:008).

![Созданный SSH ключ.](image/8.png){#fig:008 width=70%}

Открываем терминал и создаём каталог для предмета «Архитектура
компьютера». (рис. @fig:009).

![Создаём каталог для предмета](image/9.png){#fig:009 width=70%}

Создаём репозиторий на основе шаблона через web-интерфейс github. (рис. @fig:0010).

![Web-интерфейс github](image/10.png){#fig:0010 width=70%}

Переходим в каталог курса. (рис. @fig:011).

![Переход в каталог](image/11.png){#fig:011 width=70%}

Клонируем созданный репозиторий с помощью git clone. (рис. @fig:012).

![Клонируем репозиторий](image/12.png){#fig:012 width=70%}

Переходим в каталог курса с помощью cd. (рис. @fig:013).

![Переход в каталог](image/13.png){#fig:013 width=70%}

Удаляем лишние файлы с помощью rm (рис. @fig:014).

![Удаляем файлы](image/14.png){#fig:014 width=70%}

Создаём необходимые каталоги. (рис. @fig:015).

![Создание каталогов](image/15.png){#fig:015 width=70%}

 Отправляем файлы на сервер, используя git add, git commit. (рис. @fig:016).

![ Отправляем файлы на сервер.](image/16.png){#fig:016 width=70%}


#Задание для самостоятельной работы

Помещаем готовые отчёты по выполнению лабораторных работ в
соответствующие каталоги рабочего пространства. (рис. @fig:017).

![Проверяем наличие файлов](image/17.png){#fig:017 width=70%}

Загружаем файлы на github с помощью git add. (рис. @fig:018).

![Загружаем файлы на github](image/18.png){#fig:018 width=70%}

Проверяем наличие файлов на сайте. (рис. @fig:019).

![Проверяем наличие файлов](image/19.png){#fig:019 width=70%}

# Выводы

После выполнения лабораторной работы были приобретены практические
навыки по работе с системой git. Изучена идеология и применение средств
контроля версий.




