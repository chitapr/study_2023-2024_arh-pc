---
## Front matter
title: "Отчёт по лабораторной работе №5"
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

Приобретение практических навыков работы в Midnight Commander. Освоение инструкций
языка ассемблера mov и int..

# Задание

Создать программы с выводом приглашения:"Введите строку".

# Теоретическое введение

Midnight Commander (или просто mc) — это программа, которая позволяет просматривать
структуру каталогов и выполнять основные операции по управлению файловой системой,
т.е. mc является файловым менеджером. Midnight Commander позволяет сделать работу с
файлами более удобной и наглядной.
Для активации оболочки Midnight Commander достаточно ввести в командной строке mc и
нажать клавишу Enter.
В Midnight Commander используются функциональные клавиши F1 — F10 , к которым
привязаны часто выполняемые операции.

# Выполнение лабораторной работы

Перешли в каталог ~/work/arch-pc, с помощью строки ввода и команды touch создали файл lab5-1.asm в папке lab05.
(рис. @fig:001).

![Создание файла](image/51.png){#fig:001 width=70%}

Вводим текст программы вывода сообщения на экран и ввода строки с клавиатуры. 
(рис. @fig:002).

![Программа вывода и ввода](image/52.png){#fig:002 width=70%}

С помощью клавиши F3 открыла файл lab5-1.asm, убедилась, что он содержит текст программы. (рис. @fig:003).

![Просмотр файла](image/53.png){#fig:003 width=70%}

Оттранслировала текст программы lab5-1.asm в объектный файл. Выполнила компо-
новку объектного файла и запустила получившийся исполняемый файл. На запрос ввела ФИО. (рис. @fig:004).

![Компоновка и запуск](image/54.png){#fig:004 width=70%}

Скопировала файл in_out.asm в каталог с файлом lab5-1.asm и проверила, что они действительно находятся в одной папке, создала копию файла lab5-1 с именем lab5-2. (рис. @fig:005).

![Проверка](image/55.png){#fig:005 width=70%}

Скомпоновала объектный файл, запустила программу lab5-2.(рис. @fig:006).

![Компоновка и запуск](image/56.png){#fig:006 width=70%}

Запустила прорамму после замены sprintLF на sprint. (рис. @fig:007).

![Замена](image/57.png){#fig:007 width=70%}

# Выполнение самостоятельной работы

Внесла изменения в программу. (рис. @fig:008).

![Изменения](image/58.png){#fig:008 width=70%}

Запустила программу с изменениями. (рис. @fig:009).

![Запуск](image/59.png){#fig:009 width=70%}

Создала копию файла lab5-2. (рис. @fig:0010).

![Копия](image/510.png){#fig:0010 width=70%}

Исправила текст программы. (рис. @fig:0011).

![Исправление](image/511.png){#fig:0011 width=70%}

Запустила исправленную программу. (рис. @fig:0012).

![Запуск](image/512.png){#fig:0012 width=70%}

Листинги:

SECTION .data ; Секция инициированных данных
msg: DB 'Введите строку:',10 ; сообщение плюс
; символ перевода строки
msgLen: EQU $-msg ; Длина переменной 'msg'
SECTION .bss ; Секция не инициированных данных
buf1: RESB 80 ; Буфер размером 80 байт
SECTION .text ; Код программы
GLOBAL _start ; Начало программы
_start: ; Точка входа в программу
;------------ Cистемный вызов `write`
; После вызова инструкции 'int 80h' на экран будет
; выведено сообщение из переменной 'msg' длиной 'msgLen'
mov eax,4 ; Системный вызов для записи (sys_write)
mov ebx,1 ; Описатель файла 1 - стандартный вывод
mov ecx,msg ; Адрес строки 'msg' в 'ecx'
mov edx,msgLen ; Размер строки 'msg' в 'edx'
int 80h ; Вызов ядра
;------------ системный вызов `read` ----------------------
; После вызова инструкции 'int 80h' программа будет ожидать ввода
; строки, которая будет записана в переменную 'buf1' размером 80 байт
mov eax, 3 ; Системный вызов для чтения (sys_read)
mov ebx, 0 ; Дескриптор файла 0 - стандартный ввод
mov ecx, buf1 ; Адрес буфера под вводимую строку
mov edx, 80 ; Длина вводимой строки
int 80h ; Вызов ядра

mov eax,4
mov ebx,1
mov ecx,buf1
mov edx,buf1
int 80h

; После вызова инструкции 'int 80h' программа завершит работу
mov eax,1 ; Системный вызов для выхода (sys_exit)
mov ebx,0 ; Выход с кодом возврата 0 (без ошибок)
int 80h ; Вызов ядра

# Выводы

Были приобретены практические навыки работы в Midnight Commander,освоены инструкции языка ассемблера mov и int. 

