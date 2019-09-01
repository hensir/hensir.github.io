---
title: C-Primer-Puls第五章复习题目和编程练习题的答案
date: 2019-05-16 15:25:51
tags: [答案,题目]
categories: C语言
---



本章内容为《C Primer Plus第六版》第五章复习题目和编程练习题的答案

## 复习题

### 第一题

1. 假设所有变量的类型都是int，下列各项变量的值是多少：
a.x = (2 + 3) * 6;
b.x = (12 + 6)/2*3;
c.y = x = (2 + 3)/4;
d.y = 3 + 2*(x = 7/2);

<!--more-->

----------

### 第二题

2. 假设所有变量的类型都是int，下列各项变量的值是多少：
a.x = (int)3.8 + 3.3;
b.x = (2 + 3) * 10.5;
c.x = 3 / 5 * 22.0;
d.x = 22.0 * 3 / 5;

----------

### 第三题

3. 对下列各表达式求值：
a.30.0 / 4.0 * 5.0;
b.30.0 / (4.0 * 5.0);
c.30 / 4 * 5;
d.30 * 5 / 4;
e.30 / 4.0 * 5;
f.30 / 4 * 5.0;

----------


### 第四题

4. 请找出下面的程序中的错误。
``` c
int main(void)
{
    int i = 1,
    float n;
    printf("Watch out! Here come a bunch of fractions!\n");
    while (i < 30)
    n = 1/i;
    printf(" %f", n);
    printf("That's all, folks!\n");
    return;
}
```

----------


### 第五题

5. 这是程序清单 5.9 的另一个版本。从表面上看，该程序只使用了一条scanf()语句，比程序清单5.9简单。请找出不如原版之处。
``` c
#include <stdio.h>
#define S_TO_M 60
int main(void)
{
    int sec, min, left;
    printf("This program converts seconds to minutes and ");
    printf("seconds.\n");
    printf("Just enter the number of seconds.\n");
    printf("Enter 0 to end the program.\n");
    while (sec > 0)
    {
        scanf("%d", &sec);
        min = sec / S_TO_M;
        left = sec % S_TO_M;
        printf("%d sec is %d min, %d sec.\n", sec, min, left);
        printf("Next input?\n");
    }
    printf("Bye!\n");
    return 0;
}
```

----------


### 第六题

6. 下面的程序将打印出什么内容？
``` c
#include <stdio.h>
#define FORMAT "%s! C is cool!\n"
int main(void)
{
    int num = 10;
    printf(FORMAT, FORMAT);
    printf("%d\n", ++num);
    printf("%d\n", num++);
    printf("%d\n", num--);
    printf("%d\n", num);
    return 0;
}
```

----------


### 第七题

7. 下面的程序将打印出什么内容？
``` c
#include <stdio.h>
int main(void)
{
    char c1, c2;
    int diff;
    float num;
    c1 = 'S';
    c2 = 'O';
    diff = c1 - c2;
    num = diff;
    printf("%c%c%c:%d %3.2f\n", c1, c2, c1, diff, num);
    return 0;
}
```

----------


### 第八题

8. 下面的程序将打印出什么内容？
``` c
#include <stdio.h>
#define TEN 10
int main(void)
{
    int n = 0;
    while (n++ < TEN)
        printf("%5d", n);
    printf("\n");
    return 0;
}
```

----------


### 第九题

9. 修改上一个程序，使其可以打印字母a～g。
----------


### 第十题

10. 假设下面是完整程序中的一部分，它们分别打印什么？
a. int x = 0; while (++x < 3)printf("%4d", x);
b. int x = 100; while (x++ < 103) printf("%4d\n",x); printf("%4d\n",x);
c. char ch = 's'; while (ch < 'w') { printf("%c", ch); ch++; } printf("%c\n",ch);

----------


### 第十一题

11. 下面的程序会打印出什么？
``` c
#define MESG "COMPUTER BYTES DOG"
#include <stdio.h>
int main(void)
{
    int n = 0;
    while (n < 5)
        printf("%s\n", MESG);
    n++;
    printf("That's all.\n");
    return 0;
}
```

----------


### 第十二题

12. 分别编写一条语句，完成下列各任务（或者说，使其具有以下副作用）：
a.将变量x的值增加10
b.将变量x的值增加1
c.将a与b之和的两倍赋给c
d.将a与b的两倍之和赋给c

----------


### 第十三题

13. 分别编写一条语句，完成下列各任务：
a.将变量x的值减少1
b.将n除以k的余数赋给m
c.q除以b减去a，并将结果赋给p
d.a与b之和除以c与d的乘积，并将结果赋给x

----------


## 编程练习

### 第一题
1. 编写一个程序，把用分钟表示的时间转换成用小时和分钟表示的时间。
使用#define或const创建一个表示60的符号常量或const变量。
通过while 循环让用户重复输入值，直到用户输入小于或等于0的值才停止循环。
``` c
#include <stdio.h>
#define hour 60
int main(void)
{
    int min;
    printf("min = (<= 0 to quit)\n");
    scanf("%d", &min);
    while (min > 0)
    {
        printf("min = %dh%dmin\n", min / hour, min % hour); //%求余运算符
        printf("min = (<= 0 to quit)\n");
        scanf("%d", &min);
    }
    return 0;
}
```

----------



### 第二题
2. 编写一个程序，提示用户输入一个整数，然后打印从该数到比该数大 10的所有整数（例如，用户输入5，则打印5～15的所有整数，包括5和 15）。要求打印的各值之间用一个空格、制表符或换行符分开。
``` c
#include <stdio.h>
int main(void)
{
    int num, bigger;
    printf("number = ");
    scanf("%d", &num);
    bigger = num + 10;
    while (num <= bigger)
    {
        printf("%d  ", num);
        num++;
    }
    return 0;
}
```

----------


### 第三题
3. 编写一个程序，提示用户输入天数，然后将其转换成周数和天数。
例如，用户输入18，则转换成2周4天。
以下面的格式显示结果：18 days are 2 weeks, 4 days.
通过while循环让用户重复输入天数，当用户输入一个非正值时（如0 或 - 20），循环结束。
``` c
#include <stdio.h>
#define week 7
int main(void)
{
    int days;
    printf("天数 = (<= 0 to quit)\n");
    scanf("%d", &days);
    while (days > 0)
    {
	    printf("%d天 = %d周0%d天\n",days, days / week, days % week);
	    printf("天数 = (<= 0 to quit)\n");
	    scanf("%d", &days);
    }
    return 0;
}
```

----------



### 第四题
4. 编写一个程序，提示用户输入一个身高（单位：厘米），并分别以厘米和英寸为单位显示该值，允许有小数部分。
程序应该能让用户重复输入身 高，直到用户输入一个非正值。
其输出示例如下：
	Enter　a　height　in　centimeters : 182
	182.0　cm　 = 5　feet, 11.7　inches
	Enter　a　height　in　centimeters　(<= 0　to　quit) : 168.7
	168.0　cm　 = 5　feet, 6.
    4　inches
	Enter　a　height　in　centimeters　(<= 0　to　quit) : 0
	bye
``` c
#include <stdio.h>  //1英尺 = 12英寸  1厘米 = 0.0328084英尺  1厘米 = 0.393701英寸
int main(void)
{
    double cm, inches;
    int feet;
    printf("height = (cm)(<= 0 to quit)");
    scanf("%lf", &cm);
    while (cm)
    {
        feet = (int)(cm * 0.0328084);
        inches = (cm * 0.3937008) - (feet * 12);
        printf("%.lfcm = %dfeet%.1finches\n", cm, feet, inches);
        printf("height = (cm)(<= 0 to quit)");
        scanf("%lf", &cm);
    }
    printf("Bye!\n");
    return 0;
}
```

----------


### 第五题
5. 修改程序addemup.c（程序清单5.13），你可以认为addemup.c是计算20天里赚多少钱的程序
（假设第1天赚$1、第2天赚$2、第3天赚$3，以此类 推）。
修改程序，使其可以与用户交互，根据用户输入的数进行计算（即，用读入的一个变量来代替20）。
``` c
#include <stdio.h>
int main(void)
{
    int count, sum, days;
    count = 0;
    sum = 0;
    printf("days = ");
    scanf("%d", &days);
    while (count++ < days)
        sum = sum + count;
    printf("sum = %d\n", sum);
    return 0;
}
```

----------



### 第六题
6. 修改编程练习5的程序，使其能计算整数的平方和（可以认为第1天赚 $1、第2天赚$4、第3天赚$9，以此类推，这看起来很不错）。C没有平方函数，但是可以用n * n来表示n的平方。
``` c
#include <stdio.h>
int main(void)
{
    int count, sum, days;
    count = 0;
    sum = 0;
    printf("days = ");
    scanf("%d", &days);
    while (count++ < days)
        sum = (sum + count * count);
    printf("sum = %d\n", sum);
    return 0;
}
```

----------


### 第七题
7. 编写一个程序，提示用户输入一个double类型的数，并打印该数的立方值。
自己设计一个函数计算并打印立方值。main()函数要把用户输入的值传递给该函数。
``` c
#include <stdio.h>
int cube(double num);   //声明函数原型
int main(void)
{
    double num;
    printf("number = ");
    scanf("%lf", &num);
    cube(num);           //函数调用
    return 0;
}
int cube(double num)    //该函数的参数为double型num变量
{
    printf("%f\n", num * num * num);
    return 0;           //读者在做到这题时可以试着让cube函数把结果返回给main函数 再由main函数输出
}                       //当然函数详解在第九章

```

----------


### 第八题
8. 编写一个程序，显示求模运算的结果。
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
int main(void)
{
    int one, two;
    printf("two = ");
    scanf("%d", &two);
    printf("one = ");
    scanf("%d", &one);
    while (one > 0)
    {       //用两个百分号来输出百分号
        printf("%d %% %d = %d\n", one, two, one % two);
        printf("two = (<= 0 to quit)");
        scanf("%d", &one);
    }
    printf("Done\n");
    return 0;
}
```

----------


### 第九题
9. 编写一个程序，要求用户输入一个华氏温度。
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
int Temperatures(double Fahrenheit);        //声明函数原型
int main(void)
{
    double Fahrenheit;
    printf("Fahrenheit = ");                //scanf的返回值与成功读取的项数成正比
    while (scanf("%lf", &Fahrenheit) == 1)  //这句意思为：如果（scanf的返回值 == 1）这个表达式成立 则结果为1；
    {                                       //while为真的具体条件是 紧跟while的关系表达式的结果为 除0以外的所有整数
        Temperatures(Fahrenheit);
        printf("Fahrenheit = ");
    }
    printf("Bye!\n");
    return 0;
}
int Temperatures(double Fahrenheit)
{
    const double Celsius = 5.0 / 9.0 * (Fahrenheit - 32.0);
    const double Kelvin = Celsius + 273.16;
    printf("%.2lf°F = %.2lf℃ = %.2lfK\n",Fahrenheit,Celsius,Kelvin);
    return 0;
}
```