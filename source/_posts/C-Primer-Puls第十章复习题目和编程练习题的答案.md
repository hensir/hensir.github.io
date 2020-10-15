---
title: C-Primer-Puls第十章复习题目和编程练习题的答案
tags:
  - C语言
categories: C Primer Plus
cover: 'https://s1.ax1x.com/2020/04/26/JcBGNQ.png'
abbrlink: d872b2ec
date: 2019-10-03 20:30:00
---


本章内容为《C Primer Plus第六版》第十章复习题和编程练习题的答案

## 复习题
### 第一题
1. 下面的程序将打印什么内容？
``` c
        #include <stdio.h>
        int main(void)
        {
            int ref[] = {8, 4, 0, 2};
            int *ptr;
            int index;
            for (index = 0, ptr = ref; index < 4; index++, ptr++)
                printf("%d %d\n", ref[index], *ptr);
            return 0;
        }
```
----------


### 第二题
2. 在复习题1中，ref有多少个元素？

<!--more-->

----------


### 第三题
3. 在复习题1中，ref的地址是什么？ref + 1是什么意思？++ref指向什么？

----------


### 第四题
4. 在下面的代码中，\*ptr和\*(ptr + 2)的值分别是什么？

        a.
        int *ptr;
        int torf[2][2] = {12, 14, 16};
        ptr = torf[0];
        b.
        int * ptr;
        int fort[2][2] = { {12}, {14,16} };
        ptr = fort[0];

----------


### 第五题
5. 在下面的代码中，\*\*ptr和\*\*(ptr + 1)的值分别是什么？

        a. int (*ptr)[2];
        int torf[2][2] = {12, 14, 16};
        ptr = torf;
        b. int (*ptr)[2];
        int fort[2][2] = { {12}, {14,16} };
        ptr = fort;

----------


### 第六题
6. 假设有下面的声明：
        int grid[30][100];
        a.用1种写法表示grid[22][56]
        b.用2种写法表示grid[22][0]
        c.用3种写法表示grid[0][0]

----------


### 第七题
7. 正确声明以下各变量：
        a.digits是一个内含10个int类型值的数组
        b.rates是一个内含6个float类型值的数组
        c.mat是一个内含3个元素的数组，每个元素都是内含5个整数的数组
        d.psa是一个内含20个元素的数组，每个元素都是指向int的指针
        e.pstr是一个指向数组的指针，该数组内含20个char类型的值

----------


### 第八题
8. 完成以下要求:
        a.声明一个内含6个int类型值的数组，并初始化各元素为1、2、4、8、16、32
        b.用数组表示法表示a声明的数组的第3个元素（其值为4)
        c.假设编译器支持C99/C11标准，声明一个内含100个int类型值的数组，并初始化最后一个元素为-1，其他元素不考虑
        d.假设编译器支持C99/C11标准，声明一个内含100个int类型值的数组，并初始化下标为5、10、11、12、3的元素为101，其他元素不考虑

----------


### 第九题
9. 内含10个元素的数组下标范围是什么？

----------


### 第十题
10. 假设有下面的声明：
        float rootbeer[10], things[10][5], *pf, value = 2.2;
        int i = 3;
        判断以下各项是否有效：
        a.rootbeer[2] = value;
        b.scanf("%f", &rootbeer);
        c.rootbeer = value;
        d.printf("%f", rootbeer);
        e.things[4][4] = rootbeer[3];
        f.things[5] = rootbeer;
        g.pf = value;
        h.pf = rootbeer;

----------


### 第十一题
11. 声明一个800×600的int类型数组。

----------


### 第十二题
12. 下面声明了3个数组：
        double trots[20];
        short clops[10][30];
        long shots[5][10][15];
        a.分别以传统方式和以变长数组为参数的方式编写处理trots数组的void函数原型和函数调用
        b.分别以传统方式和以变长数组为参数的方式编写处理clops数组的void函数原型和函数调用
        c.分别以传统方式和以变长数组为参数的方式编写处理shots数组的void函数原型和函数调用

----------


### 第十三题
13. 下面有两个函数原型：
        void show(const double ar[], int n);// n是数组元素的个数
        void show2(const double ar2[][3], int n);// n是二维数组的行数
        a.编写一个函数调用，把一个内含8、3、9和2的复合字面量传递给show()函数。
        b.编写一个函数调用，把一个2行3列的复合字面量（8、3、9作为第1行，5、4、1作为第2行）传递给show2()函数。

----------

## 编程练习
### 第一题
1. 修改程序清单10.7的rain.c程序，用指针进行计算（仍然要声明并初始化数组）。
``` c
#include <stdio.h>
#define MONTHS 12
#define YEARS 5
int main(void)
{
    const float rain[YEARS][MONTHS] =
        {{4.3, 4.3, 4.3, 3.0, 2.0, 1.2, 0.2, 0.2, 0.4, 2.4, 3.5, 6.6},
         {8.5, 8.2, 1.2, 1.6, 2.4, 0.0, 5.2, 0.9, 0.3, 0.9, 1.4, 7.3},
         {9.1, 8.5, 6.7, 4.3, 2.1, 0.8, 0.2, 0.2, 1.1, 2.3, 6.1, 8.4},
         {7.2, 9.9, 8.4, 3.3, 1.2, 0.8, 0.4, 0.0, 0.6, 1.7, 4.3, 6.2},
         {7.6, 5.6, 3.8, 2.8, 3.8, 0.2, 0.0, 0.0, 0.0, 1.3, 2.6, 5.2}};
    int year, month;
    float subtot, total;
    float (* ptr)[MONTHS] = rain;
    printf(" YEAR  RAINFALL (inches)\n");
    for (year = 0, total = 0; year < YEARS; year++)
    {
        for (month = 0, subtot = 0; month < MONTHS; month++)
            //subtot += rain[year][month];
            subtot += ptr[year][month];
            //subtot += *(ptr[year] + month);
            //subtot += *(*(ptr + year) + month);
        printf("%5d %15.1f\n", 2010 + year, subtot);
        total += subtot;
    }
    printf("\nThe yearly average is %.1f inches.\n\n", total / YEARS);
    printf("MONTHLY AVERAGES:\n\n");
    printf(" Jan Feb Mar Apr May Jun Jul Aug Sep Oct ");
    printf(" Nov Dec\n");
    for (month = 0; month < MONTHS; month++)
    {
        for (year = 0, subtot = 0; year < YEARS; year++)
            //subtot += rain[year][month];
            //subtot += ptr[year][month];
            //subtot += *(ptr[year] + month);
            subtot += *(*(ptr + year) + month);
        printf("%4.1f ", subtot / YEARS);
    }
    printf("\n");
    return 0;
}
```

----------

### 第二题
2. 编写一个程序，初始化一个double类型的数组，然后把该数组的内容拷贝至3个其他数组中（在main()中声明这4个数组）。使用带数组表示法的函数进行第1份拷贝。使用带指针表示法和指针递增的函数进行第2份拷贝。把目标数组名、源数组名和待拷贝的元素个数作为前两个函数的参数。第3个函数以目标数组名、源数组名和指向源数组最后一个元素后面的元素的指针。也就是说，给定以下声明，则函数调用如下所示：

        double source[5] = {1.1, 2.2, 3.3, 4.4, 5.5};
        double target1[5];
        double target2[5];
        double target3[5];
        copy_arr(target1, source, 5);
        copy_ptr(target2, source, 5);
        copy_ptrs(target3,source, source + 5);
``` c
#include <stdio.h>
void copy_arr(double *, double *, int);
void copy_ptr(double *, double *, int);
void copy_ptrs(double *, double *, double *);
int main(void)
{
    double source[5] = {1.1, 2.2, 3.3, 4.4, 5.5};
    double target1[5], target2[5], target3[5];
    copy_arr(target1, source, 5);
    copy_ptr(target2, source, 5);
    copy_ptrs(target3, source, source + 5);
    return 0;
}
void copy_arr(double target[], double source[], int num)    //数组表示法
{
    for (int index = 0; index < num; index++)
    {
        target[index] = source[index];
        printf("%.1lf ", target[index]);
    }
    printf("\n");
}
void copy_ptr(double *target, double *source, int num)  //指针递增
{
    double *pt = target;
    for (int index = 0; index < num; index++)
    {
        *(pt++) = *(source++);
        printf("%.1lf ", *(target + index));
    }
    printf("\n");
}
void copy_ptrs(double *target, double *source, double *num) //指针指向数组最后一个元素的后面    //指针加法
{
    double *pt = source;
    for (int index = 0; pt < num; pt++, index++)
    {
        *(target + index) = *(source + index);
        printf("%.1lf ", target[index]);
    }
}
```
----------

### 第三题
3. 编写一个函数，返回储存在int类型数组中的最大值，并在一个简单的程序中测试该函数。
``` c
#include <stdio.h>
int max(int *, int);
int main(void)
{
    int array[10] =
        {0, 2, 5, 8, 4, 9, 7, 3, 1, 6};
    printf("%d", max(array, 10));
    return 0;
}
int max(int *pt, int num)
{
    int max = 0;
    for (int index = 0; index < num; index++)
    {
        if (pt[index] > max)
            max = pt[index];
    }
    return max;
}
```
----------

### 第四题
4. 编写一个函数，返回储存在double类型数组中最大值的下标，并在一个简单的程序中测试该函数。
``` c
#include <stdio.h>
int index_max(double *, int);
int main(void)
{
    double array[10] =
        {0, 2.2, 5.5, 8.8, 4.4, 9.9, 7.7, 3.3, 1.1, 6.6};
    printf("%d", index_max(array, 10));
    return 0;
}
int index_max(double *pt, int num)
{
    int index, max = 0;
    for (index = 1; index < num; index++)
    {
        if (pt[index] > pt[max])
            max = index;
    }
    return max;
}
```
----------

### 第五题
5. 编写一个函数，返回储存在double类型数组中最大值和最小值的差值，并在一个简单的程序中测试该函数。
``` c
#include <stdio.h>
double Dv(double *, int);
int main(void)
{
    double array[10] =
        {10, 2.2, 5.5, 8.8, 4.4, 9.9, 7.7, 3.3, 1.1, 6.6};
    printf("%.1lf", Dv(array, 10));
    return 0;
}
double Dv(double *array, int num)
{
    double max = array[0], min = array[0];
    for (int index = 0; index < num; index++)
    {
        if (array[index] > max)
            max = array[index];
        else if (array[index] < min)
            min = array[index];
    }
    return (max - min);
}
```
----------

### 第六题
6. 编写一个函数，把double类型数组中的数据倒序排列，并在一个简单的程序中测试该函数。
``` c
#include <stdio.h>
void RO(double *, int);
void RT(double *, int);
int main(void)
{
    double array[10] = {1.1, 2.2, 3.3, 4.4, 5.5, 6.6, 7.7, 8.8, 9.9, 10};
    RO(array, 10);
    RT(array, 10);
    for (int index = 0; index < 10; index++)
        printf("%.1lf ", array[index]);
    return 0;
}
void RO(double *pt, int num)
{
    double array[10];
    for (int index = 0, xedni = num - 1; xedni >= 0; index++, xedni--)
        array[index] = pt[xedni];
    for (int index = 0; index < num; index++)
        pt[index] = array[index];
}
void RT(double *pt, int num)
{
    double LT;
    for (int index = 0, xedni = num - 1; xedni >= num / 2; index++, xedni--)
    {
        LT = pt[xedni];
        pt[xedni] = pt[index];
        pt[index] = LT;
    }
}
```
----------

### 第七题
7. 编写一个程序，初始化一个double类型的二维数组，使用编程练习2中的一个拷贝函数把该数组中的数据拷贝至另一个二维数组中（因为二维数组是数组的数组，所以可以使用处理一维数组的拷贝函数来处理数组中的每个子数组）。
``` c
#include <stdio.h>
void copy_arr(double *, double *, int);
int main(void)
{
    double source[5] = {1.1, 2.2, 3.3, 4.4, 5.5};
    double target1[5][5];
    copy_arr(target1, source, 5);
    for (int index = 0; index < 5; index++)
        printf("%.1lf ", *(*(target1 + 0) + index));
    return 0;
}
void copy_arr(double target[], double source[], int num)
{
    for (int index = 0; index < num; index++)
    {
        target[index] = source[index];
        printf("%.1lf ", target[index]);
    }
    printf("\n");
}
```
----------

### 第八题
8. 使用编程练习2中的拷贝函数，把一个内含7个元素的数组中第3～第5个元素拷贝至内含3个元素的数组中。该函数本身不需要修改，只需要选择合适的实际参数（实际参数不需要是数组名和数组大小，只需要是数组元素的地址和待处理元素的个数）。
``` c
#include <stdio.h>
void copy_ptr(double *target, double *source, int num);
int main(void)
{
    double array[7] = {1.1, 2.2, 3.3, 4.4, 5.5, 6.6, 7.7};
    double target[3];
    copy_ptr(target, array + 2, 3);
    return 0;
}
void copy_ptr(double *target, double *source, int num)
{
    double *pt = target;
    for (int index = 0; index < num; index++)
    {
        *(pt++) = *(source++);
        printf("%.1lf ", *(target + index));
    }
    printf("\n");
}
```
----------

### 第九题
9. 编写一个程序，初始化一个double类型的3×5二维数组，使用一个处理变长数组的函数将其拷贝至另一个二维数组中。还要编写一个以变长数组为形参的函数以显示两个数组的内容。这两个函数应该能处理任意N×M数组 （如果编译器不支持变长数组，就使用传统C函数处理N×5的数组）。
``` c
#include <stdio.h>
void copy_VLA(int, int, double[*][*], double[*][*]);
void put_VLA(int, int, double[*][*]);
int main(void)
{
    double array[3][5] =
        {{10, 11, 12, 13, 14},
         {20, 21, 22, 23, 24},
         {30, 31, 32, 33, 34}};
    double target[3][5];
    copy_VLA(3, 5, array, target);
    put_VLA(3, 5, array);
    put_VLA(3, 5, target);
    return 0;
}
void copy_VLA(int i, int j, double pt[i][j], double target[i][j])
{
    for (int k = 0; k < i; k++)
    {
        for (int l = 0; l < j; l++)
            target[k][l] = pt[k][l];
    }
}
void put_VLA(int i, int j, double pt[i][j])
{
    for (int k = 0; k < i; k++)
    {
        for (int l = 0; l < j; l++)
            printf("%.lf ", pt[k][l]);
        putchar('\n');
    }
    putchar('\n');
}
```
----------

### 第十题
10. 编写一个函数，把两个数组中相对应的元素相加，然后把结果储存到第3个数组中。也就是说，如果数组1中包含的值是2、4、5、8，数组2中包含的值是1、0、4、6，那么该函数把3、4、9、14赋给第3个数组。函数接受3个数组名和一个数组大小。在一个简单的程序中测试该函数。
``` c
#include <stdio.h>
void array_add(double *, double *, double *, int);
int main(void)
{
    double array1[9] = {1, 2, 3, 4, 5, 6, 7, 8, 9};
    double array2[9] = {9, 8, 7, 6, 5, 4, 3, 2, 1};
    double array3[9];
    array_add(array1, array2, array3, 9);
    return 0;
}
void array_add(double *array1, double *array2, double *array3, int num)
{
    for (int index = 0; index < num; index++)
    {
        array3[index] = array1[index] + array2[index];
        printf("%.lf ", array3[index]);
    }
    printf("\n");
}
```
----------

### 第十一题
11. 编写一个程序，声明一个int类型的3×5二维数组，并用合适的值初始化它。该程序打印数组中的值，然后各值翻倍（即是原值的2倍），并显示出各元素的新值。编写一个函数显示数组的内容，再编写一个函数把各元素的值翻倍。这两个函数都以函数名和行数作为参数。
``` c
#include <stdio.h>
void t_times(int (*)[5], int);
void putarray(int (*)[5], int); //二维数组省略形参指针名
int main(void)
{
    int array[3][5] =
        {{10, 11, 12, 13, 14},
         {20, 21, 22, 23, 24},
         {30, 31, 32, 33, 34}};
    putarray(array, 3);
    t_times(array, 3);
    putarray(array, 3);
    return 0;
}
void t_times(int (*pt)[5], int num)
{
    for (int i = 0; i < num; i++)
    {
        for (int j = 0; j < 5; j++)
            pt[i][j] = pt[i][j] * 2;
    }
}
void putarray(int (*pt)[5], int num)
{
    for (int i = 0; i < num; i++)
    {
        for (int j = 0; j < 5; j++)
            printf("%d ", *(*(pt + i) + j));
        putchar('\n');
    }
    putchar('\n');
}
```
----------

### 第十二题
12. 重写程序清单10.7的rain.c程序，把main()中的主要任务都改成用函数来完成。
``` c
#include <stdio.h>
#define MONTHS 12
#define YEARS 5
float M_sum(float (*)[MONTHS], int);    //五年中每月的降水量总和
void M_average(float (*)[MONTHS], int); //五年中每月的降水量平均值
int main(void)
{
    const float rain[YEARS][MONTHS] =
        {{4.3, 4.3, 4.3, 3.0, 2.0, 1.2, 0.2, 0.2, 0.4, 2.4, 3.5, 6.6},
         {8.5, 8.2, 1.2, 1.6, 2.4, 0.0, 5.2, 0.9, 0.3, 0.9, 1.4, 7.3},
         {9.1, 8.5, 6.7, 4.3, 2.1, 0.8, 0.2, 0.2, 1.1, 2.3, 6.1, 8.4},
         {7.2, 9.9, 8.4, 3.3, 1.2, 0.8, 0.4, 0.0, 0.6, 1.7, 4.3, 6.2},
         {7.6, 5.6, 3.8, 2.8, 3.8, 0.2, 0.0, 0.0, 0.0, 1.3, 2.6, 5.2}};
    float total = M_sum(rain, YEARS);
    printf("\nThe yearly average is %.1f inches.\n\n", total / YEARS); //五年的降水量平均值
    M_average(rain, YEARS);
    return 0;
}
float M_sum(float (*rain)[MONTHS], int num)
{
    int year, month;
    float subtot, total;
    printf(" YEAR  RAINFALL (inches)\n");
    for (year = 0, total = 0; year < YEARS; year++)
    {
        for (month = 0, subtot = 0; month < MONTHS; month++)
            subtot += rain[year][month];
        printf("%5d %15.1f\n", 2010 + year, subtot);
        total += subtot;
    }
    return total;
}
void M_average(float (*rain)[MONTHS], int num)
{
    int year, month;
    float subtot, total;
    printf("MONTHLY AVERAGES:\n\n");
    printf(" Jan Feb Mar Apr May  Jun Jul Aug Sep Oct ");
    printf(" Nov Dec\n");
    for (month = 0; month < MONTHS; month++)
    {
        for (year = 0, subtot = 0; year < YEARS; year++)
            subtot += rain[year][month];
        printf("%4.1f ", subtot / YEARS);
    }
    printf("\n");
}
```
----------

### 第十三题
13. 编写一个程序，提示用户输入3组数，每组数包含5个double类型的数（假设用户都正确地响应，不会输入非数值数据）。该程序应完成下列任务。
a.把用户输入的数据储存在3×5的数组中
b.计算每组（5个）数据的平均值
c.计算所有数据的平均值
d.找出这15个数据中的最大值
e.打印结果每个任务都要用单独的函数来完成（使用传统C处理数组的方式）。完成任务b，要编写一个计算并返回一维数组平均值的函数，利用循环调用该函数3次。对于处理其他任务的函数，应该把整个数组作为参数，完成任务c和d的函数应把结果返回主调函数。
``` c
#include <stdio.h>
#define SLEN 5
#define LIM 3
void getarray(double *);            //赋值数组                  //使用SLEN和LIM的积来判断总共需要多少次循环 而非for嵌套 14题为for嵌套
double ave_group(double *, int);         //输出数组各行的平均值
void putarray(double (*)[SLEN], int);    //输出数组
double ave_total(double (*)[SLEN], int); //所有数值的平均值
double max_all(double (*)[SLEN], int);   //所有数值的最大值
int main(void)
{
    double array[LIM][SLEN] =
        {{0.1, 0.2, 0.3, 0.4, 0.5},
         {1.1, 1.2, 1.3, 1.4, 1.5},
         {2.1, 2.2, 2.3, 2.4, 2.5}};
    getarray(array);
    putchar('\n');
    putarray(array, LIM);
    putchar('\n');
    for (int i = 0; i < LIM; i++)
        printf("数组第%d行五个元素的平均值为%.3lf\n", i, ave_group(&array[i], SLEN));
    putchar('\n');
    printf("数组中所有数值的平均值为%lf\n", ave_total(array, LIM));
    putchar('\n');
    printf("数组中所有数值的最大值为%lf\n", max_all(array, LIM));
    return 0;
}
double max_all(double (*pt)[SLEN], int num)
{
    double max = pt[0][0];
    double *ptr = *pt;
    for (int i = 0; i < num; i++)
    {
        for (int j = 0; j < SLEN; j++)
        {
            if (*ptr++ > max)
                max = *ptr;
        }
    }
    return max;
}
double ave_total(double (*pt)[SLEN], int num)
{
    double total;
    for (int i = 0; i < num; i++)
    {
        for (int j = 0; j < SLEN; j++)
            total += pt[i][j];
    }
    return total / (LIM * SLEN);
}
double ave_group(double *pt, int num)
{
    double total;
    for (int i = 0; i < num; i++)
        total += pt[i];
    return (total / SLEN);
}
void getarray(double *pt)
{
    int index = 1;
    printf("数组的第%d个元素的值为", index++);
    while (scanf("%lf", &*(pt)))
    {
        *pt++;
        if (index > LIM * SLEN)
            break;
        printf("\n数组的第%d个元素的值为", index++);
    }
}
void putarray(double (*array)[SLEN], int num)
{
    for (int i = 0; i < num; i++)
    {
        for (int j = 0; j < SLEN; j++)
            printf("%-10.2lf ", array[i][j]);
        putchar('\n');
    }
}
```
----------

### 第十四题
14. 以变长数组作为函数形参，完成编程练习13。
``` c
#include <stdio.h>
#define SLEN 5
#define LIM 3
void getarray(int, double[*]);            //给数组赋值
void putarray(int, int, double[*][*]);    //打印数组
double ave_group(int, int, double ar[*][*]); //各行平均值
double ave_total(int, int, double[*][*]); //所有数值平局值
double max_all(int, int, double[*][*]);   //所有数值的最大值
//double ave_grou2(int i, int j, double *(*(pt + i) + j));        //这句无效  都是数组形参 如果是指针形参该怎么声明 且 省略形参指针名
int main(void)
{
    double array[LIM][SLEN] =
        {{0.1, 0.2, 0.3, 0.4, 0.5},
         {1.1, 1.2, 1.3, 1.4, 1.5},
         {2.1, 2.2, 2.3, 2.4, 2.5}};
    getarray(LIM, array);
    putchar('\n');
    putarray(LIM, SLEN, array);
    putchar('\n');
    for (int i = 0; i < LIM; i++)
        printf("数组第%d行五个元素的平均值为%.3lf\n", i, ave_group(i, SLEN, array));
    putchar('\n');
    printf("数组中所有数值的平均值为%lf\n", ave_total(LIM, SLEN, array));
    putchar('\n');
    printf("数组中所有数值的最大值为%lf\n", max_all(LIM, SLEN, array));
    return 0;
}
double ave_group(int i, int j, double pt[i][j])
{
    double total;
    for (int k = 0; k < j; k++)
        total += pt[i][k];
    return (total / SLEN);
}
double ave_total(int i, int j, double pt[i][j])
{
    double total;
    for (int q = 0; q < i; q++)
    {
        for (int b = 0; b < j; b++)
            total += pt[q][b];
    }
    return total / (LIM * SLEN);
}
void putarray(int i, int j, double pt[i][j])
{
    for (int q = 0; q < i; q++)
    {
        for (int b = 0; b < j; b++)
            printf("%-10.2lf ", pt[q][b]);
        putchar('\n');
    }
}
void getarray(int num, double pt[num])
{
    int index = 1;
    for (int i = 0; i < num; i++)
    {
        for (int k = 0; k < SLEN; k++)
        {
            printf("数组的第%d个元素的值为", index++);
            scanf("%lf", &*(pt));
            *pt++;
        }
    }
}
double max_all(int i, int j, double pt[i][j])
{
    double max = pt[0][0];
    for (int n = 0; n < i; n++)
    {
        for (int m = 0; m < j; m++)
        {
            if (pt[n][m] > max)
                max = pt[n][m];
        }
    }
    return max;
}
```