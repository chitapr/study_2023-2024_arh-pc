---
## Front matter
title: "Отчёт по лабораторной работе №9"
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

Приобретение навыков написания программ с использованием подпрограмм. Знакомство
с методами отладки при помощи GDB и его основными возможностями.

# Задание

Преобразовать программу из лабораторной работы N8 , реализовав вычисление значения функции f(x) как подпрограмму. С помощью отладчика GDB, анализируя изменения значений регистров, определить ошибку и исправить ее.

# Теоретическое введение

Отладка — это процесс поиска и исправления ошибок в программе. В общем случае его
можно разделить на четыре этапа:
• обнаружение ошибки;
• поиск её местонахождения;
• определение причины ошибки;
• исправление ошибки.
Можно выделить следующие типы ошибок:
• синтаксические ошибки — обнаруживаются во время трансляции исходного кода и
вызваны нарушением ожидаемой формы или структуры языка;
• семантические ошибки — являются логическими и приводят к тому, что программа
запускается, отрабатывает, но не даёт желаемого результата;
• ошибки в процессе выполнения — не обнаруживаются при трансляции и вызывают пре-
рывание выполнения программы (например, это ошибки, связанные с переполнением
или делением на ноль).
Второй этап — поиск местонахождения ошибки. Некоторые ошибки обнаружить доволь-
но трудно. Лучший способ найти место в программе, где находится ошибка, это разбить
программу на части и произвести их отладку отдельно друг от друга.
Третий этап — выяснение причины ошибки. После определения местонахождения ошибки
обычно проще определить причину неправильной работы программы.
Последний этап — исправление ошибки. После этого при повторном запуске программы,
может обнаружиться следующая ошибка, и процесс отладки начнётся заново.

# Выполнение лабораторной работы

Создала каталог для выполнения лабораторной работы No 9, перешла в него и со-
здала файл lab09-1.asm: (рис. @fig:001).

![Создание файла](image/1.png){#fig:001 width=70%}

Запустила файл с изменённым текстом листинга 9.1. (рис. @fig:002).

![Результат](image/2.png){#fig:002 width=70%}

Провела трансляцию программ с ключом -g, загрузила файл в отладчик. (рис. @fig:003).

![Открываем отладчик](image/3.png){#fig:003 width=70%}

Проверила работу программы, запустив ее в оболочке GDB с помощью команды run:
(рис. @fig:004).

![Запуск программы](image/4.png){#fig:004 width=70%}

Для более подробного анализа программы установила брейкпоинт на метку _start, запустила программу. (рис. @fig:005).

![Запуск программы с брейкпоинтом](image/5.png){#fig:005 width=70%}

Посмотрела дисассимилированный код программы с помощью команды disassemble
начиная с метки _start. (рис. @fig:006).

![Дисассимилированный код программы](image/6.png){#fig:006 width=70%}

Переключилась на отображение команд с Intel’овским синтаксисом, введя команду set
disassembly-flavor intel. (рис. @fig:007).

![Отображение команд с Intel’овским синтаксисом](image/7.png){#fig:007 width=70%}

Включила режим псевдографики для более удобного анализа программы. (рис. @fig:008).

![Переход в режим псевдографики](image/8.png){#fig:008 width=70%}

На предыдущих шагах была установлена точка останова по имени метки (_start). Проверила это с помощью команды info breakpoints (кратко i b): (рис. @fig:009).

![Команда i b](image/9.png){#fig:009 width=70%}

Выполнила 5 инструкций с помощью команды stepi и проследила за изменением
значений регистров.  (рис. @fig:010).

![Команда stepi](image/10.png){#fig:010 width=70%}

Посмотрела содержимое регистров с помощью команды info registers. (рис. @fig:011).

![Команда i r](image/11.png){#fig:011 width=70%}

Посмотрела значение переменной msg1 по имени. (рис. @fig:012).

![Значение переменной msg1](image/14.png){#fig:012 width=70%}

Посмотрела значение переменной msg2 по адресу. (рис. @fig:013).

![Значение переменной msg2](image/15.png){#fig:013 width=70%}

Изменила первый символ переменной msg1. (рис. @fig:014).

![Изменение msg1](image/16.png){#fig:014 width=70%}

Заменила символ во второй переменной msg2. (рис. @fig:015).

![Изменение msg2](image/17.png){#fig:015 width=70%}

С помощью команды set изменила значение регистра ebx:(рис. @fig:016).

![Команда set](image/18.png){#fig:016 width=70%}

Скопировала файл lab8-2.asm, созданный при выполнении лабораторной работы No8,
с программой выводящей на экран аргументы командной строки в файл с
именем lab09-3.asm: (рис. @fig:017).

![Создание файла lab09-3](image/19.png){#fig:017 width=70%}

Загрузила исполняемый файл в отладчик, указав аргументы: (рис. @fig:018).

![Загрузка файла](image/20.png){#fig:018 width=70%}

Адрес вершины стека хранится в регистре esp и по этому адресу располагается число
равное количеству аргументов командной строки (включая имя программы): (рис. @fig:019).

![Адрес](image/21.png){#fig:019 width=70%}

Посмотрела остальные позиции стека  (рис. @fig:020).

![Остальные позиции стека](image/22.png){#fig:020 width=70%}

# Выполнение самостоятельной работы

Преобразовала программу из лабораторной работы No8, реализовав вычисление значения функции f(x) как подпрограмму. (рис. @fig:021).

![Запуск программы, результат работы программы](image/23.png){#fig:021 width=70%}

С помощью отладчика нашли ошибки в программе. (рис. @fig:022).

![Ошибки](image/24.png){#fig:022 width=70%}

Проверила работу программы. (рис. @fig:023).

![Результат работы программы](image/25.png){#fig:023 width=70%}

# Выводы

Были приобретены навыки написания программ с использованием подпрограмм.

# Листинги

```
%include 'in_out.asm'
SECTION .data
f_x db "функция: 3(x+2)",0h
msg db 10,13,'результат: ',0h
SECTION .text
global _start

_f:
push ebx
dec eax
mov ebx, 10
mul ebx
pop ebx
ret

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
call _f
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



%include 'in_out.asm'
SECTION .data
div: DB 'Результат: ',0
SECTION .text
GLOBAL _start
_start:
; ---- Вычисление выражения (3+2)*4+5
mov ebx,3
mov eax,2
add eax,ebx
mov ecx,4
mul ecx
add eax,5
mov edi,eax
; ---- Вывод результата на экран
mov eax,div
call sprint
mov eax,edi
call iprintLF
call quit
```

