---
## Front matter
title: "Отчёт по лабораторной работе №8"
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

Приобретение навыков написания программ с использованием циклов и обработкой
аргументов командной строки.

# Задание

Написать программу, которая находит сумму значений функции f(x) для
x = x1, x2, . . ., xn.

# Теоретическое введение

Стек — это структура данных, организованная по принципу LIFO («Last In — First Out»
или «последним пришёл — первым ушёл»). Стек является частью архитектуры процессора и
реализован на аппаратном уровне. Для работы со стеком в процессоре есть специальные
регистры (ss, bp, sp) и команды.
Основной функцией стека является функция сохранения адресов возврата и передачи
аргументов при вызове процедур. Кроме того, в нём выделяется память для локальных
переменных и могут временно храниться значения регистров.
Стек имеет вершину, адрес последнего добавленного элемента, который хранится в ре-
гистре esp (указатель стека). Противоположный конец стека называется дном. Значение,
помещённое в стек последним, извлекается первым. При помещении значения в стек указа-
тель стека уменьшается, а при извлечении — увеличивается.
Для стека существует две основные операции:
• добавление элемента в вершину стека (push);
• извлечение элемента из вершины стека (pop).

# Выполнение лабораторной работы

Создала каталог для программ лабораторной работы 8, перешла в него и создала
файл lab8-1.asm: (рис. @fig:001).

![Создание каталога и файла](image/1.png){#fig:001 width=70%}

Создала файл и запустила программу с текстом листинга 8.1, проверила его работу.
(рис. @fig:002).

![Результат работы программы](image/3.png){#fig:002 width=70%}

Изменила текст программы добавив изменение значения регистра ecx в цикле, проверила работу программы. (рис. @fig:003).

![Запуск программы](image/4.png){#fig:003 width=70%}

Создала исполняемый файл, проверила работу программы с добавлением команды push
и pop. (рис. @fig:004).

![Запуск программы](image/5.png){#fig:004 width=70%}

Создала файл lab8-2.asm в каталоге ~/work/arch-pc/lab08 и ввела в него текст программы из листинга 8.2. Создала исполняемый файл и запустила его, указав аргументы. (рис. @fig:005).

![Создание файла, запуск программы](image/6.png){#fig:005 width=70%}

Создала файл lab8-3.asm в каталоге ~/work/arch-pc/lab08 и ввела в него текст программы из листинга 8.3. Создала исполняемый файл и запустила его, указав аргументы.(рис. @fig:006).

![Создание файла, запуск, результат работы программы](image/7.png){#fig:006 width=70%}

Запустила программу с изменениями текста из листинга 8.3 для вычисления произведения аргументов командной строки. (рис. @fig:007).

![Создание файла, запуск, результат работы программы](image/8.png){#fig:007 width=70%}

# Выполнение самостоятельной работы

Создание файла и запуск программы для вычисления суммы значений функции. (рис. @fig:008).

![Создание файла, результат работы программы](image/9.png){#fig:008 width=70%}

# Выводы

Были приобретены навыки написания программ с использованием циклов и обработкой
аргументов командной строки.

# Листинги

```

%include 'in_out.asm'
 
SECTION .data
f_x db "функция: 3(x+2)",0h
msg db 10,13,'результат: ',0h
 
SECTION .text
global _start
 
_start:
pop ecx
pop edx
sub ecx,1
mov esi, 0
 
next:
cmp ecx,0h
jz _end
pop eax
call atoi
;dec eax
add eax,2
mov ebx,3
mul ebx
add esi, eax
 
loop next
 
_end:
mov eax, f_x
call sprint
mov eax, msg
call sprint
mov eax, esi
call iprintLF
 
call quit

```

