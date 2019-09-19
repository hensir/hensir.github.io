---

title: C-Primer-Puls第九章复习题目和编程练习题的答案
date: 2019-08-24 13:50:00
tags: [题目,答案]
categories: C语言

---


本章内容为《C Primer Plus第六版》第九章复习题和编程练习题

## 复习题
### 第一题
1. 实际参数和形式参数的区别是什么？


----------


### 第二题
2. 根据下面各函数的描述，分别编写它们的ANSI C函数头。注意，只需写出函数头，不用写函数体。
    a.donut()接受一个int类型的参数，打印若干（参数指定数目）个0
    b.gear()接受两个int类型的参数，返回int类型的值
    c.guess()不接受参数，返回一个int类型的值
    d.stuff_it()接受一个double类型的值和double类型变量的地址，把第1个值储存在指定位置

<!--more-->

----------

### 第三题
3. 根据下面各函数的描述，分别编写它们的ANSI C函数头。注意，只需写出函数头，不用写函数体。
    a.n_to_char()接受一个int类型的参数，返回一个char类型的值
    b.digit()接受一个double类型的参数和一个int类型的参数，返回一个int类型的值
    c.which()接受两个可储存double类型变量的地址，返回一个double类型的地址
    d.random()不接受参数，返回一个int类型的值

----------

### 第三题
4. 设计一个函数，返回两整数之和。
``` c
#include <stdio.h>
int add(int, int);
int main(void)
{
    int num1 = 10, num2 = 10;
    printf("%d", add(num1, num2));
    return 0;
}
int add(int num1, int num2)
{
    return num1 + num2;
}
```

----------

### 第五题
5. 如果把复习题4改成返回两个double类型的值之和，应如何修改函数？
```  c
#include <stdio.h>
double add(double, double);
int main(void)
{
    double num1 = 10, num2 = 10;
    printf("%lf", add(num1, num2));
    return 0;
}
double add(double num1, double num2)
{
    return num1 + num2;
}

```

----------

### 第六题
6. 设计一个名为alter()的函数，接受两个int类型的变量x和y，把它们的值分别改成两个变量之和以及两变量之差。
``` c
#include <stdio.h>
void alter(int *, int *);
int main(void)
{
    int x = 10, y = 10;
    alter(&x, &y);
    printf("%d %d", x, y);
    return 0;
}
void alter(int * x, int * y)
{
    *x = *x + *y;
    *y = *x - *y * 2;
}
```


----------

### 第七题
7. 下面的函数定义是否正确？
``` c
void salami(num)
{
    int num, count;
    for (count = 1; count <= num;num++)
    printf(" O salami mio!\n");
}
```

----------

### 第八题
8. 编写一个函数，返回3个整数参数中的最大值。
``` c
#include <stdio.h>
int max(int x, int y, int z);
int main(void)
{
    int x = 6, y = 66, z = 666;
    printf("%d", max(x, y, z));
    return 0;
}
int max(int x, int y, int z)
{
    if (x > y && x > z)
        return x;
    else if (y > x && y > z)
        return y;
    else
        return z;
}
```

----------


### 第九题
9. 给定下面的输出：
        Please choose one of thefollowing:
            1) copy files       2) move files
            2) remove files     4) quit
        Enter the number of your choice:
a.编写一个函数，显示一份有4个选项的菜单，提示用户进行选择（输出如上所示）。
b.编写一个函数，接受两个int类型的参数分别表示上限和下限。该函数从用户的输入中读取整数。如果整数超出规定上下限，函数再次打印菜单（使用a部分的函数）提示用户输入，然后获取一个新值。如果用户输入的整数在规定范围内，该函数则把该整数返回主调函数。如果用户输入一个非 整数字符，该函数应返回4。
c.使用本题a和b部分的函数编写一个最小型的程序。最小型的意思是，该程序不需要实现菜单中各选项的功能，只需显示这些选项并获取有效的响应即可。

----------

## 编程练习

### 第一题
1. 设计一个函数min(x, y)，返回两个double类型值的较小值。在一个简单的驱动程序中测试该函数。
``` c
#include <stdio.h>
double min(double, double);
int main(void)
{
    double x = 3.14, y = 3.1415926;
    printf("min = %lf", min(x, y));
    return 0;
}
double min(double x, double y)
{
    if (x <= y)
    return x;
    else
    return y;
}
```

----------

### 第二题
2. 设计一个函数chline(ch, i, j)，打印指定的字符j行i列。在一个简单的驱动程序中测试该函数。
``` c
#include <stdio.h>
void chline(char, int, int);
int main(void)
{
    int i, j;
    char ch;
    scanf("%c%d%d", &ch, &i, &j);
    chline(ch, i, j);
    return 0;
}
void chline(char ch, int i, int j)
{
    for (int p = 0; p < i; p++)
    {
        for (int b = 0; b < j; b++)
            printf("%c", ch);
        printf("\n");
    }
}
```

----------

### 第三题
3. 编写一个函数，接受3个参数：一个字符和两个整数。字符参数是待打印的字符，第1个整数指定一行中打印字符的次数，第2个整数指定打印指定字符的行数。编写一个调用该函数的程序。

----------

### 第四题
4. 两数的调和平均数这样计算：先得到两数的倒数，然后计算两个倒数的平均值，最后取计算结果的倒数。编写一个函数，接受两个double类型的参数，返回这两个参数的调和平均数。

----------

### 第五题
5. 编写并测试一个函数larger_of()，该函数把两个double类型变量的值替换为较大的值。例如，larger_of(x, y)会把x和y中较大的值重新赋给两个变量。
``` c
#include <stdio.h>
void larger_of(double *, double *);
int main(void)
{
    double q = 666, p = 999;
    larger_of(&q, &p);
    printf("%lf\n%lf", q, p);
    return 0;
}
void larger_of(double *d, double *b)
{
    if (*d > *b)
        *b = *d;
    else
        *d = *b;
}
```

----------

### 第六题
6. 编写并测试一个函数，该函数以3个double变量的地址作为参数，把最小值放入第1个变量，中间值放入第2个变量，最大值放入第3个变量。
``` c
#include <stdio.h>
void match(double *, double *, double *);
int main(void)
{
	double a, b, c;
	while (scanf("%lf%lf%lf", &a, &b, &c) == 3)
	{
		match(&a, &b, &c);
		printf("%.lf	%.lf	%.lf\n", a, b, c);
	}
	return 0;
}
void match(double * a, double * b, double * c)
{
	double a1 = *a, b1 = *b, c1 = *c;
	if (*a > *b && *a > *c)
	{
		if (*c > *b)
		{
			*c = a1;
			*b = c1;
			*a = b1;
		}
		else
		{
			*c = a1;
			*b = b1;
			*a = c1;
		}
	}
	if (*b > *a && *b > *c)
	{
		if(*c > *a)
		{
			*c = b1;
			*b = c1;
		}
		else
		{
			*c = b1;
			*b = a1;
			*a = c1;
		}
	}
	if (*c > *b && *c > *a)
	{
		if(*a > *b)
		{
			*b = a1;
			*a = b1;
		}
	}
}
```

----------

### 第七题
7. 编写一个函数，从标准输入中读取字符，直到遇到文件结尾。程序要报告每个字符是否是字母。如果是，还要报告该字母在字母表中的数值位置。例如，c和C在字母表中的位置都是3。合并一个函数，以一个字符作为参数，如果该字符是一个字母则返回一个数值位置，否则返回-1。

----------

### 第八题
8. 第6章的程序清单6.20中，power()函数返回一个double类型数的正整数次幂。改进该函数，使其能正确计算负幂。另外，函数要处理0的任何次幂都为0，任何数的0次幂都为1（函数应报告0的0次幂未定义，因此把该值处 理为1）。要使用一个循环，并在程序中测试该函数。

----------

### 第九题
9. 使用递归函数重写编程练习8。

----------

### 第十题
10. 为了让程序清单9.8中的to_binary()函数更通用，编写一个to_base_n()函数接受两个在2～10范围内的参数，然后以第2个参数中指定的进制打印第1个参数的数值。例如，to_base_n(129，8)显示的结果为201，也就是129的八进制数。在一个完整的程序中测试该函数。

----------

### 第十一题
11. 编写并测试Fibonacci()函数，该函数用循环代替递归计算斐波那契数。