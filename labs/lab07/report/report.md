---
## Front matter
title: "Отчёт по лабораторной работе №7"
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

Изучение команд условного и безусловного переходов. Приобретение навыков написания
программ с использованием переходов. Знакомство с назначением и структурой файла
листинга.

# Задание

Написать программу для нахождения наименьшего из трёх чисел, программу для вычисления значения функции f(x).

# Теоретическое введение

Для реализации ветвлений в ассемблере используются так называемые команды передачи
управления или команды перехода. Можно выделить 2 типа переходов:
• условный переход – выполнение или не выполнение перехода в определенную точку
программы в зависимости от проверки условия.
• безусловный переход – выполнение передачи управления в определенную точку про-
граммы без каких-либо условий.

# Выполнение лабораторной работы

Создала каталог для программ лабораторной работы № 7, перешла в него и со-
здала файл lab7-1.asm: (рис. @fig:001).

![Создание файла](image/1.png){#fig:001 width=70%}

Создала исполняемый файл и запустила его с кодом листинга 7.1. (рис. @fig:002).

![Создание файла, запуск](image/2.png){#fig:002 width=70%}

Создала исполняемый файл и запустила его с кодом листинга 7.2. (рис. @fig:003).

![Создание файла, запуск](image/3.png){#fig:003 width=70%}

Создала исполняемый файл и запустила его с изменениями инструкции jmp. (рис. @fig:004).

![Результат работы программы](image/4.png){#fig:004 width=70%}

Создала файл lab7-2.asm в каталоге ~/work/arch-pc/lab07. Запустила с использованием программы из листинга 7.3. (рис. @fig:005).

![Создание файла, запуск](image/5.png){#fig:005 width=70%}

Создала файл листинга для программы из файла lab7-2.asm, открыла файл листинга lab7-2.lst с помощью текстового редактора. Рассмотрим несколько строк: строке 9 содержится номер сторки [9], адресс [00000003], машинный код [803800] и содержимое строки кода [cmp byte [eax], 0] в строке 11 содержится номер сторки [11], адресс [00000008], машинный код [40] и содержимое строки кода [inc eax] в строке 24 содержится номер сторки [24], адресс [0000000F], машинный код [52] и содержимое строки кода [push edx] (рис. @fig:006).

![Файл листинга](image/6.png){#fig:006 width=70%}

Удалила один операнд, чтобы посмотреть какая будет получена ошибка. (рис. @fig:007).

![Ошибка](image/8.png){#fig:007 width=70%}

# Выполнение самостоятельной работы

Запустила программу для вычисления наименьшего из трёх чисел. (рис. @fig:008).

![Результат работы программы](image/9.jpg){#fig:008 width=70%}

Создала исполняемый файл и запустила программу для нахождения f(x), проверила работу для двух пар x,a. (рис. @fig:009).

![Компоновка файла, запуск программы.](image/10.png){#fig:009 width=70%}

# Выводы

Изучили команды условного и безусловного переходов. Приобрели навыки написания
программ с использованием переходов. Познакомились с назначением и структурой файла
листинга.

# Листинги

```
lab7-3

%include 'in_out.asm'

section .data
    msg1 db "Наименьшее число:"
    a dd 45
    b dd 67
    c dd 15

section .bss
    min resb 10

section .text
global _start

_start:
    mov eax, msg1
    call sprint

    mov ecx, [a]
    mov [min], ecx ; 'min = A'
    ; ---------- Сравниваем 'A' и 'С' (как числа)
    cmp ecx, [c] ; Сравниваем 'A' и 'С'
    jl check_B ; если 'A<C', то переход на метку 'check_B',
    mov ecx, [c] ; иначе 'ecx = C'
    mov [min], ecx ; 'min = C'
; ---------- Преобразование 'min(A,C)' из символа в число

check_B:
    ; ---------- Сравниваем 'min(A,C)' и 'B' (как числа)
mov ecx, [min]
    cmp ecx, [b] ; Сравниваем 'min(A,C)' и 'B'
    jl fin ; если 'min(A,C)>B', то переход на 'fin',
    mov ecx, [b] ; иначе 'ecx = B'

    mov [min], ecx

; ---------- Вывод результата
fin:
    mov eax, [min]
    call iprintLF ; Вывод 'min(A,B,C)'
    call quit ; Выход
    
lab7-4

%include 'in_out.asm'

SECTION .data
input1 db "Введите х: ",0h
input2 db "Ввведите а: ",0h

SECTION .bss
max resb 10
x resb 10
a resb 10

SECTION .text
GLOBAL _start

_start:
mov eax,input1
call sprint

mov ecx,x
mov edx,10
call sread

mov eax,x
call atoi 
mov [x],eax 

mov eax,input2
call sprint

mov ecx,a
mov edx,10
call sread

mov eax,a
call atoi 
mov [a],eax 

mov ebx, [x]
cmp [a], ebx
je check

mov eax, [a]
mov ebx, [x]
add eax, ebx
call iprintLF
call quit

check:
mov eax, [a]
mov ebx, 6
mul ebx
call iprintLF
call quit

```

