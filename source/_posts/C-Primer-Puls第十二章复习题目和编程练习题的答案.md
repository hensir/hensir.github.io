---
title: C-Primer-Puls第十二章复习题目和编程练习题的答案
tags:
  - C语言
categories: C Primer Plus
cover: 'https://s1.ax1x.com/2020/04/26/JcBGNQ.png'
abbrlink: 30d1212
date: 2020-02-26 13:41:00
---
本章内容为《C Primer Plus第六版》第十二章复习题和编程练习题的答案
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
``` c
#include <stdio.h>
int main(void)
{
    int units = 0;
    printf("How many pounds to a firkin of butter?\n");
    scanf("%d", &units);
    while (units != 56)
    {
        printf("No luck, my friend. Try again.\n");
        scanf("%d", &units);
    }
    printf("You must have looked it up!\n");
    return 0;
}
```
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
``` c
// pe12-2b.c
#include <stdio.h>
#include "pe12-2a.h"
int main(void)
{
    int mode;
    printf("Enter 0 for metric mode, 1 for US mode: ");
    scanf("%d", &mode);
    while (mode >= 0)           //输入零或正整数   -1退出
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
 ``` c
// pe12-2a.c
#include "pe12-2a.h"
static int pattern = 0;         //模式
static int last_pattern = 1;    //默认上一次输入的正确模式为 0
static double distance = 0;     //行驶距离
static double fuelconsumed = 0; //消耗的燃料
void set_mode(int mode)
{
    extern int pattern;
    pattern = mode;
}
void get_info()
{
    extern int pattern;
    extern double distance;
    extern double fuelconsumed;
    if (pattern != 0 && pattern != 1)
    {
        pattern = last_pattern;
        printf("Invalid mode specified. Mode %d used.\n", last_pattern);
    }
    if (pattern) //如果模式为 1
    {
        last_pattern = pattern;     //如果当前模式正确则
        puts("Enter distance traveled in miles:");
        scanf("%lf", &distance);
        puts("Enter fuel consumed in gallons:");
        scanf("%lf", &fuelconsumed);
    }
    else if (!(pattern)) //如果模式为 0
    {
        last_pattern = pattern;
        puts("Enter distance traveled in kilometers:"); //换行
        scanf("%lf", &distance);
        puts("Enter fuel consumed in liters:");
        scanf("%lf", &fuelconsumed);
    }
}
void show_info()
{
    extern int pattern;
    extern double distance;
    extern double fuelconsumed; //要确保到si函数时  模式必须为 1 or 0
    if (pattern)
        printf("Fuel consumption is %.1lf miles per gallon.\n", distance / fuelconsumed);
    else
        printf("Fuel consumption is %.2lf liters per 100 km.\n", fuelconsumed / distance * 100);
}
```
 ``` c
// pe12-2a.h
#include <stdio.h>
void set_mode(int);
void get_info();
void show_info();
```
----------

### 第三题
3. 重新设计编程练习2，要求只使用自动变量。该程序提供的用户界面不变，即提示用户输入模式等。但是，函数调用要作相应变化。
``` c
// pe12-2b.c
#include <stdio.h>
#include "pe12-2a.h"
int main(void)
{
    int mode;
    int last_mode = 1;
    double distance = 0;     //行驶距离
    double fuelconsumed = 0; //消耗的燃料
    printf("Enter 0 for metric mode, 1 for US mode: ");
    scanf("%d", &mode);
    while (mode >= 0) //输入零或正整数   -1退出
    {
        get_info(mode, &last_mode, &distance, &fuelconsumed);
        show_info(mode, distance, fuelconsumed);
        printf("Enter 0 for metric mode, 1 for US mode");
        printf(" (-1 to quit): ");
        scanf("%d", &mode);
    }
    printf("Done.\n");
    return 0;
}
```
``` c
// pe12-2a.c
#include "pe12-2a.h"
void get_info(int mode, int *last_mode, double *distance, double *fuelconsumed)
{
    if (mode != 0 && mode != 1)
    {
        mode = *last_mode;
        printf("Invalid mode specified. Mode %d used.\n", *last_mode);
    }
    if (mode) //如果模式为 1
    {
        *last_mode = mode; //如果当前模式正确则
        puts("Enter distance traveled in miles:");
        scanf("%lf", distance);
        puts("Enter fuel consumed in gallons:");
        scanf("%lf", fuelconsumed);
    }
    else if (!(mode)) //如果模式为 0
    {
        *last_mode = mode;
        puts("Enter distance traveled in kilometers:");
        scanf("%lf", distance);
        puts("Enter fuel consumed in liters:");
        scanf("%lf", fuelconsumed);
    }
}
void show_info(int mode, double distance, double fuelconsumed)
{
    if (mode)
        printf("Fuel consumption is %.1lf miles per gallon.\n", distance / fuelconsumed);
    else
        printf("Fuel consumption is %.2lf liters per 100 km.\n", fuelconsumed / distance * 100);
}
```
``` c
// pe12-2a.h
#include <stdio.h>
void get_info(int, int *, double *, double *);
void show_info(int, double, double);
```
----------

### 第四题
4. 在一个循环中编写并测试一个函数，该函数返回它被调用的次数。
``` c
#include <stdio.h>
int count = 0;      //文件作用域的变量自动初始化为 0
void fun(void);
int main(void)
{
    char ch;
    while((ch = getchar()) != 'q')  //字符串首字母不为q则
    {
        fun();
        while (getchar() != '\n')
            continue;
    }
    printf("%d", count);
    return 0;
}
void fun(void)
{
    extern count;
    count++;
    return count;
}
```
----------

### 第五题
5. 编写一个程序，生成100个1～10范围内的随机数，并以降序排列（可以把第11章的排序算法稍加改动，便可用于整数排序，这里仅对整数排序）。
``` c
#include <stdio.h>
#include <stdlib.h>
int main(void)
{
    int random[100] = {0};
    int temp = 0;
    for (int i = 0; i < 100; i++)
        random[i] = (rand() % 10 + 1);
    for (int i = 0; i < 100; i++)
    {
        for (int j = 0; j < i; j++)
        {
            if (random[i] > random[j])
            {
                temp = random[i];
                random[i] = random[j];
                random[j] = temp;
            }
        }
    }
    for (int i = 0; i < 100; i++)
        printf("%d ", random[i]);
    return 0;
}
```
----------

### 第六题
6. 编写一个程序，生成1000个1～10范围内的随机数。不用保存或打印这些数字，仅打印每个数出现的次数。用 10 个不同的种子值运行，生成的数字出现的次数是否相同？可以使用本章自定义的函数或ANSIC的rand()和 srand()函数，它们的格式相同。这是一个测试特定随机数生成器随机性的方法。
``` c
#include <stdio.h>
#include <stdlib.h>
int main(void)      //次数不相同   都是100左右
{
    int seed[10] = {0};
    for (int i = 0; i < 10; i++)
    {
        int a1 = 0, a2 = 0, a3 = 0, a4 = 0, a5 = 0, a6 = 0, a7 = 0, a8 = 0, a9 = 0, a10 = 0;
        seed[i] = rand();
        srand(seed[i]);         //以默认种子为 1 rand()生成10个种子以供使用
        for (int j = 0; j < 1000; j++)
        {
            switch (rand() % 10 + 1)
            {
            case 1:
                a1++;
                break;
            case 2:
                a2++;
                break;
            case 3:
                a3++;
                break;
            case 4:
                a4++;
                break;
            case 5:
                a5++;
                break;
            case 6:
                a6++;
                break;
            case 7:
                a7++;
                break;
            case 8:
                a8++;
                break;
            case 9:
                a9++;
                break;
            case 10:
                a10++;
                break;
            }
        }
        printf("| 1:%3d | 2:%3d | 3:%3d | 4:%3d | 5:%3d | 6:%3d | 7:%3d | 8:%3d | 9:%3d | 10:%3d |\n", a1, a2, a3, a4, a5, a6, a7, a8, a9, a10);
    }
    return 0;
}
```
----------

### 第七题
7. 编写一个程序，按照程序清单12.13输出示例后面讨论的内容，修改该程序。使其输出类似：
        Enter the number of sets; enter q to stop : 18
        How many sides and how many dice? 6 3
        Here are 18 sets of 3 6-sided throws.
        12 10 6 9 8 14 8 15 9 14 12 17 11 7 10 13 8 14
        How many sets? Enter q to stop: q
``` c
/* manydice.c -- 多次掷骰子的模拟程序 */
/* 与 diceroll.c 一起编译*/
#include <stdio.h>
#include <stdlib.h>   /* 为库函数 srand() 提供原型 */
#include <time.h>     /* 为 time() 提供原型 */
#include "diceroll.h" /* 为roll_n_dice()提供原型，为roll_count变量提供声明 */
int main(void)          //去除了那个外部变量
{
    int dice, roll, sides, status, num;
    srand((unsigned int)time(0)); /* 随机种子 */
    puts("Enter the number of sets; enter q to stop :");
    while (scanf("%d", &num))
    {
        printf("How many sides and how many dice?\n");
        while ((status = (scanf("%d %d", &sides, &dice))) != 2 &&sides == 0)
        {
            printf("You should have entered an integer.");
            printf(" Let's begin again.\n");
            while (getchar() != '\n')
                continue; /* 处理错误的输入 */
            printf("How many sides and how many dice?\n");
            continue; /* 进入循环的下一轮迭代 */
        }
        printf("Here are %d sets of %d %d-sided throws.\n", num, dice, sides);
        for (int i = 0; i < num; i++)
        {
            roll = roll_n_dice(dice, sides);
            printf("%d ", roll);
        }
        printf("\nHow many sets? Enter q to stop: \n");
    }
    printf("GOOD FORTUNE TO YOU!\n");
    return 0;
}
```
``` c
/* diceroll.c -- 掷骰子模拟程序 */
/* 与 mandydice.c 一起编译 */
#include "diceroll.h"
#include <stdio.h>
#include <stdlib.h>          /* 提供库函数 rand()的原型 */
static int rollem(int sides) /* 该函数属于该文件私有 */
{
    int roll;                       //接收随机数的最大值    并记录总共筛了几次 且一个骰子筛一次
    roll = rand() % sides + 1;
    return roll;
}
int roll_n_dice(int dice, int sides)
{
    int d;
    int total = 0;
    if (sides < 2)
    {
        printf("Need at least 2 sides.\n ");
        return -2;
    }
    if (dice < 1)
    {
        printf("Need at least 1 die.\n");
        return -1;
    }
    for (d = 0; d < dice; d++)      //设两个骰子，每个骰子6个面 total值为两个骰子的所得总值
        total += rollem(sides);
    return total;
}
```
``` c
// diceroll.h
extern int roll_count;
int roll_n_dice(int dice, int sides);
```
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
 提供make_array()和show_array()函数的定义，完成该程序。make_array()函数接受两个参数，第1个参数是int类型数组的元素个数，第2个参数是要赋给每个元素的值。该函数调用malloc()创建一个大小合适的数组，将其每个元素设置为指定的值，并返回一个指向该数组的指针。show_array()函数显示数组的内容，一行显示8个数。
``` c
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
int *make_array(int elem, int val)
{
    int *pt = (int *)malloc(elem * sizeof(int));
    for (int i = 0; i < elem; i++)
        pt[i] = val;
    return (int *)pt;
}
void show_array(const int ar[], int n)
{
    int j = 1;
    for (int i = 0; i < n; i++, j++)
    {
        printf("%d", ar[i]);
        if (j % 8 == 0)
            putchar('\n');
    }
            putchar('\n');
}
```
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
``` c
#include <stdio.h>
#include <stdlib.h> //malloc 的原型
char *s_gets(char *, int);
#define size 10
int main(void)
{
    int num; //单词数量
    char(*pt)[size];
    char temp[100] = {0};
    puts("How many words do you wish to enter?");
    scanf("%d", &num);
    getchar();
    pt = (int(*)[size])malloc(num * size * sizeof(char));
    if (pt == NULL) //如果 malloc 申请内存失败
    {
        puts("Memory allocation failed. Goodbye.");
        exit(EXIT_FAILURE);
    }
    printf("Enter %d words now:\n", num);
    s_gets(temp, 100);
    for (int i = 0, l = 0; i < num; i++)
    {
        int j;
        for (j = 0; j < size; j++, l++)
        {
            if (temp[l] == ' ' || temp[l] == '\0') // l是用来统计 temp的总共走向的  i是一维   j是二维   l是字符走向
            {
                l++;
                pt[i][j] = '\0';
                break;
            }
            pt[i][j] = temp[l];
        }
        if (j == size)       //如果用户输入的字符数量超过了9个
        {
            l++;
            pt[i][size - 1] = '\0';
        }
    }
    puts("Here are your words:");
    for (int i = 0; pt[i] && i < num; i++)
        printf("%s\n", pt[i]);
    return 0;
}
char *s_gets(char *st, int n)
{
    char *ret_val;
    int i = 0;
    ret_val = fgets(st, n, stdin);
    if (ret_val)
    {
        while (st[i] != '\n' && st[i] != '\0')
            i++;
        if (st[i] == '\n')
            st[i] = '\0';
        else
            while (getchar() != '\n')
                continue;
    }
    return ret_val;
}
```
----------
