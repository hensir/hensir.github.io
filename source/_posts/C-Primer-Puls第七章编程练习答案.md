---
title: C-Primer-Puls第七章复习题目和编程练习题的答案
date: 2019-05-19 20:07:00
tags: [答案,题目]
categories: C语言
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
    int word = 0;
    int space = 0;
    int LF = 1;
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
            continue;
        }
        else if (ch == '!')
        {
            putchar('!');
            putchar('!');
            once++;
            continue;
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
    int one = 0;
    int two = 0;
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
    char ar; //ar就是上一个值的载体
    int fre = 0;
    while ((ch = getchar()) != '#')
    {
        if (ch == 'i' && ar == 'e')
            fre++;
        ar = ch; //ar不能被立即（覆）赋值 否则它根本无法保存上一个值
    }
    printf("%d", fre);
    return 0;
}
```

----------




### 第七题

----------


### 第八题

----------


### 第九题

----------


### 第十题

----------


### 第十一题