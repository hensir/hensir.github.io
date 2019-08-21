---
title: C-Primer-Puls第六章编程练习答案
date: 2019-05-18 18:44:00
tags: [C语言,答案]
categories: 代码
---



本章内容为《C Primer Plus第六版》第六章编程练习的答案


##  第一题
1.编写一个程序，创建一个包含26个元素的数组，并在其中储存26个小写字母。然后打印数组的所有内容。

``` c
#include <stdio.h>
int main(void)
{
    int index;
    char Letter;
    char array[26];
    for (index = 0,Letter = 'a'; index < 26; index++,Letter++)
    {
        array[index] = Letter;
        printf(" %c", array[index]);
    }
    return 0;
}
```

<!--more-->


##  第二题

2.使用嵌套循环，按下面的格式打印字符：

    $
    $$
    $$$
    $$$$
    $$$$$

---

``` c
#include <stdio.h>
int main(void)
{
    int outer, inner;
    for (int outer = 0; outer < 5; outer++)
    {
        for (int inner = 0; inner <= outer; inner++)
            printf("$");
        printf("\n");
    }
    return 0;
}
```



##  第三题

3.使用嵌套循环，按下面的格式打印字母：

    F
    FE
    FED
    FEDC
    FEDCB
    FEDCBA

注意：如果你的系统不使用ASCII或其他以数字顺序编码的代码，可以 把字符数组初始化为字母表中的字母：
char lets[27] = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
然后用数组下标选择单独的字母，例如lets[0]是‘A’，等等。

``` c
#include <stdio.h>
int main(void)
{
    char outer = 'F';
    char inner = 'F';
    for (outer = 'F'; outer >= 'A'; outer--)
    {
       for (inner = 'F'; inner >= outer; inner--)
            printf("%c", inner);
       printf("\n");
    }
    return 0;
}
```


##  第四题


4.使用嵌套循环，按下面的格式打印字母：
A              65
BC             66
DEF            68
GHIJ           71
KLMNO          75
PQRSTU         80
如果你的系统不使用以数字顺序编码的代码，请参照练习3的方案解决。
数组的值为A到Z 用循环来控制输出哪些元素

``` c
#include <stdio.h>
int main(void)
{
    char index;
    int outer, inner;
    for (index = 'A',outer = 1; outer <= 6; outer++)
    {
        for (inner = 1; inner <= outer;inner++, index++)
            printf("%c", index);
            printf("\n");
    }
    return 0;
}
```


##  第五题

5.编写一个程序，提示用户输入大写字母。使用嵌套循环以下面金字塔 型的格式打印字母：

        Ａ
       ABA
      ABCBA
     ABCDCBA
    ABCDEDCBA

打印这样的图形，要根据用户输入的字母来决定。例如，上面的图形是 在用户输入E后的打印结果。
提示：用外层循环处理行，每行使用3个内层循环，分别处理空格、以升序打印字母、以降序打印字母。
如果系统不使用ASCII或其他以数字顺序 编码的代码，请参照练习3的解决方案。

``` c
#include <stdio.h>
int main(void)
{
    char  word;     //接收指定值
    int   line;     //控制升序打印字母的个数 放在外层中循环递增 意思是控制第一行的升序层打印一个字母 第二层。。。（与目标有些无伤大雅的出入）用断点跑一遍你就明白了
    char space;     //控制打印空格的个数  赋值在外层中 指定值减去'A'就是要打印的空格数量
    int  index;     //在空格和升序中均被用来当作索引
    char    Ao;     //升序
    char    Do;     //降序
    scanf("%c", &word);
    for (line = 0, space = word - 'A'; Ao <= word; Ao++, line++, space--)
    {
        for (index = 0; index < space; index++)                //空格层
            printf(" ");
        for (index = 1, Ao = 'A'; index <= line; index++, Ao++)//升序层  搞明白为什么index要初始化为1 提示：index <= line;和外层line = 0；
            printf("%c", Ao);
        for (Do = Ao; Do >= 'A'; Do--)                         //降序层  Do取升序Ao的值 然后递减输出到A
            printf("%c", Do);
        printf("\n");
    }
    return 0;
}
```



##  第六题

6.编写一个程序打印一个表格，每一行打印一个整数、该数的平方、该数的立方。
要求用户输入表格的上下限。使用一个for循环。

``` c
#include <stdio.h>
int main(void)
{
    int Begin, End;
    printf("Begin = ");
    scanf("%d", &Begin);
    printf("End = ");
    scanf("%d", &End);
    for (; Begin <= End; Begin++)
        printf("The square and cube of %5d is %5d and %5d\n", Begin, Begin * Begin, Begin * Begin * Begin);
    return 0;
}
```


##  第七题

7.编写一个程序把一个单词读入一个字符数组中，然后倒序打印这个单 词。
提示：strlen()函数（第4章介绍过）可用于计算数组最后一个字符的下标。

``` c
#include <stdio.h>
#include <string.h>
int main(void)
{
    char word[100];
    scanf("%s", word);
    int size = strlen(word) - 1;    //stren函数从1开始计数,所以要减1
    for (; size >= 0; size--)
        printf("%c", word[size]);
    return 0;
}
```



##  第八题

8.编写一个程序，要求用户输入两个浮点数，并打印两数之差除以两数 乘积的结果。
在用户输入非数字之前，程序应循环处理用户输入的每对值。

``` c
#include <stdio.h>  //注意审题
int main(void)
{
    float one,two;
    printf("Enter a pair of numbers\n");
    while (scanf("%f %f", &one, &two) == 2)
    {
        printf("%g", (one - two) / (one * two));
        printf("Enter a pair of numbers\n");
    }
    printf("Bye!\n");
    return 0;
}
```



##  第九题

9.修改练习8，使用一个函数返回计算的结果。

``` c
#include <stdio.h>
float Operation(float one, float two);
int main(void)
{
    float one,two;
    printf("Enter a pair of numbers\n");
    while (scanf("%f %f", &one, &two) == 2)
    {
        float Result = Operation(one,two);
        printf("%g\n", Result);
        printf("Enter a pair of numbers\n");
    }
    printf("Bye!\n");
    return 0;
}
float Operation(float one, float two)
{
    return (one - two) / (one * two);
}
```



##  第十题

10.编写一个程序，要求用户输入一个上限整数和一个下限整数，计算 从上限到下限范围内所有整数的平方和，并显示计算结果。
然后程序继续提 示用户输入上限和下限整数，并显示结果，直到用户输入的上限整数小于下 限整数为止。程序的运行示例如下：
Enter　lower　and　upper　integer　limits : 5　9
The　sums　of　the　squares　from　25　to　81　is　255
Enter　next　set　of　limits : 3　25
The　sums　of　the　squares　from　9　to　625　is　5520
Enter　next　set　of　limits : 5　5
Done

``` c
#include <stdio.h>
int calculation(int, int);  //声明函数原型
int main(void)
{
    int lower_num, upper_num;
    printf("Enter　lower　and　upper　integer　limits :");
    scanf("%d %d", &lower_num, &upper_num);
    while (lower_num < upper_num)
    {
        printf("The sums of the squares from %d to %d is ", lower_num * lower_num, upper_num * upper_num);
        calculation(lower_num, upper_num);
        printf("Enter next set of limits :");
        scanf("%d %d", &lower_num, &upper_num);
    }
    printf("Done!");
    return 0;
}
int calculation(int lower_num, int upper_num)
{
    int result;
    for (result = 0; lower_num <= upper_num; lower_num++)
        result += lower_num * lower_num;
    printf("%d\n", result);
}
```


##  第十一题

11.编写一个程序，在数组中读入8个整数，然后按倒序打印这8个整数。

``` c
#include <stdio.h>
#define SIZE 8
int main(void)
{
    int index = 0;  //两阶段 遍历数组赋值和遍历数组输出
    int number[SIZE];
    for (index = 0; index < SIZE; index++)  //数组是从0开始的
        scanf("%d", &number[index]);
    printf("\n");
    for (index = SIZE - 1; index >= 0; index--)
        printf("%d ", number[index]);
    return 0;
}
```


##  第十二题

12.考虑下面两个无限序列：
1.0 + 1.0/2.0 + 1.0/3.0 + 1.0/4.0 + ...
1.0 - 1.0/2.0 + 1.0/3.0 - 1.0/4.0 + ...
编写一个程序计算这两个无限序列的总和，直到到达某次数。提示：奇数个-1 相乘得-1，偶数个-1相乘得1。让用户交互地输入指定的次数，当用户输入0或负值时结束输入。查看运行100项、1000项、10000项后的总和，是否发现每个序列都收敛于某值？

``` c
#include <stdio.h>
int main(void)
{
    int j, index;
    double i = 1;
    double result1 = 0;
    double result2 = 0;
    scanf("%d", &j);
    for (index = 0; index < j; index++, i++)
    {
        result1 += 1 / i;
        if ((int)i & 1)
            result2 += 1 / i;
        else
            result2 -= 1 / i;
        printf("%result1 = %lf   result2 = %lf\n", result1, result2);
    }
    return 0;
}
```


##  第十三题

13.编写一个程序，创建一个包含8个元素的int类型数组，分别把数组元素设置为2的前8次幂。
使用for循环设置数组元素的值，使用do while循环显示数组元素的值。

``` c
#include <stdio.h>
#define SIZE 8
int main(void)
{
    int array[SIZE], index, num;
    for (index = 0, num = 1; index < SIZE; index++, num *= 2)
        array[index] = num;
    index = 0;
    do
    {
        printf("%d\n", array[index]);
        index++;
    } while (index < SIZE);
    return 0;
}
```


## 第十四题

14.编写一个程序，创建两个包含8个元素的double类型数组，使用循环提示用户为第一个数组输入8 个值。第二个数组元素的值设置为第一个数组对应元素的累积之和。
例如，第二个数组的第 4个元素的值是第一个数组前 4个元素之和，第二个数组的第5个元素的值是第一个数组前5个元素之和 （用嵌套循环可以完成，但是利用第二个数组的第5个元素是第二个数组的 第4个元素与第一个数组的第5个元素之和，只用一个循环就能完成任务，不需要使用嵌套循环）。最后，使用循环显示两个数组的内容，第一个数组显示成一行，第二个数组显示在第一个数组的下一行，而且每个元素都与第一个数组各元素相对应。

``` c
#include <stdio.h>
int main(void)
{
    double one[8], two[8];
    int index;
    printf("one = ");
    for (index = 0; index <= 7; index++)
    {
        scanf("%lf", &one[index]); //7个数字需要一次输完   否则就需要再创两个for来输出数组
        printf("%4.1lf|", one[index]);
    }
    printf("\n");
    two[-1] = 0; //数组下标-1
    for (index = 0; index <= 7; index++)
    {
        two[index] = one[index] + two[index - 1];
        printf("%4.1lf|", two[index]);
    }
    return 0;
}
```


## 第十五题

15.编写一个程序，读取一行输入，然后把输入的内容倒序打印出来。可以把输入储存在char类型的数组中，假设每行字符不超过255。
回忆一下，根据%c转换说明，scanf()函数一次只能从输入中读取一个字符，而且在用户按下Enter键时scanf()函数会生成一个换行字符（\n）。

``` c
#include <stdio.h>
int main(void)
{
    char word[255];
    int index = -1;
    do
    {
        index++;                    //思考一下为什么递增一定要放在这一行
        scanf("%c", &word[index]);
    } while (word[index] != '\n');
    for (index -= 1; index >= 0; index--)
        printf("%c", word[index]);
    return 0;
}
```


## 第十六题

16.Daphne以10%的单利息投资了100美元（也就是说，每年投资获利相当于原始投资的10%）。
Deirdre以 5%的复合利息投资了 100 美元（也就是说，利息是当前余额的 5%，包含之前的利息）。
编写一个程序，计算需要多少年Deirdre的投资额才会超过Daphne，并显示那时两人的投资额。


``` c
#include <stdio.h>
int main(void)
{
    double Daphne = 100;
    double Deirdre = 100;
    int years = 1;
    while (Deirdre <= Daphne)
    {
        Daphne = Daphne + 10;
        Deirdre = Deirdre * 1.05;
        years++;
    }
    printf("第%d年Deirdre的投资额超过了Daphne", years);
    return 0;
}
```



## 第十七题

17.Chuckie Lucky赢得了100万美元（税后），他把奖金存入年利率8%的账户。
在每年的最后一天， Chuckie取出10万美元。编写一个程序，计算多少年后Chuckie会取完账户的钱？

``` c
#include <stdio.h>
int main(void)
{
    double dollar = 1000000;
    int year = 0;
    while (dollar > 0)
    {
        year++;
        dollar -= (100000 - dollar * 0.08);
    }
    printf("第%2d年 Chuckie Lucky先生 把钱取完了", year);
    return 0;
}
```



## 第十八题

18.Rabnud博士加入了一个社交圈。起初他有5个朋友。他注意到他的朋友数量以下面的方式增长。
第1周少了1个朋友，剩下的朋友数量翻倍；第2 周少了2个朋友，剩下的朋友数量翻倍。
一般而言，第N周少了N个朋友，剩下的朋友数量翻倍。编写一个程序，计算并显示Rabnud博士每周的朋友数量。
该程序一直运行，直到超过邓巴数（Dunbar’s number）。邓巴数是粗略 估算一个人在社交圈中有稳定关系的成员的最大值，该值大约是150。


``` c
#include <stdio.h>
#define DB 150
int main(void)
{
    int friends, index;
    for (friends = 5, index = 1; friends <= DB; friends -= index, friends *= 2, index++)    //初始朋友5个，第一周减一个朋友；朋友总数不能大于邓巴数；朋友数量减去这周要减的数量，剩下的朋友数量翻倍，每周要减的朋友数量加一。
        printf("第%2d周Rabnud博士有%3d个朋友\n", index, friends);
    return 0;
}
```
