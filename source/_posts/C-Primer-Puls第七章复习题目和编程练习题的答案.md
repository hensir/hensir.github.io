---
title: C-Primer-Puls第七章复习题目和编程练习题的答案
date: 2019-05-19 20:07:00
tags: [答案,题目]
categories: C语言
cover: https://s1.ax1x.com/2020/04/26/JcBGNQ.png
---

本章内容为《C Primer Plus第六版》第七章复习题目和编程练习题的答案

## 复习题

### 第一题
1. 判断下列表达式是true还是false。
a 100 > 3 && 'a'>'c'
b 100 > 3 || 'a'>'c'
c !(100>3)

<!--more-->

----------

### 第二题
2. 根据下列描述的条件，分别构造一个表达式：
a umber等于或大于90，但是小于100
b h不是字符q或k
c umber在1～9之间（包括1和9），但不是5
d umber不在1～9之间

----------

### 第三题
3. 下面的程序关系表达式过于复杂，而且还有些错误，请简化并改正。
``` c
#include <stdio.h>
int main(void)
{
    int weight, height;
    scanf("%d , weight, height);
    if (weight < 100 && height > 64)
    if (height >= 72)
    printf("You are very tall for your weight.\n");
    else if (height < 72 &&> 64)
    printf("You are tall for your weight.\n");
    else if (weight > 300 && !(weight <= 300)&& height < 48)
    if (!(height >= 48))
    printf(" You are quite short for your weight.\n");
    else
    printf("Your weight is ideal.\n");
    return 0;
}
```

----------

### 第四题
4. 下列个表达式的值是多少？
        a.5 > 2
        b.3 + 4 > 2 && 3 < 2
        c.x >= y || y > x
        d.d = 5 + ( 6 > 2 )
        e.'X' > 'T' ? 10 : 5
        f.x > y ? y > x : x > y

----------

### 第五题
5. 下面的程序将打印什么？
``` c
#include <stdio.h>
int main(void)
{
    int num;
    for (num = 1; num <= 11; num++)
    {
        if (num % 3 == 0)
            putchar('$');
        else
            putchar('*');
        putchar('#');
        putchar('%');
    }
    putchar('\n');
    return 0;
}
```

----------


### 第六题
6. 下面的程序将打印什么？
```c
#include <stdio.h>
int main(void)
{
    int i = 0;
    while (i < 3)
    {
        switch (i++)
        {
        case 0:
            printf("fat ");
        case 1:
            printf("hat ");
        case 2:
            printf("cat ");
        default:
            printf("Oh no!");
        }
        putchar('\n');
    }
    return 0;
}
```

----------

### 第七题
7. 下面的程序有哪些错误？
``` c
#include <stdio.h>
int main(void)
{
    char ch;
    int lc = 0;
    int uc = 0;
    int oc = 0;
    while ((ch = getchar()) != '#')
    {
        if ('a' <= ch >= 'z')
            lc++;
        else if (!(ch < 'A') || !(ch > 'Z')
            uc++;
            oc++;
    }
    printf(%d lowercase, %d uppercase, %d other, lc, uc, oc);
    return 0;
}
```

----------

### 第八题
8. 下面的程序将打印什么？
``` c
#include <stdio.h>
int main(void)
{
    int age = 20;
    while (age++ <= 65)
    {
        if ((age % 20) == 0) /* age是否能被20整除？ */
            printf("You are %d.Here is a raise.\n", age);
        if (age = 65)
            printf("You are %d.Here is your gold watch.\n", age);
    }
    return 0;
}
```

----------


### 第九题
9. 给定下面的输入时，以下程序将打印什么？
q c h b
``` c
#include <stdio.h>
int main(void)
{
    char ch;
    while ((ch = getchar()) != '#')
    {
        if (ch == '\n')
            continue;
        printf("Step 1\n");
        if (ch == 'c')
            continue;
        else if (ch == 'b')
            break;
        else if (ch == 'h')
            goto laststep;
        printf("Step 2\n");
    laststep:
        printf("Step 3\n");
    }
    printf("Done\n");
    return 0;
}
```

----------

### 第十题
10. 重写复习题9，但这次不能使用continue和goto语句。

----------


## 编程练习

### 第一题
1. 编写一个程序读取输入，读到#字符停止，然后报告读取的空格数、换行符数和所有其他字符的数量。
``` c
#include <stdio.h>
int main(void)
{
    char ch;
    int word = 0，space = 0, LF = 1;
    while ((ch = getchar()) != '#')
    {
        word += 1;
        if (ch == ' ')
            space += 1;
        else if (ch == '\n')
            LF += 1;
    }
    printf("这段字符串中有%d个空格，%d个换行符，总共%d个字符", space, LF, word);
    return 0;
}
```

----------



### 第二题
2. 编写一个程序读取输入，读到#字符停止。程序要打印每个输入的字符以及对应的ASCII码（十进制）。
一行打印8个字符。建议 : 使用字符计数 和求模运算符（%）在每8个循环周期时打印一个换行符。
``` c
#include <stdio.h>
int main(void)
{
    char c;
    int i = 0;
    while ((c = getchar()) != '#')
    {
        if (c == '\n')
        {
            i = 0;
            continue;
        }
        printf("%c-%d ", c, c);
        i++;
        if (i % 8 == 0)
            printf("\n");
    }
    return 0;
}
```

----------



### 第三题
3. 编写一个程序，读取整数直到用户输入0。
输入结束后，程序应报告 用户输入的偶数（不包括 0）个数、这些偶数的平均值、输入的奇数个数及其奇数的平均值。
``` c
#include <stdio.h>
int main(void)
{
    int num = 0;      //接收指定值
    int n_even = 0;   //偶数的个数
    int even_num = 0; //偶数的总和
    int n_odd = 0;    //奇数的个数
    int odd_num = 0;  //奇数的总和
    while (scanf("%d", &num), num != 0)
    {
        if (num == '\n')
            continue;
        if (num % 2 == 0)
        {
            n_even++;
            even_num += num;
        }
        else
        {
            n_odd++;
            odd_num += num;
        }
    }
    //如果没有奇/偶数及数值 那就另作提示
    if (n_even != 0)
        printf("偶数有%3d个 偶数的平均数为%3d\n", n_even, even_num / n_even);
    else
        printf("没有偶数\n");
    if (n_odd != 0)
        printf("奇数有%3d个 奇数的平均数为%3d\n", n_odd, odd_num / n_odd);
    else
        printf("没有奇数\n");
    return 0;
}
```

----------


### 第四题
4. 使用if else语句编写一个程序读取输入，读到#停止。
用感叹号替换句号，用两个感叹号替换原来的感叹号，最后报告进行了多少次替换。
``` c
#include <stdio.h>
int main(void)
{
    char ch;
    int once = 0;
    while ((ch = getchar()) != '#')
    {
        if (ch == '.')
        {
            putchar('!');
            once++;
        }
        else if (ch == '!')
        {
            putchar('!');
            putchar('!');
            once++;
        }
        putchar(ch);
    }
    printf("替换了%d次", once);
    return 0;
}
```

----------


### 第五题
5. 使用switch重写练习4。
``` c
#include <stdio.h>
int main(void)
{
    char ch;
    int one = 0, two = 0;
    while ((ch = getchar()) != '#')
    {
        switch (ch)
        {
        case '.':
        {
            putchar('!');
            one++;
            break;
        }
        case '!':
        {
            putchar('!');
            putchar('!');
            two++;
            break;
        }
        default:
            putchar(ch);
        }
    }
    int once = one + two;
    printf("总共替换了%d次\n", once);
    printf("其中 . 符号替换了%d次 ！ 符号替换了%d次\n", one, two);
    return 0;
}
```

----------


### 第六题
6. 编写程序读取输入，读到#停止，报告ei出现的次数。
注意该程序要记录前一个字符和当前字符。用“Receive your eieio award”这样的输入来测试
``` c
#include <stdio.h>
int main(void)
{
    char ch;
    int fre = 0;
    while ((ch = getchar()) != '#')
    {
        if (ch == 'e' && getchar() == 'i')
            fre++;
    }
    printf("%d", fre);
    return 0;
}
```

----------




### 第七题
7. 编写一个程序，提示用户输入一周工作的小时数，然后打印工资总额、税金和净收入。做如下假设：
a.基本工资 = 10.00美元/小时
b.加班（超过40小时） = 1.5倍的时间
c.税率： 前300美元为15% 续150美元为20%
余下的为25%
用#define定义符号常量。不用在意是否符合当前的税法。
``` c
#include <stdio.h>
#define m_hour 10
#define t_over 40
#define h_over 1.5
#define m_fourty (m_hour * t_over)
#define tr_m1 300                                       //第一个分界点
#define tr_m2 450                                       //第二个分界点
#define trf 0.15                                        //前300美元的费率
#define trs 0.20                                        //续150美元的费率
#define trt 0.25                                        //余下的美元费率
#define f_taxation (tr_m1 * trf)                        //300美元的税费
#define s_taxation (f_taxation + trs * (tr_m2 - tr_m1)) //450美元的税费
double taxation(double);
int main(void)
{
    double hour, m_all;               //工作时间和工资总额  一周168小时
    printf("一周工作的小时数 = ");
    scanf("%lf", &hour);
    if (hour > 40)
        m_all = m_fourty + m_hour * (h_over * (hour - t_over));
    else
        m_all = hour * m_hour;
    printf("工资总额 = %5.2lf\n税金     = %5.2lf\n净收入   = %5.2lf\n", m_all, taxation(m_all), m_all - taxation(m_all));
    return 0;
}
double taxation(double m_all)
{
    double ta;     //税金
    if(m_all <= tr_m1)      //300美元以内的税费
    ta = m_all * trf;
    else if (m_all > tr_m1) //450美元以内的税费
    ta = f_taxation + trs * (m_all - tr_m1);
    else if (m_all > tr_m2) //超过450美元的税费
    ta = s_taxation + trt * (m_all - tr_m2);
    return ta;
}
```
----------


### 第八题
8. 修改练习7的假设a，让程序可以给出一个供选择的工资等级菜单。使用switch完成工资等级选择。运行程序后，显示的菜单应该类似这样：
        *****************************************************************
        Enter the number corresponding to the desired pay rate or action:
        1) $8.75/hr     2) $9.33/hr
        2) $10.00/hr    4) $11.20/hr
        5) quit
        *****************************************************************
如果选择 1～4 其中的一个数字，程序应该询问用户工作的小时数。程序要通过循环运行，除非用户输入 5。如果输入 1～5 以外的数字，程序应 提醒用户输入正确的选项，然后再重复显示菜单提示用户输入。使用#define 创建符号常量表示各工资等级和税率。
``` c
#include <stdio.h>
#define t_over 40
#define h_over 1.5
#define tr_m1 300                                       //第一个分界点
#define tr_m2 450                                       //第二个分界点
#define trf 0.15                                        //前300美元的费率
#define trs 0.20                                        //续150美元的费率
#define trt 0.25                                        //余下的美元费率
#define f_taxation (tr_m1 * trf)                        //300美元的税费
#define s_taxation (f_taxation + trs * (tr_m2 - tr_m1)) //450美元的税费
double taxation(double);
double M_all(double);
double mof(int);
void menu(void);
int main(void)
{
    double m_all, m_hour;
    int target;
    menu();
    while ((target = getchar()) != '5')
    {
        if (target == '\n')
            continue;
        switch (target)
        {
        case '1':
            m_hour = 8.75;
            break;
        case '2':
            m_hour = 9.33;
            break;
        case '3':
            m_hour = 10.00;
            break;
        case '4':
            m_hour = 11.20;
            break;
        default:
            printf("请输入1-5之间的数字");
            menu();
            break;
        }
        while (getchar() != '\n')
            continue;
        m_all = M_all(m_hour);
        printf("工资总额 = %5.2lf\n税金     = %5.2lf\n净收入   = %5.2lf\n", m_all, taxation(m_all), m_all - taxation(m_all));
        menu();
    }
    return 0;
}
void menu(void)
{
    printf("\n*****************************************************************\n");
    printf("Enter the number corresponding to the desired pay rate or action:\n1) $8.75/hr     2) $9.33/hr\n3) $10.00/hr    4) $11.20/hr\n5) quit\n");
    printf("*****************************************************************\n");
}
double M_all(double m_hour) //计算工资总额
{
    double hour;
    printf("请输入工作小时数");
    scanf("%lf", &hour);
    double m_all, m_fourty;
    m_fourty = (m_hour * t_over);
    if (hour > t_over)
        m_all = m_fourty + m_hour * (h_over * (hour - t_over));
    else
        m_all = hour * m_hour;
    return m_all;
}
double taxation(double m_all) //计算税费
{
    double ta;          //税金
    if (m_all <= tr_m1) //300美元以内的税费
        ta = m_all * trf;
    else if (m_all > tr_m1) //450美元以内的税费
        ta = f_taxation + trs * (m_all - tr_m1);
    else if (m_all > tr_m2) //超过450美元的税费
        ta = s_taxation + trt * (m_all - tr_m2);
    return ta;
}
```
----------


### 第九题
9. 编写一个程序，只接受正整数输入，然后显示所有小于或等于该数的素数。
``` c
#include <stdio.h>
int main(void)
{
    int num, i, j, result, a;
    scanf("%d", &num);
    for (i = 1; i <= num; i++)
    {
        for (j = 2; j < i; j++)
        {
            if (i % j == 0)
            {
                a = 0;
                break;
            }
            else
            {
                a = 1;
            }
        }
        if (a == 1)
            printf("%d  ", i);
    }
    return 0;
}
```
----------


### 第十题
10. 1988年的美国联邦税收计划是近代最简单的税收方案。它分为4个类别，每个类别有两个等级。
下面是该税收计划的摘要（美元数为应征税的收入）：
|类别|税金|
|单身|17850美元按15%计，超出部分按28%计|
|户主|23900美元按15%计，超出部分按28%计|
|已婚，共有|29750美元按15%计，超出部分按28%计|
|已婚，离异|14875美元按15%计，超出部分按28%计|
例如，一位工资为20000美元的单身纳税人，应缴纳税费0.15×17850+0.28×（20000−17850）美元。编写一个程序，让用户指定缴纳税金的种类和应纳税收入，然后计算税金。程序应通过循环让用户可以多次输入。
``` c
#include <stdio.h>
#define SINTRT 17850          //单身的税费阈值
#define SINTRM (SINTRT * TRO) //单身的一级税费
#define HOHTRT 23900          //户主的税费阈值
#define HOHTRM (HOHTRT * TRO) //户主的一级税费
#define MARTRT 29750          //已婚的税费阈值
#define MARTRM (MARTRT * TRO) //已婚的一级税费
#define DIVTRT 14875          //离异的税费阈值
#define DIVTRM (DIVTRT * TRO) //离异的一级税费
#define TRO 0.15              //一级税率
#define TRT 0.28              //二级税率
void result(double, double, double);
void banner(void);
int main(void)
{
    char ch;
    double T_target, M_target;
    banner();
    while ((ch = getchar()) != '5')
    {
        switch (ch)
        {
        case '1':
            T_target = SINTRT;
            M_target = SINTRM;
            result(T_target, M_target, 1);
            break;
        case '2':
            T_target = HOHTRT;
            M_target = HOHTRM;
            result(T_target, M_target, 2);
            break;
        case '3':
            T_target = MARTRT;
            M_target = MARTRM;
            result(T_target, M_target, 3);
            break;
        case '4':
            T_target = DIVTRT;
            M_target = DIVTRM;
            result(T_target, M_target, 4);
            break;
        default:
            printf("请重新输入");
            break;
        }
        banner();
        while (getchar() != '\n')
            continue;
    }
    return 0;
}
void result(double T_target, double M_target, double tip)
{
    double DR = 0, result;
    printf("类别：%.lf\n请输入美元(输入q以退出到种类选择)\n", tip);
    while ((scanf("%lf", &DR)) == 1)
    {
        if (DR <= T_target)
            result = DR * TRO;
        else
            result = M_target + (DR - T_target) * TRT;
        printf("%.2lf美元的税费\n", result);
        printf("类别：%.lf\n请输入美元(输入q以退出到种类选择)\n", tip);
        while (getchar() != '\n')
            continue;
    }
}
void banner(void)
{
    printf("************************************************************\n"
           "请输入一个对应的字符以使程序进入下一步\n"
           "1)单身        2)户主\n3)已婚，共有  4)已婚，离异\n5)退出\n"
           "************************************************************\n");
}
```
----------


### 第十一题
11.  ABC 邮购杂货店出售的洋蓟售价为 2.05 美元/磅，甜菜售价为 1.15美元/磅，胡萝卜售价为 1.09美元/磅。在添加运费之前，100美元的订单有 5%的打折优惠。少于或等于5磅的订单收取6.5美元的运费和包装费，5磅～ 20磅的订单收取14美元的运费和包装费，超过20磅的订单在14美元的基础上 每续重1磅增加0.5美元。编写一个程序，在循环中用switch语句实现用户输入不同的字母时有不同的响应，即输入a的响应是让用户输入洋蓟的磅数，b 是甜菜的磅数，c是胡萝卜的磅数，q 是退出订购。程序要记录累计的重量。即，如果用户输入 4 磅的甜菜，然后输入 5磅的甜菜，程序应报告9磅的甜菜。然后，该程序要计算货物总价、折扣（如果有的话）、运费和包装费。随后，程序应显示所有的购买信息：物品售价、订购的重量（单位：磅）、订购的蔬菜费用、订单的总费用、折扣（如果有的话）、运费和包装费，以及所有的费用总额。
``` c
#include <stdio.h>
#define YJM 2.05        //洋蓟价格
#define TCM 1.15        //甜菜价格
#define HLBM 1.09       //胡萝卜价格
#define DCS 0.05        //打折优惠
#define PA 5            //一级磅数阈值
#define PB 20           //二级磅数阈值
#define PAM 6.5         //一级磅数单价
#define PBM 14          //二级磅数单价
#define OFPA PA *PAM    //一级磅数总价
#define OFPB PB *PBM    //二级磅数总价
#define OFP 0.5         //超过20磅每磅续加0.5美元
void menu(void);        //菜单
double add(char);       //统计所需蔬菜磅数
double freight(double); //包装费和运费
int main(void)
{
    char target;        //进入switch
    double yj, tc, hlb; //洋蓟， 甜菜， 胡萝卜
    int dft = 1;        //防止用户输入其他值程序报出总蔬菜磅数
    menu();
    while ((target = getchar()) != 'q')
    {
        switch (target)
        {
        case 'a':
            dft = 1;
            yj += add('a');
            break;
        case 'b':
            dft = 1;
            tc += add('b');
            break;
        case 'c':
            dft = 1;
            hlb += add('c');
            break;
        default:
            dft = 0;
            printf("请重新输入\n");
            break;
        }
        menu();
        while (getchar() != '\n')
            continue;
        if (dft)
            printf("%5.2lf磅洋蓟 = %5.2lf美元\n%5.2lf磅甜菜 = %5.2lf美元\n%5.2lf磅胡萝卜 = %5.2lf美元\n", yj, yj * YJM, tc, tc * TCM, hlb, hlb * HLBM);
    }
    double Tp = (yj * YJM) + (tc * TCM) + (hlb * HLBM); //蔬菜总费用
    double Tpk = 0;                                     //折扣数
    if (Tp > 100)
        Tpk = Tp * DCS;
    double Pound = yj + tc + hlb;   //总磅数
    double PoundM = freight(Pound); //包装费和运费
    double aof = Tp + PoundM - Tpk; //所有的加在一起
    if (Tpk)
        printf("蔬菜总磅数 = %.2lf磅\n蔬菜总费用 = %.2lf美元\n折扣 = %.2lf美元\n运费和包装费 = %.2lf美元\n所有的费用 = %.2lf美元\n", Pound, Tp, Tpk, PoundM, aof);
    else
        printf("蔬菜总磅数 = %.2lf磅\n蔬菜总费用 = %.2lf美元\n运费和包装费 = %.2lf美元\n所有的费用 = %.2lf美元\n", Pound, Tp, PoundM, aof);
    return 0;
}
double freight(double Pound)
{
    double Ft;
    if (Pound <= PA)
        Ft = PAM;
    else if (Pound > PA && Pound < PB)
        Ft = PBM;
    else if (Pound > PB)
        Ft = PBM + (Pound - PB) * OFP;
    return Ft;
}
double add(char tip)
{
    double bang, _bang;
    printf("类别：%c\n请输入磅数(输入q以退出到选择菜单)\n", tip);
    while (scanf("%lf", &bang) == 1)
    {
        _bang += bang;
        printf("类别：%c，当前磅数为 %.2lf\n", tip, _bang);
        printf("请输入磅数(输入q以退出到选择菜单)\n", tip);
        while (getchar() != '\n')
            continue;
    }
    return _bang;
}
void menu(void)
{
    printf("**************************************************\n*                                                *"
           "\n*  a)   洋蓟 2.05美元/磅    b) 甜菜 1.15美元/磅  *\n*  c) 胡萝卜 1.09美元/磅    q) 退出订购          *\n*                                                *"
           "\n**************************************************\n");
}
```