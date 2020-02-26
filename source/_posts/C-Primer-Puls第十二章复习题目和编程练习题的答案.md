---

title: C-Primer-Puls第十二章复习题目和编程练习题的答案
date: 2020-02-26 13:41:00
tags: [答案,题目]
categories: C语言

---
本章内容为《C Primer Plus第六版》第十一章复习题和编程练习题的答案
## 复习题
### 第一题
1. 哪些类别的变量可以成为它所在函数的局部变量？

----------


### 第二题
2. 哪些类别的变量在它所在程序的运行期一直存在？

<!--more-->
----------

### 第三题
3. 哪些类别的变量可以被多个文件使用？哪些类别的变量仅限于在一个文件中使用？

----------

### 第四题
4. 块作用域变量具有什么链接属性？

----------

### 第五题
5. extern关键字有什么用途？

----------

### 第六题
6. 考虑下面两行代码，就输出的结果而言有何异同：
        int * p1 = (int *)malloc(100 * sizeof(int));
        int * p1 = (int *)calloc(100, sizeof(int));

----------

### 第七题
7. 下面的变量对哪些函数可见？程序是否有误？
``` c
/* 文件 1 */
int daisy;
int main(void)
{
    int lily;
    ...;
}
int petal()
{
    extern int daisy, lily;
    ...;
}
/* 文件 2 */
extern int daisy;
static int lily;
int rose;
int stem()
{
    int rose;
    ...;
}
void root()
{
    ...;
}
```
----------

### 第八题
8. 下面程序会打印什么？
``` c
#include <stdio.h>
char color = 'B';
void first(void);
void second(void);
int main(void)
{
    extern char color;
    printf("color in main() is % c\n ", color);
    first();
    printf("color in main() is %c\n", color);
    second();
    printf("color in main() is %c\n ", color);
    return 0;
}
void first(void)
{
    char color;
    color = 'R';
    printf("color in first() is %c\n ", color);
}
void second(void)
{
    color = 'G';
    printf("color in second() is %c\n", color);
}
```

----------

### 第九题
9. 假设文件的开始处有如下声明：
        static int plink;
        int value_ct(const int arr[], int value, int n);
a.以上声明表明了程序员的什么意图？
b.用const int value和const int n分别替换int value和int n，是否对主调程序的值加强保护。

----------

## 编程练习

### 第一题
1. 不使用全局变量，重写程序清单12.4。

----------

### 第二题
2. 在美国，通常以英里/加仑来计算油耗；在欧洲，以升/100公里来计算。下面是程序的一部分，提示用户选择计算模式（美制或公制），然后接收数据并计算油耗。
``` c
// pe12-2b.c // 与 pe12-2a.c 一起编译
#include <stdio.h>
#include "pe12-2a.h"
int main(void)
{
    int mode;
    printf("Enter 0 for metric mode, 1 for US mode: ");
    scanf("%d", &mode);
    while (mode >= 0)
    {
        set_mode(mode);
        get_info();
        show_info();
        printf("Enter 0 for metric mode, 1 for US mode");
        printf(" (-1 to quit): ");
        scanf("%d", &mode);
    }
    printf("Done.\n");
    return 0;
}
```
 下面是一些输出示例：

        Enter 0 for metric mode, 1 for US mode: 0
        Enter distance traveled in kilometers: 600
        Enter fuel consumed in liters: 78.8
        Fuel consumption is 13.13 liters per 100 km.
        Enter 0 for metric mode, 1 for US mode (-1 to quit): 1
        Enter distance traveled in miles: 434
        Enter fuel consumed in gallons: 12.7
        Fuel consumption is 34.2 miles per gallon.
        Enter 0 for metric mode, 1 for US mode (-1 to quit): 3
        Invalid mode specified. Mode 1(US) used.
        Enter distance traveled in miles: 388
        Enter fuel consumed in gallons: 15.3
        Fuel consumption is 25.4 miles per gallon.
        Enter 0 for metric mode, 1 for US mode (-1 to quit): -1
        Done.

 如果用户输入了不正确的模式，程序向用户给出提示消息并使用上一次输入的正确模式。请提供pe12-2a.h头文件和pe12-2a.c源文件。源代码文件应定义3个具有文件作用域、内部链接的变量。一个表示模式、一个表示距离、一个表示消耗的燃料。get_info()函数根据用户输入的模式提示用户输入相应数据，并将其储存到文件作用域变量中。show_info()函数根据设置的模式计算并显示油耗。可以假设用户输入的都是数值数据。

----------

### 第三题
3. 重新设计编程练习2，要求只使用自动变量。该程序提供的用户界面不变，即提示用户输入模式等。但是，函数调用要作相应变化。

----------

### 第四题
4. 在一个循环中编写并测试一个函数，该函数返回它被调用的次数。

----------

### 第五题
5. 编写一个程序，生成100个1～10范围内的随机数，并以降序排列（可以把第11章的排序算法稍加改动，便可用于整数排序，这里仅对整数排序）。

----------

### 第六题
6. 编写一个程序，生成1000个1～10范围内的随机数。不用保存或打印这些数字，仅打印每个数出现的次数。用 10 个不同的种子值运行，生成的数字出现的次数是否相同？可以使用本章自定义的函数或ANSIC的rand()和 srand()函数，它们的格式相同。这是一个测试特定随机数生成器随机性的方法。

----------

### 第七题
7. 编写一个程序，按照程序清单12.13输出示例后面讨论的内容，修改该程序。使其输出类似：
        Enter the number of sets; enter q to stop : 18
        How many sides and how many dice? 6 3
        Here are 18 sets of 3 6-sided throws.
        12 10 6 9 8 14 8 15 9 14 12 17 11 7 10 13 8 14
        How many sets? Enter q to stop: q

----------

### 第八题
8. 下面是程序的一部分：
``` c
// pe12-8.c
#include <stdio.h>
int *make_array(int elem, int val);
void show_array(const int ar[], int n);
int main(void)
{
    int *pa;
    int size;
    int value;
    printf("Enter the number of elements: ");
    while (scanf("%d", &size) == 1 && size > 0)
    {
        printf("Enter the initialization value: ");
        scanf("%d", &value);
        pa = make_array(size, value);
        if (pa)
        {
            show_array(pa, size);
            free(pa);
        }
        printf("Enter the number of elements (<1 to quit): ");
    }
    printf("Done.\n");
    return 0;
}
```
 提供make_array()和show_array()函数的定义，完成该程序。make_array()函数接受两个参数，第1个参数是int类型数组的元素个数，第2个参数是要赋给每个元素的值。该函数调用malloc()创建一个大小合适的数组，将其每个 元素设置为指定的值，并返回一个指向该数组的指针。show_array()函数显示数组的内容，一行显示8个数。

----------

### 第九题
9. 编写一个符合以下描述的函数。首先，询问用户需要输入多少个单词。然后，接收用户输入的单词，并显示出来，使用malloc()并回答第1个问题（即要输入多少个单词），创建一个动态数组，该数组内含相应的指向char的指针（注意，由于数组的每个元素都是指向char的指针，所以用于储存malloc()返回值的指针应该是一个指向指针的指针，且它所指向的指针指向char）。在读取字符串时，该程序应该把单词读入一个临时的char数组， 使用malloc()分配足够的存储空间来储存单词，并把地址存入该指针数组 （该数组中每个元素都是指向 char 的指针）。然后，从临时数组中把单词拷贝到动态分配的存储空间中。因此，有一个字符指针数组，每个指针都指向一个对象，该对象的大小正好能容纳被储存的特定单词。下面是该程序的一个运行示例：
        How many words do you wish to enter? 5
        Enter 5 words now:
        I enjoyed doing this exerise
        Here are your words:
        I
        enjoyed
        doing
        this
        exercise

----------
