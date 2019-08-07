---
title: C-Primer-Puls第五章编程练习答案
date: 2019-05-16 15:25:51
tags: [C语言,答案]
categories: 代码
---



本文章为《C Primer Plus第六版》第五章编程练习的答案


## 第一题
1.编写一个程序，把用分钟表示的时间转换成用小时和分钟表示的时间。
使用#define或const创建一个表示60的符号常量或const变量。
通过while 循环让用户重复输入值，直到用户输入小于或等于0的值才停止循环。

``` c
#include <stdio.h>
#include <stdlib.h>
#define hour 60
int main(void)
{
    int time;
    printf("请输入时间（单位：分钟）");
    scanf("%d", &time);     
    while (time > 0)		
    {
        printf("当前时间为%d小时%d分钟\n", time / hour, time % hour);
	    scanf("%d", &time);
    }
	return 0;
}
```

<!--more-->

## 第二题
2.编写一个程序，提示用户输入一个整数，然后打印从该数到比该数大 10的所有整数（例如，用户输入5，则打印5～15的所有整数，包括5和 15）。
要求打印的各值之间用一个空格、制表符或换行符分开。

``` c
#include <stdlib.h>
#include <stdio.h>
int main(void)
{
    int num;
    printf("请输入一个整数");
    scanf("%d", &num);
    int index = num + 10;
    while (num <= index)
	{
	    printf("%d  ", num);
	    num++;
    }
    return 0;
}
```

## 第三题
3.编写一个程序，提示用户输入天数，然后将其转换成周数和天数。
例如，用户输入18，则转换成2周4天。
以下面的格式显示结果：18 days are 2 weeks, 4 days.
通过while循环让用户重复输入天数，当用户输入一个非正值时（如0 或 - 20），循环结束。

``` c
#include <stdio.h>
#include <stdlib.h>
#define week 7
int main(void)
{
    int days;
	printf("请输入天数");
    scanf("%d", &days);
    while (days > 0)
    {
	    printf("%d转换为%d周%d天",days, days / week, days % week);
	    scanf("%d", &days);
    }
    return 0;
}
```

    
## 第四题
4.编写一个程序，提示用户输入一个身高（单位：厘米），并分别以厘米和英寸为单位显示该值，允许有小数部分。
程序应该能让用户重复输入身 高，直到用户输入一个非正值。
其输出示例如下：
	Enter　a　height　in　centimeters : 182											
	182.0　cm　 = 5　feet, 11.7　inches
	Enter　a　height　in　centimeters　(<= 0　to　quit) : 168.7
	168.0　cm　 = 5　feet, 6.4　inches
	Enter　a　height　in　centimeters　(<= 0　to　quit) : 0
	bye


``` c
#include <stdio.h>
#include <stdlib.h>
int main(void)					
{
    double cm, inches;
    int feet;
    printf("请输入一个您的身高：\n");
    scanf("%lf", &cm);
    while (cm)													
    {															
        feet = (int)(cm * 0.0328084);							
	    printf("厘米为%.lf\n英寸为%d\n英尺为%.1f\n", cm, feet, (cm * 0.3937008) - (feet * 12));	
	    printf("请输入您的身高（< 0 to quit）");
	    scanf("%lf", &cm);
    }
    printf("Byebye!\n");
    return 0;
}
```

## 第五题
5.修改程序addemup.c（程序清单5.13），你可以认为addemup.c是计算20天里赚多少钱的程序
（假设第1天赚$1、第2天赚$2、第3天赚$3，以此类 推）。
修改程序，使其可以与用户交互，根据用户输入的数进行计算（即， 用读入的一个变量来代替20）。

``` c
#include <stdio.h>
#include <stdlib.h>
int main(void)
{
    int count, d20;
    printf("请输入第一天所得钱数");
    scanf("%d", &count);
    d20 = count + 20;
    while (count < d20)
    {
        printf("count = %d\n", count);
        count++;
    }
    printf("count = %d\n", count);	
    return 0;
}
```


## 第六题
6.修改编程练习5的程序，使其能计算整数的平方和
（可以认为第1天赚 $1、第2天赚$4、第3天赚$9，以此类推，这看起来很不错）。
C没有平方函数，但是可以用n * n来表示n的平方。

``` c
#include <stdio.h>
#include <stdlib.h>
int main(void)
{
    int count, d20;
    printf("请输入第一天所得钱数");
    scanf("%d", &count);
    d20 = count + 20;
    while (count < d20)
    {
	    printf("count = %d\n", count * count);  只改了一个参数 就是n * n
	    count++;
    }
    printf("count = %d\n", count);	
    return 0;
}
```

## 第七题
7.编写一个程序，提示用户输入一个double类型的数，并打印该数的立方值。
自己设计一个函数计算并打印立方值。main()函数要把用户输入的值传递给该函数。

``` c
#include <stdio.h>
#include <stdlib.h>
int process(double db);
int main(void)
{
    double dl;
    printf("请输入一个数值:\n");
    scanf("%lf", &dl);
    process(dl);    返回值划不来
    system("pause");
    return 0;
}
int process(double db)
{
    printf("%f\n", db * db * db);
    return 0;
}
```

## 第八题
8.编写一个程序，显示求模运算的结果。
把用户输入的第1个整数作为 求模运算符的第2个运算对象，该数在运算过程中保持不变。
用户后面输入的数是第1个运算对象。当用户输入一个非正值时，程序结束。其输出示例 如下：
 This　program　computes　moduli.
 Enter　an　integer　to　serve　as　the　second　operand:　256
 Now　enter　the　first　operand : 438
 438 % 256　is　182
 Enter　next　number　for　first　operand　(<= 0　to　quit) : 1234567
 1234567 % 256　is　135
 Enter　next　number　for　first　operand　(<= 0　to　quit) : 0
 Done

``` c
#include <stdio.h>
#include <stdlib.h>
int main(void)
{
    int one, two;
    printf("This program computer moduli.\n");
    printf("Enter an integer to serve as the second operand: ");
    scanf("%d", &two);
    printf("Now enter the first operand : ");
    scanf("%d", &one);
    while (one > 0)
    {
        printf("%d %% %d is %d\n", one, two, one % two);
        printf("Enter next number for first operand (<= 0 to quit) : ");
        scanf("%d", &one);
    }
    printf("Done\n");
    return 0;
}
```
    
## 第九题
9.编写一个程序，要求用户输入一个华氏温度。
程序应读取double类型 的值作为温度值，并把该值作为参数传递给一个用户自定义的函数Temperatures()。
该函数计算摄氏温度和开氏温度，并以小数点后面两位数字 的精度显示3种温度。
要使用不同的温标来表示这3个温度值。下面是华氏温 度转摄氏温度的公式：
摄氏温度 = 5.0 / 9.0 * (华氏温度 - 32.0)
开氏温标常用于科学研究，0表示绝对零，代表最低的温度。下面是摄 氏温度转开氏温度的公式：
开氏温度 = 摄氏温度 + 273.16
Temperatures()函数中用const创建温度转换中使用的变量。
在main()函数 中使用一个循环让用户重复输入温度，当用户输入 q 或其他非数字时，循环 结束。
scanf()函数返回读取数据的数量，所以如果读取数字则返回1，如果 读取q则不返回1。
可以使用 == 运算符将scanf()的返回值和1作比较，测试两值是否相等。

``` c
#include <stdio.h>
#include <stdlib.h>
int main9(void)
{
    double HS;
    printf("请输入一个华氏温度值");
    while (scanf("%lf", &HS) == 1)			
    {
	    Temperatures(HS);
	    printf("请输入一个华氏温度值");	
    }									
    printf("Byebye!\n");
    return 0;
}
int Temperatures(double HS)	
{
    const double SS = 5.0 / 9.0 * (HS - 32.0);
    const double KS = SS + 273.16;
    printf("华氏温度为：%.2lf\n摄氏温度为：%.2lf\n开式温度为：%.2lf\n",HS,SS,KS);
    return 0;
}
```