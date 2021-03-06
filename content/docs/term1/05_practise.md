# Практика 5

На этой практике продолжаем разбираться с указателями. Но в отличие от предыдещей практии, где мы использовали автоматическую память, мы рассмотрим использование динамического выделения памяти на куче.

После этой практики вы должны уметь без Google объяснить:
- В чем разница между динамическим и автоматическим выделением памятью
- Что такое malloc, calloc, free и как ими пользоваться.
- Когда использовать динамическую память и malloc
- Что такое указатель на функцию и как его использовать

## Примеры

```c
#include <stdio.h>
#include <stdlib.h>

int main(void) {
	int* arr; // жил да был указатель
	arr = (int*)malloc(sizeof(int)); // и выделили для одного int место в памяти
	*arr = 42; // и положили туда 42
	printf("%p %d\n", arr, *arr); // и напечатали адрес его на экране, как и само содержимое памяти
	free(arr); // и очистили память
	// и тут решили создать массив!
	size_t n = 10*10;
	arr = (int*)calloc(sizeof(int), n); // выделили память на массив размера n элементов, каждый по sizeof(int) байт.
	for (int i = 0; i < n;i++) {
		arr[i] = i*10; // заполнили его числами 0, 10, 20...,990
	}

	for (int i = 0; i < n; i++) {
		printf("%d %d\n", *(arr+i), arr[i]); // а это одно и то же
	}
	free(arr);
}
```

## Задания

1. Во всех заданиях действует запрет на использование библиотечных функций, кроме `malloc`, `calloc`, `realloc`, `free`, `printf`, `scanf`.
2. Вам не требуется выделять память динамически в этих задачах.
2. Вся логика задания должна находиться в функциях.
3. В функции `main` ТОЛЬКО тестирование работоспособности функции.
4. Прототипы функций менять запрещено.
5. Вспомогательные функции создавать можно.

### Задание 1. Strdup

Напишите функцию, которая возвращает указатель на новый выделенный сегмент памяти, который хранит копию строки, переданной, как аргумент функции.  
По сути вы делаете копию функции из [string.h](https://en.cppreference.com/w/c/experimental/dynamic/strdup).

#### Прототип функции

```c
char *_strdup(const char* str);
``` 

#### Ожидаемое поведение

- функция возвращает NULL, если `str` это NULL
- функция возвращает NULL, если не хватает памяти
- в любом другом случае полученная копия строки должна корректно печататься и заканчиваться `\0`.

### Задание 2.1. Создание матрицы

Напишите функцию, которая выделяет память для двумерной матрицы из целых чисел,

#### Прототип функции

```c
int **alloc_grid(int width, int height);
```

#### Ожидаемое поведение

- каждый элемент матрицы должен быть равен 0
- если входные параметры некорректны (равны 0, отрицательны), то функция возвращает NULL
- если не хватает памяти, то функция возрващает NULL

### Задание 2.2. Удаление матрицы

Напишите функцию, которая очищает память выделенную для ранее созданной матрицы. 

#### Прототип функции

```c
void free_grid(int **grid, int height)
```

#### Ожидаемое поведение

- Ваша программа не должна падать, если входные параметры некорректны
- Проверьте работоспособность вместе с функцией `alloc_grid`.


### Задание 3. Split

Напишите функцию, которая разбивает предложение на слова. То есть использует пробелы как разделитель строки.  
Полная функция [strtok](https://en.cppreference.com/w/c/string/byte/strtok) реализована в стандартной библиотке. Использовать ее нельзя.

#### Прототип функции

```c
char **strplit(const char *str);
```

#### Ожидаемое поведение

- Функция принимает на вход строку.
- Возвращает массив строк, которые не включают оконечные пробелы. Строки нуль-терминальные.
- Если разделитель не встречается, то возвращает массив из одного слова, равного самой строке.
- Если строка пустая или NULL, то возвращается NULL.
- Функция возвращает NULL, если что-то идет не так.

#### Пример поведения

```c
// некоторый псевдокод
strsplit("hello world! Nya") == ["hello", "world!", "Nya"]
``` 

### Задание 4. Поиск истины

Напишите функцию, которая находит индекс первого попавшегося элемента в массиве, который(т.е. элемент) удовлетворяет некоторому условию. Условие подается на вход функции, как указатель на функцию. 

#### Прототип функции

```c
// array - указатель на массив
// size - размер массива
// predicate - указатель на функцию, которая принимает на вход число - элемент массива, и возвращает 1 если условие выполнено и 0 иначе.
int find_index(const int *array, int size, int (*predicate)(int));
```

#### Ожидаемое поведение

- в любой непонятной ситуации функция возвращает -1, как индикатор ошибки.
	- если массив пустой
	- если размер непправильного формата
	- если ничего не найдено
- predicate создает пользователь функции. Поэтому надо протестировать на разных предикатах:
	1. поиск первого четного числа
	2. поиск первого числа, больше 42

## Домашнее задание.

Читать главу [6](http://givi.olnd.ru/kr2/06.html) K&R.