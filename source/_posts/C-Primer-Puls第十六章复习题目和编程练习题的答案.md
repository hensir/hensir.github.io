---
title: C-Primer-Puls第十六章复习题目和编程练习题的答案
tags:
  - C语言
categories: C Primer Plus
cover: 'https://s1.ax1x.com/2020/04/26/JcBGNQ.png'
abbrlink: be63c193
date: 2020-05-27 17:00:00
---

本章内容为《C Primer Plus第六版》第十六章复习题和编程练习题的答案

## 复习题

### 第一题

1. 下面的几组代码由一个或多个宏组成，其后是使用宏的源代码。在每种情况下代码的结果是什么？这些代码是否是有效代码？（假设其中的变量已声明）

   ```c
   a.
   #define FPM 5280 /*每英里的英尺数*/
   dist = FPM * miles;
   b.
   #define FEET 4
   #define POD FEET + FEET
   plort = FEET * POD;
   c.
   #define SIX = 6;
   nex = SIX;
   d.
   #define NEW(X) X + 5
   y = NEW(y);
   berg = NEW(berg) * lob;
   est = NEW(berg) / NEW(y);
   nilp = lob * NEW(-berg);
   ```




----------

### 第二题

2. 修改复习题1中d部分的定义，使其更可靠。


----------

### 第三题

3. 定义一个宏函数，返回两值中的较小值。


----------

### 第四题

4. 定义EVEN_GT(X, Y)宏，如果X为偶数且大于Y，该宏返回1。


----------

### 第五题

5. 定义一个宏函数，打印两个表达式及其值。例如，若参数为3+4和4*12，则打印：
   3+4 is 7 and 4*12 is 48


----------

### 第六题

6. 创建#define指令完成下面的任务。
     a.创建一个值为25的命名常量。
     b.SPACE表示空格字符。
     c.PS()代表打印空格字符。
     d.BIG(X)代表X的值加3。
     e.SUMSQ(X, Y)代表X和Y的平方和。


----------

### 第七题

7. 定义一个宏，以下面的格式打印名称、值和int类型变量的地址：
   name: fop; value: 23; address: ff464016


----------

### 第八题

8. 假设在测试程序时要暂时跳过一块代码，如何在不移除这块代码的前提下完成这项任务？


----------

### 第九题

9. 编写一段代码，如果定义了PR_DATE宏，则打印预处理的日期。


----------

### 第十题

10. 内联函数部分讨论了3种不同版本的square()函数。从行为方面看，这3种版本的函数有何不同？


----------

### 第十一题

11. 创建一个使用泛型选择表达式的宏，如果宏参数是_Bool类型，对"boolean"求值，否则对"not boolean"求值。


----------

### 第十二题

12. 下面的程序有什么错误？

    ```c
    #include <stdio.h>
    int main(int argc, char argv[])
    {
    	printf("The square root of %f is %f\n", argv[1],sqrt(argv[1]) );
    }
    ```




----------

### 第十三题

13. 假设 scores 是内含 1000 个 int 类型元素的数组，要按降序排序该数组中的值。假设你使用qsort()和comp()比较函数。
    a.如何正确调用qsort()？
    b.如何正确定义comp()？


----------

### 第十四题

14. 假设data1是内含100个double类型元素的数组，data2是内含300个double类型元素的数组。
    a.编写memcpy()的函数调用，把data2中的前100个元素拷贝到data1中。
    b.编写memcpy()的函数调用，把data2中的后100个元素拷贝到data1中。


----------

## 编程练习

### 第一题

1. 开发一个包含你需要的预处理器定义的头文件。

``` c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <Windows.h>
//本自定义头文件库包括以下函数
void SDTC(long, long);          //SetDataToClip         设置指定数据到剪切板
void SCPTC(void);               //SetCursorPosToClip    设置鼠标坐标到剪切板
void CAP(int x, int y);         //ClickAppointPos       鼠标左键点击传入的坐标值
void IAS(char *str);            //InputAppointString    按下指定字符串包含的按键
```
<!--more-->
``` c
void SCPTC(void)
{
    LONG zx = -1;
    LONG zy = -1;
    POINT ptB = {0, 0};
    while (1)
    {
        LPPOINT xy = &ptB;                  //位置变量
        GetCursorPos(xy);                   //获取鼠标当前位置
        if ((zx != xy->x) || (zy != xy->y)) //如果鼠标移动，（即当前的坐标改变则打印出坐标）打印出做坐标。
        {
            system("CLS"); //不要一列输出 在鼠标移动后就进行一个清屏
            printf("x=%d,y=%d\n", xy->x, xy->y);
            zx = xy->x;
            zy = xy->y; //检测鼠标左键的状态  如果鼠标左键被按下
        }
        if (GetKeyState(0x20) < 0 || GetKeyState(0x01) < 0) //如果空格或者鼠标左键被按下 就调用这个函数
            SetDataToClip(zx, zy);
    }
}
void SetDataToClip(long x, long y)
{
    if (!OpenClipboard(NULL) || !EmptyClipboard()) // 打开剪贴板
    {
        printf("打开或清空剪切板出错！/n");
        return;
    }
    HGLOBAL hMen;
    char cz[20]; //直接使用sprintf()就能用了
    sprintf(cz, "%d, %d", x, y);
    TCHAR strText[256]; //这一步用函数可能更稳一些
    strcpy(strText, cz);
    hMen = GlobalAlloc(GMEM_MOVEABLE, ((strlen(strText) + 1) * sizeof(TCHAR))); // 分配全局内存
    if (!hMen)
    {
        printf("分配全局内存出错！/n");
        CloseClipboard(); // 关闭剪切板
        return;
    }
    // 把数据拷贝考全局内存中
    LPSTR lpStr = (LPSTR)GlobalLock(hMen);                       // 锁住内存区
    memcpy(lpStr, strText, ((strlen(strText)) * sizeof(TCHAR))); // 内存复制
    lpStr[strlen(strText)] = (TCHAR)0;                           // 字符结束符
    GlobalUnlock(hMen);                                          // 释放锁
    SetClipboardData(CF_TEXT, hMen);                             // 把内存中的数据放到剪切板上
    CloseClipboard();
    return;
}
void InputAppointString(char *str)
{
	int i = 0;
	Sleep(500);
	while (str[i] != '\0')
	{
		int target = str[i];			//数组中得字符转换成int型的数值 然后传给keybd_event()函数
		Sleep(100);
		keybd_event(target, 0, 0, 0);
		keybd_event(target, 0, 2, 0);
		i++;
	}
	printf("字符串%s输入成功\n", str);
}
void ClickAppointPos(int x, int y)
{
	SetCursorPos(x, y);							   //移动鼠标到指定坐标值
	mouse_event(MOUSEEVENTF_LEFTDOWN, 0, 0, 0, 0); //左键按下
	mouse_event(MOUSEEVENTF_LEFTUP, 0, 0, 0, 0);   //左键松开
	printf("坐标值%d,%d点击成功\n", x, y);
}
void enter(int i)       //修一下  再加一个sleep函数的参数   要高级一些的  也就是可以自定义是否选择设置这个sleep参数
{                       //在高级一些 自定义函数的参数数量 可以一次调用多个参数
	keybd_event(i, 0, 0, 0); //按下win键
	keybd_event(i, 0, 2, 0); //松开
}
```
----------

### 第二题

2. 两数的调和平均数这样计算：先得到两数的倒数，然后计算两个倒数的平均值，最后取计算结果的倒数。使用#define指令定义一个宏“函数”，执行该运算。编写一个简单的程序测试该宏。
``` c
#include <stdio.h>
#define RECI(x, y) (1.0 / (((1.0 / (x)  + 1.0   / (y)))  / 2.0))
int main(void)
{
    printf("%lf", RECI(3.0, 5.0));
    return 0;
}
```

----------

### 第三题

3. 极坐标用向量的模（即向量的长度）和向量相对x轴逆时针旋转的角度来描述该向量。直角坐标用向量的x轴和y轴的坐标来描述该向量（见图16.3）。编写一个程序，读取向量的模和角度（单位：度），然后显示x轴和y轴的坐标。相关方程如下：
   x = r*cos A y = r*sin A

   需要一个函数来完成转换，该函数接受一个包含极坐标的结构，并返回一个包含直角坐标的结构（或返回指向该结构的指针）。

![直角坐标和极坐标](https://s1.ax1x.com/2020/05/27/tA5afx.png)


----------

### 第四题

4. ANSI库这样描述clock()函数的特性：
   #include <time.h>
   clock_t clock (void);
   这里，clock_t是定义在time.h中的类型。该函数返回处理器时间，其单位取决于实现（如果处理器时间不可用或无法表示，该函数将返回-1）。然而，CLOCKS_PER_SEC（也定义在time.h中）是每秒处理器时间单位的数量。因此，两个 clock()返回值的差值除以 CLOCKS_PER_SEC得到两次调用之间经过的秒数。在进行除法运算之前，把值的类型强制转换成double类型，可以将时间精确到小数点以后。编写一个函数，接受一个double类型的参数表示时间延迟数，然后在这段时间运行一个循环。编写一个简单的程序测试该函数。
``` c
#include <stdio.h>
#include <time.h>
void inte(double);
int main(void)
{
    inte(10000000);
    return 0;
}
void inte(double i)
{
    clock_t o = clock();
    for (int j = 0; j < i;)
        j++;
    clock_t s = clock();
    printf("处理器时间间隔为%lf", (double)(s - o) / CLOCKS_PER_SEC);
}
```

----------

### 第五题

5. 编写一个函数接受这些参数：内含int类型元素的数组名、数组的大小和一个代表选取次数的值。该函数从数组中随机选择指定数量的元素，并打印它们。每个元素只能选择一次（模拟抽奖数字或挑选陪审团成员）。另外，如果你的实现有time()（第12章讨论过）或类似的函数，可在srand()中使用这个函数的输出来初始化随机数生成器rand()。编写一个简单的程序测试该函数。
``` c
#include <stdio.h>
#include <time.h>
#include <stdlib.h>
#define SIZE 10
#define FRE 10
void ran(int *, int, int);
int main(void)
{
    int array[SIZE] = {0};
    srand(time(NULL));
    for (int i = 0; i < SIZE; i++)
    {
        array[i] = rand();
        printf("| %5d ", array[i]);
        if (i % 6 == 5)
            putchar('\n');
    }
    putchar('\n');
    ran(array, SIZE, FRE);
    return 0;
}
void ran(int *p, int size, int fre)
{
    int luck[fre];              // 新数组用于存储lucky值(下标) 然后后面要做检重和逐个下标输出
    srand(time(NULL));
    if (fre <= size)
    {
        for (int i = 0; i < fre; i++)
        {
            luck[i] = rand() % size;
            for (int j = 0; j < i; j++) // 检测重复
            {
                while (luck[j] == luck[i])
                {
                    luck[i] = rand() % size;
                    j = -1;         // 重点在这里 luck[i]是有可能等于luck[j]前面已经检查过的数字的  所以每当撞值时我就让j回到0重新检查一边
                }                   // j后面 做个while检查肯定会跳出 接着就是j++ 所以j = -1;  这样就算10 10这样的大的几率都不会撞
            }                       // 当然前者要保证比后者大 也就是fre <= size
        }
        for (int i = 0; i < fre; i++)
        {
            printf("| %5d ", p[luck[i]]);
            if (i % 6 == 5)
                putchar('\n');
        }
    }
    exit(1);
}
```

----------

### 第六题

6. 修改程序清单16.17，使用struct names元素（在程序清单16.17后面的讨论中定义过），而不是double类型的数组。使用较少的元素，并用选定的名字显式初始化数组。
``` c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <time.h>
#include <ctype.h>
#define NUM 100
struct names
{
    char first[40];
    char last[40];
};
void fillarray(struct names *, int n);
void showarray(const struct names *, int n);
int comp(const void *p1, const void *p2);
int main(void)
{
    struct names staff[100];
    fillarray(staff, NUM);
    puts("Random list:");
    showarray(staff, NUM);
    qsort(staff, NUM, sizeof(struct names), comp);
    puts("\nSorted list:");
    showarray(staff, NUM);
    return 0;
}
void fillarray(struct names *ar, int n)
{
    srand(time(NULL));
    int j = 0;
    for (int i = 0; i < n; i++) // ar[i].first[6] = '\0';
    {                           // 6这个常量是我设置的 也就是我通融的
        for (j = 0; j < 6; j++)
        {
            ar[i].first[j] = (rand() % 57 + 65);                          //  可以看到这两种形式 和指针一模一样
            while (!(isalpha(ar[i].first[j])) || ispunct(ar[i].first[j])) //只是表示形式而不是声明这种大事  ，编译器给我们优化过去了
                ar[i].first[j] = (rand() % 57 + 65);
        }
        ar[i].first[6] = '\0';
        for (j = 0; j < 6; j++)
        {
            ar[i].last[j] = (rand() % 57 + 65);
            while (!(isalpha(ar[i].last[j])) || ispunct(ar[i].last[j]))
                ar[i].last[j] = (rand() % 57 + 65);
        }
        ar[i].first[6] = '\0';
    }
}
void showarray(const struct names *ar, int n)
{
    for (int i = 0; i < n; i++)
        printf("%d first: %6s  last: %6s\n", i, ar[i].first, ar[i].last);
}
int comp(const void *p1, const void *p2)
{
    const struct names *ps1 = (const struct names *)p1;
    const struct names *ps2 = (const struct names *)p2;
    int res;
    res = strcmp(ps1->first, ps2->first);
    if (res != 0)
        return res;
    else
        return strcmp(ps1->last, ps2->last);
}
```

----------

### 第七题

7. 下面是使用变参函数的一个程序段：
   ```c
   #include <stdio.h>
   #include <stdlib.h>
   #include <stdarg.h>
   void show_array(const double ar[], int n);
   double * new_d_array(int n, ...);
   int main()
   {
      double * p1;
      double * p2;
      p1 = new_d_array(5, 1.2, 2.3, 3.4, 4.5, 5.6);
      p2 = new_d_array(4, 100.0, 20.00, 8.08, -1890.0);
      show_array(p1, 5);
      show_array(p2, 4);
      free(p1);
      free(p2);
      return 0;
   }
   ```

   new_d_array()函数接受一个int类型的参数和double类型的参数。该函数返回一个指针，指向由malloc()分配的内存块。int类型的参数指定了动态数组中的元素个数，double类型的值用于初始化元素（第1个值赋给第1个元素，以此类推）。编写show_array()和new_d_array()函数的代码，完成这个程序。
``` c
#include <stdio.h>
#include <stdlib.h>
#include <stdarg.h>
void show_array(const double ar[], int n);
double *new_d_array(int n, ...);
int main()
{
    double *p1;
    double *p2;
    p1 = new_d_array(5, 1.2, 2.3, 3.4, 4.5, 5.6);
    p2 = new_d_array(4, 100.0, 20.00, 8.08, -1890.0);
    show_array(p1, 5);
    show_array(p2, 4);
    free(p1);
    free(p2);
    return 0;
}
void show_array(const double ar[], int n)
{
    for (int i = 0; i < n; i++)
        printf("%lf \n", ar[i]);
}
double *new_d_array(int n, ...)
{
    va_list ap;
    va_start(ap, n);
    double *p = (double *) malloc(n * sizeof(double));
    for (int i = 0; i < n; i++)
        p[i] = va_arg(ap, double);
    va_end(ap);
    return p;
}

```