# Практика 1

## В классе

В классе и дома решите все задачи.

Весь код можно писать внутри функции main. 
Свои функции создавать не обязательно. 
Динамической памятью пользоваться не надо.

Вам понадобятся функции `printf` для печати в консоль текста.  
Функция `scanf` для ввода чисел из консоли. Когда пользователь нажимает на Enter число считается введеным.

### Примеры

Для начала попробуйте скопировать и запустить эти примеры. 
Можете использовать онлайн компиляторы [repl.it](https://repl.it/) или [www.onlinegdb.com](https://www.onlinegdb.com/). 
А можете открыть любой текстовый редактор, вставить туда код из примера, сохранить его с расширением `.c` и скомпилировать компилятором gcc: `gcc main.c -o main.out` и запустить программу из консоли `./main.out`.

Подробнее про настройку окружения читайте в разделе [Инструменты](../tools/index.md)

```c
// Подключаем заголовочный файл для работы функций ввода-вывода информации
#include <stdio.h> // чтобы работала печать в консоль printf.

// Пример простой задачи.
int main(void) {
  int n;
  printf("Enter a number\n");
  scanf("%i", &n); // магическая функция для ввода числа. Обратите внимание на знак & перед именем переменной. Мы обсудим это позже на лекциях.
  printf("f(x) = x^2 = %d^2 = %d\n",n, n*n);
}
```

Написать программу, запрашивающую целое число с клавиатуры и выводящую строку «нечётное число», если
число нечетное и строку «чётное», в противном случае.

```c
// Подключаем заголовочный файл для работы функций ввода-вывода информации
#include <stdio.h>
// С функции main() начинается выполнение программы
int main(void) {
  // Определяем переменную, в которую будет записываться число
  int a;
  // Приглашаем ввести число с клавиатуры
  printf("Введите a: ");
  scanf("%i",&a);
  //Проверяем число на четность и выводим соответствующие сообщения
  if (a % 2 == 1) { //можно написать просто if(a % 2)- результат не изменится
    printf("нечётное число\n");
  } else {
    printf("чётное число\n");
  }
  //Завершаем программу
  return 0;
}
```

Написать программу, выводящую на консоль квадраты чисел от 0 до 25.

```c
#include<stdio.h>

int main(void) {
  int a; // очередной элемент последовательности
  // Организуем цикл for, определяя параметр цикла (переменная int i)
  // внутри самого оператора for;
  
  for(int i=0; i<=25; i++) {
    a = i*i;
    printf("%i^2 = %i\n",i,a);
  }

  return 0;
}
```

Написать программу, вычисляющую сумму первых n элементов последовательности, определяемую
соотношениями: $$a_1 = 2, a_{i+1} = a_{i}^2$$

```c
#include<stdio.h>

int main() {
  int a = 2; // первый элемент последовательности
  int s = 0; // переменная для хранения значения суммы
  int n; // переменная, в которую будет заноситься количество слагаемых
  
  // Организуем ввод n
  printf("Введите количество элементов последовательности: ");
  scanf("%i",&n);
  
  for (int i=1; i<=n; i++){
    a = a*a;// вычисляем следующий элемент последовательности
    s = s+a;// добавляем новый элемент к сумме
  }

  // Выводим значение суммы
  printf("Сумма равна %i\n",s);
  return 0;
}
```

Написать программу, которая скопирует один массив размера 5 в другой массив в обратном порядке и каждое число умножить на 10.

```c
#include<stdio.h>

// Пример со статическим массивом
int main(void) {
  int x[] = {1,2,3,4,5}; // создали массив и заполнили его числами сразу. Его размер будет равен количеству чисел в блоке инициализации в фигурных скобках.
  int y[5]; // создали массив из 5 элементов.

  for (int i = 0; i < 5; i++) {
    y[i] = 10*x[4-i]; // почему тут 4??? хммм. Странно то как.
  }

  for (int i = 0; i<5;i++) {
    printf("%d ", y[i]);
  }
  printf("\n");
}
```

Написать программу, которая заполнит массив числами, введеными с клавиатуры.

```c
#include<stdio.h>

// Пример со статическим массивом
int main(void) {
  int x[10]; // выделили память на массив размера 10.

  for (int i = 0; i < 10; i++) {
    scanf("%d", &x[i]);
  }


  // проверим что он сохранил числа
  for (int i = 0; i < 10;i++) {
    printf("%d ", x[i]);
  }
  printf("\n");
}
```

### Задания

1. Напишите программу, которая вычисляет значение выражения `f(x)` не используя функцию стандартной библиотеки `abs`. Число x водится с клавиатуры. $$f(x) = \| \| 2x+3 \| -1 \| $$ 

2. Напишите программу, вычисляющую значение выражения: 

$$\begin{equation}
  f(x) = \begin{cases}
    2x^2-1 &\ x < 0 \\\\
    x - 7 &\ x > 10 \\\\
    x ^ 3 &\
  \end{cases}
\end{equation}$$

3. Написать программу, выводящую на экран 20 первых элементов последовательности Фибоначчи. Числа Фибоначчи образуются по правилу: $$a_1 = 1, \\\\ a_2 = 1, \\\\ a_{i+1}=a_i + a_{i-1}$$

4. Напишите программу, подсчитывающую сумму цифр данного натурального числа. Например, для числа `1234` сумма равна `1+2+3+4=10`.

5. Напишите программу, которая напечатает все простые числа до N, включительно. Подумайте над тем, как сделать алгоритм чуть лучше, чем полный перебор.

6. Написать программу, которая проверяет, является ли число `N` палиндромом, то есть число одинаково читающееся в обоих направлениях. Например, `121` - палиндром. `657756` - палиндром. Напечатайте в консоль `N is palindrom` или `N is not palindrom`.

7. Написать программу, которая выводит наибольший простой палиндром не больше N. Например, при N = 1000, это будет 929. 
  
8. Напишите прграмму, которая решает квадратное уравнение в действительных числах методом дискриминанта. Коэффициенты должны вводиться с клавиатуры. $$f(x) = x^2 -x -6, x_1=3, x_2=-2$$

9. Написать программу, которая заполняет массив размера N=10, числами из консоли. Напечатайте в консоль среднее арифметическое, максимум, минимум этой последовательности чисел.

10. Разработать программу для подсчета максимального числа
идущих подряд одинаковых элементов массива. Заполните массив размера 10 числами из консоли. Пример, для `1 1 2 2 5 5 5 4 1 1` ответ `3`.

## Дома

Доделать задачи из класса.

[Читать главу 2 K&R](http://givi.olnd.ru/kr2/02.html).