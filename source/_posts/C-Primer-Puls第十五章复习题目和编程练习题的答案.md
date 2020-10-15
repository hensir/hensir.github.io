---
title: C-Primer-Puls第十五章复习题目和编程练习题的答案
tags:
  - C语言
categories: C Primer Plus
cover: 'https://s1.ax1x.com/2020/04/26/JcBGNQ.png'
abbrlink: fc18d53f
date: 2020-04-08 11:42:00
---

本章内容为《C Primer Plus第六版》第十五章复习题和编程练习题的答案
## 复习题
### 第一题
1. 把下面的十进制转换为二进制：
a.3
b.13
c.59
d.119
<!--more-->

----------

### 第二题
2. 将下面的二进制值转换为十进制、八进制和十六进制的形式：
a.00010101
b.01010101
c.01001100
d.10011101

----------

### 第三题
3. 对下面的表达式求值，假设每个值都为8位：
a.～3
b.3 & 6
c.3 | 6
d.1 | 6
e.3 ^ 6
f.7 >> 1
g.7 << 2

----------

### 第四题
4. 对下面的表达式求值，假设每个值都为8位：
a.～0
b.!0
c.2 & 4
d.2 && 4
e.2 | 4
f.2 || 4
g.5 << 3

----------

### 第五题
5. 因为ASCII码只使用最后7位，所以有时需要用掩码关闭其他位，其相应的二进制掩码是什么？分别用十进制、八进制和十六进制来表示这个掩码。

----------

### 第六题
6. 程序清单15.2中，可以把下面的代码：
        while (bits-- > 0)
        {
            mask |= bitval;
            bitval <<= 1;
        }
替换成：
        while (bits-- > 0)
        {
            mask += bitval;
            bitval *= 2;
        }
程序照常工作。这是否意味着*=2等同于<<=1？+=是否等同于|=？

----------

### 第七题
7. a.Tinkerbell计算机有一个硬件字节可读入程序。该字节包含以下信息：
|位|含义|
|:-|:-|
|0~1|1.4MB软盘驱动器的数量|
|2|未使用|
|3~4|CD-ROM驱动器数量|
|5|未使用|
|6~7|硬盘驱动器的数量|

 Tinkerbell和IBM PC一样，从右往左填充结构位字段。创建一个适合存放这些信息的位字段模板。
 b.Klinkerbell与Tinkerbell类似，但是它从左往右填充结构位字段。请为Klinkerbell创建一个相应的位字段模板。


## 编程练习
### 第一题
1. 编写一个函数，把二进制字符串转换为一个数值。例如，有下面的语句：
char * pbin = "01001001";
那么把pbin作为参数传递给该函数后，它应该返回一个int类型的值25。
``` c
#include <stdio.h>
#include <string.h>
int get_str(char *, int num); // 返回值为成功获取的str数量
int put_str(char *);          // 返回str的int值
int main(void)
{
    char str[100] = {0};
    while (get_str(str, 100) != 0)
        printf("%d\n", put_str(str));
    return 0;
}
int get_str(char *pt, int num)
{
    char ch;
    int i = 0;
    while ((ch = getchar()) != '\n' && (i != num))
    {
        if (isdigit(ch))
        {
            if (ch == '0' || ch == '1')
            {
                *pt = ch;
                pt++;
            }
            else
                return 0; // 只要有一个不是1或0就给他炸
        }
        else
            return 0;
        i++;
    }
    *pt = '\0';
    return i;
}
int put_str(char *pt)
{
    int value = 0;
    for (int i = 0; pt[i]; i++)
    {
        value <<= 1;
        value |= (pt[i] - '0');
    }
    return value;
}
```
----------

### 第二题
2. 编写一个程序，通过命令行参数读取两个二进制字符串，对这两个二进制数使用～运算符、&运算符、|运算符和^运算符，并以二进制字符串形式打印结果（如果无法使用命令行环境，可以通过交互式让程序读取字符 串）。
``` c
#include <stdio.h>
#include <limits.h>
#include <stdbool.h>    // bool
#include <stdlib.h>     //exit()
int str_int(char *pt);  // string To int
bool inspect(char *pt); // 检测传回来的字符串 有一个不是0或1就给他炸
void binstr(int);       // 数值转二进制字符串
int main(int argc, char *argv[])
{
    int a, b;
    if ((inspect(argv[1])) && (inspect(argv[2])))
    {
        a = str_int(argv[1]);
        b = str_int(argv[2]);
    }
    printf("a     = ");
    puts(argv[1]);
    printf("b     = ");
    puts(argv[2]);
    printf("~a    = ");
    binstr(~a);
    printf("~b    = ");
    binstr(~b);
    printf("a | b = ");
    binstr(a | b);
    printf("a ^ b = ");
    binstr(a ^ b);
    return 0;
}
void binstr(int value) // 统一32位
{
    char bs[32] = {0};
    for (int i = 0; i < 32; i++)
    {
        bs[i] = (01 & value) + '0';
        value >>= 1;
    }
    for (int i = 32 - 1; i >= 0; i--)
        printf("%c", bs[i]);
    putchar('\n');
}
char *itobs(int n, char *ps)
{
    int i;
    const static int size = CHAR_BIT * sizeof(int);
    for (i = size - 1; i >= 0; i--, n >>= 1)
        ps[i] = (01 & n) + '0';
    ps[size] = '\0';
    return ps;
}
int str_int(char *pt)
{
    int value = 0;
    for (int i = 0; pt[i]; i++)
    {
        value <<= 1;
        value |= (pt[i] - '0');
    }
    return value;
}
bool inspect(char *pt)
{
    for (int i = 0; pt[i] != '\0'; i++)
    {
        if ((pt[i] != '0') && (pt[i] != '1'))
        {
            printf("1");
            exit(1);
        }
    }
    return 1;
}
```
----------

### 第三题
3. 编写一个函数，接受一个 int 类型的参数，并返回该参数中打开位的数量。在一个程序中测试该函数。
``` c
#include <stdio.h>
int opi(int);
int main(void) // 转成binstr 然后如果 这个pt[i]为1就是打开
{
    printf("%d", opi(9457));
    return 0;
}
int opi(int value)
{
    int count = 0;
    while (value)
    {
        count += (value & 1);
        value >>= 1;
    }
    return count;
}
```
----------

### 第四题
4. 编写一个程序，接受两个int类型的参数：一个是值；一个是位的位置。如果指定位的位置为1，该函数返回1；否则返回0。在一个程序中测试 该函数。
``` c
#include <stdio.h>
int istrue(int, int);
#define size 32
int main(void)
{
    printf("%d\n", istrue(5, 4));
    printf("%s\n", ist(5, 4) ? "打开" : "关闭");
    return 0;
}
int ist(int value, int n)
{
    return (value & (1 << (n - 1)));
}
int istrue(int value, int pos)
{
    char b[size + 1] = {0};
    for (int i = 0; i < 32; i++)
    {
        b[i] = (01 & value) + '0';
        value >>= 1;
    }
    b[size] = '\0';
    puts(b);
    if (pos < size && b[pos - 1] == '1')
        return 1;
    return 0;
}
```
----------

### 第五题
5. 编写一个函数，把一个 unsigned int 类型值中的所有位向左旋转指定数量的位。例如，rotate_l(x, 4)把x中所有位向左移动4个位置，而且从最左端移出的位会重新出现在右端。也就是说，把高阶位移出的位放入低阶位。在一个程序中测试该函数。
``` c
#include <stdio.h>
#include <limits.h>
unsigned int rotate_l(unsigned int, int);   // 让我写的话 还是int > binstr >int
void print_bstr(unsigned int num);
int main(void)
{
    rotate_l(15, 34);
    return 0;
}
unsigned int rotate_l(unsigned int num, int loop) // 第二十七的d是满32位的 所有>>31后会留一个1 然后是 28，29，30 留一
{                                                 // 换句话 这四个b=1 都是上一个d满32位所得的结果 所以从31开始就结束了
    int a = 0, b = 0, c = 0, d = 0, e = 0, f = 0;
    for (int i = 0; i < loop; i++)
    {
        a = (CHAR_BIT * sizeof(unsigned int) - 1);
        b = num >> a;
        c = num << 1;
        d = b | c;
        num = d;
        printf("%2d a = 31, b = %d ", i, b);
        printf("c = ");
        print_bstr(c);
        printf("d = ");
        print_bstr(d);
        putchar('\n');
        // num = (num >> (CHAR_BIT * sizeof(unsigned int) - 1)) | (num << 1);
    }
    return num;
}
//  24 a = 31, b = 0 c = 1 1110 0000 0000 0000 0000 0000 0000     d = 1 1110 0000 0000 0000 0000 0000 0000
//  25 a = 31, b = 0 c = 11 1100 0000 0000 0000 0000 0000 0000    d = 11 1100 0000 0000 0000 0000 0000 0000
//  26 a = 31, b = 0 c = 111 1000 0000 0000 0000 0000 0000 0000   d = 111 1000 0000 0000 0000 0000 0000 0000
//  27 a = 31, b = 0 c = 1111 0000 0000 0000 0000 0000 0000 0000  d = 1111 0000 0000 0000 0000 0000 0000 0000
//  28 a = 31, b = 1 c = 1110 0000 0000 0000 0000 0000 0000 0000  d = 1110 0000 0000 0000 0000 0000 0000 0001
//  29 a = 31, b = 1 c = 1100 0000 0000 0000 0000 0000 0000 0010  d = 1100 0000 0000 0000 0000 0000 0000 0011
//  30 a = 31, b = 1 c = 1000 0000 0000 0000 0000 0000 0000 0110  d = 1000 0000 0000 0000 0000 0000 0000 0111
//  31 a = 31, b = 1 c = 1110                                     d = 1111
//  32 a = 31, b = 0 c = 1 1110                                   d = 1 1110
//  33 a = 31, b = 0 c = 11 1100                                  d = 11 1100
//  34 a = 31, b = 0 c = 111 1000                                 d = 111 1000
void print_bstr(unsigned int num)
{
    static int n = 0;
    if (!num && !n)
        return;
    if (num)
    {
        n++;
        print_bstr(num >> 1);
    }
    else
        return;
    putchar('0' + (num & 1));
    if ((--n % 4) == 0)
        putchar(' ');
}
```
----------

### 第六题
6. 设计一个位字段结构以储存下面的信息。
字体ID：0～255之间的一个数；
字体大小：0～127之间的一个数；
对齐：0～2之间的一个数，表示左对齐、居中、右对齐；
加粗：开（1）或闭（0）；
斜体：开（1）或闭（0）；
在一个程序中使用该结构来打印字体参数，并使用循环菜单来让用户改变参数。例如，该程序的一个运行示例如下：

 该程序要使用按位与运算符（&）和合适的掩码来把字体ID和字体大小信息转换到指定的范围内。
``` c
#include <stdio.h>
#include <string.h>
#include <stdbool.h>
#include <stdlib.h>
#define LEFT 0
#define RIGHT 1
#define CENTER 2
const char *ALM[3] = {"LEFT", "CENTER", "RIGHT"};
typedef struct
{
    unsigned int id : 8; // 字体ID           //
    unsigned size : 7;   // 字体大小         // 这两个要用掩码
    unsigned int : 1;    // 比特对齐
    unsigned alm : 2;    // 字体左中右对齐
    bool bold : 1;       // 粗体
    bool italics : 1;    // 斜体
    bool ul : 1;         // 下划线
    unsigned int : 3;    // 比特对齐
} font;
void menu(font *); // 菜单和六函
void change_font(font *);
void change_size(font *);
void change_alig(font *);
void toggle_bold(font *);
void toggle_ital(font *);
void toggle_unde(font *);
typedef void (*VF_font)(font *);                                                                               // 函数指针
const VF_font fun_p[7] = {change_font, change_size, change_alig, toggle_bold, toggle_ital, toggle_unde, menu}; // 函数数组
#define ID_MASK 0xFF                                                                                           //ID掩码
#define SIZE_MASK 0x7F                                                                                         //大小掩码
const char *funorder = {"fsabium"};
int main(void)
{
    font text = {1, 17, LEFT, true, false, false};
    char op, *p;
    menu(&text);                                        // 感觉tolower会降低逼格 所以不加了
    while ((op = getchar()) && (p = strchr(funorder, op)))
    {
        fun_p[p - funorder](&text); // 等下看下官方例题的掩码有没有报警告
        fflush(stdin);
        system("CLS");
        menu(&text);
    }
    printf("Bye!");
    return 0;
}
void menu(font *p)
{
    extern const char *ALM[];
    printf(" ID SIZE ALIGNMENT    B    I    U\n");
    printf("%3d %4d  %5s", p->id, p->size, ALM[p->alm]);
    printf("      %3s  %3s  %3s\n", p->bold == true ? "on" : "off", p->italics == true ? "on" : "off", p->ul == true ? "on" : "off");
    printf("f)change font    s)change size    a)change alignment\n");
    printf("b)toggle bold    i)toggle italic  u)toggle underline\nq)quit\n");
}
void change_font(font *p)
{
    p->id &= ~ID_MASK;
    int ID = 0;
    do
    {
        printf("请输入0-255之间的数值");
        fflush(stdin);
    } while (!(scanf("%d", &ID)) || !(ID >= 0) || !(ID <= 255));
    p->id |= ID;
}
void change_size(font *p)
{
    p->size &= ~SIZE_MASK; // 虽然这样写比较水 但这里能用就行 下面unsignd int 才是硬菜
    int SIZE = 0;
    do
    {
        printf("请输入0-127之间的数值");
        fflush(stdin);
    } while (!(scanf("%d", &SIZE)) || !(SIZE >= 0) || !(SIZE <= 127));
    p->size |= SIZE;
}
void change_alig(font *p)
{
    printf("l)left    c)center    r)right\n");
    char *almorder = {"lcr"}, *pt = NULL, ALM;
    while (!(scanf("%c", &ALM)) || !(pt = strchr(almorder, ALM)))
    {
        printf("请输入l,c,r三者其中的数值");
        fflush(stdin);
    }
    p->alm = pt - almorder;
}
void toggle_bold(font *p)
{
    p->bold ^= 1;
}
void toggle_ital(font *p)
{
    p->italics ^= 1;
}
void toggle_unde(font *p)
{
    p->ul ^= 1;
}
```
----------

### 第七题
7. 编写一个与编程练习 6 功能相同的程序，使用 unsigned long 类型的变量储存字体信息，并且使用按位运算符而不是位成员来管理这些信息。
``` c
#include <stdio.h>
#include <stdbool.h>
#include <string.h>
#include <stdlib.h>
#define ID_MASK 0xFF // 掩码
#define SIZE_MASK 0x7F00
#define alig_MASK 0x18000
#define bold_MASK 0x20000
#define ital_MASK 0x40000
#define unde_MASK 0x80000
void menu(unsigned int); // 菜单和六函
void change_font(unsigned int *);
void change_size(unsigned int *);
void change_alig(unsigned int *);
void toggle_bold(unsigned int *);
void toggle_ital(unsigned int *);
void toggle_unde(unsigned int *);
typedef void (*VF_font)(unsigned int *);
const VF_font fun_p[6] = {change_font, change_size, change_alig, toggle_bold, toggle_ital, toggle_unde};
const char *funorder = {"fsabiu"};
const char *ALM[3] = {"LEFT", "CENTER", "RIGHT"};
int main(void)
{
    unsigned int font = 985684; // 84 10 center t t t
    char op, *p;
    menu(font);
    while ((op = getchar()) && (p = strchr(funorder, op)))
    {
        fun_p[p - funorder](&font);
        system("clear");
        menu(font);
        fflush(stdin);  // linux这边这个函数有点小问题啊
        while (getchar() != '\n') ;
    }
    printf("Bye!");
    return 0;
}
void menu(unsigned int font)
{
    printf(" ID SIZE ALIGNMENT    B    I    U\n");
    printf("%3d %4d  %5s", font & ID_MASK, ((font & SIZE_MASK) >> 8), ALM[((font & alig_MASK) >> 15) - 1]);
    printf("     %3s  %3s  %3s\n", ((font & bold_MASK) == bold_MASK) == true ? "on" : "off", ((font & ital_MASK) == ital_MASK) == true ? "on" : "off", ((font & unde_MASK) == unde_MASK) == true ? "on" : "off");
    printf("f)change font    s)change size    a)change alignment\n");
    printf("b)toggle bold    i)toggle italic  u)toggle underline\nq)quit\n");
}
void change_font(unsigned int *p)
{
    *p &= ~ID_MASK; // 清除原先数据  没什么好讲的走的都是一个模子
    int ID = 0;
    do
    {
        printf("请输入0-255之间的数值");
        fflush(stdin);
    } while (!(scanf("%d", &ID)) || !(ID >= 0) || !(ID <= 255));
    *p |= ID;
}
void change_size(unsigned int *p)
{
    *p &= ~SIZE_MASK;
    int SIZE = 0;
    do
    {
        printf("请输入0-127之间的数值");
        fflush(stdin);
    } while (!(scanf("%d", &SIZE)) || !(SIZE >= 0) || !(SIZE <= 127));
    *p |= (SIZE << 8);
}
void change_alig(unsigned int *p)
{
    *p &= ~alig_MASK;
    printf("l)left    c)center    r)right\n");
    char *almorder = {"lcr"}, *pt = NULL, ALM;
    while (!(scanf("%c", &ALM)) || !(pt = strchr(almorder, ALM)))
    {
        printf("请输入l,c,r三者其中的数值");
        fflush(stdin);
    }
    *p |= (pt - almorder + 1) << 15;
}
void toggle_bold(unsigned int *p)
{
    *p ^= bold_MASK;
}
void toggle_ital(unsigned int *p)
{
    *p ^= ital_MASK;
}
void toggle_unde(unsigned int *p)
{
    *p ^= unde_MASK;
}
```