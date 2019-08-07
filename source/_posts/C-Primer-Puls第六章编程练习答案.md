---
title: C-Primer-Puls第六章编程练习答案
date: 2019-05-18 18:44:00
tags: [C语言,答案]

---



本文章为《C Primer Plus第六版》第六章编程练习的答案


## 第一题
1.编写一个程序，创建一个包含26个元素的数组，并在其中储存26个小 写字母。然后打印数组的所有内容。

``` c
#include <stdio.h>
#include <stdlib.h>
int main(void)
{
        int num;
        char AB;
        char ch[26];
        for (num = 0,AB = 'a'; num <= 26; num++,AB++)
        {
               ch[num] = AB;
               printf(" %c", ch[num]);
        }
        return 0;
}
```

<!--more-->


## 第二题

2.使用嵌套循环，按下面的格式打印字符：

    $
    $$
    $$$
    $$$$
    $$$$$

---

``` c
#include <stdio.h>
#include <stdlib.h>
int main(void)
{
        int num, num2;
        for (num = 0; num < 5; num++)
        {
               for (num2 = 0; num2 <= num; num2++)
                       printf("$");
                       
               printf("\n");
        }
        return 0;
}
```



## 第三题

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
#include <stdlib.h>
int main(void)
{       
        char Fw = 'F';     
        char Fword = 'F';           
        for (Fw = 'F'; Fw >= 'A'; Fw--)      
        {
               for (Fword = 'F'; Fword >= Fw; Fword--)     
                        printf("%c", Fword);

               printf("\n");
        }
        return 0;
}
```


## 第四题


4.使用嵌套循环，按下面的格式打印字母：
A                      65
BC                     66
DEF                    68
GHIJ           71
KLMNO          75
PQRSTU         80
如果你的系统不使用以数字顺序编码的代码，请参照练习3的方案解决。
数组的值为A到Z 用循环来控制输出哪些元素

``` c
#include <stdio.h>
#include <stdlib.h>
int main(void)
{
    char Aword = 'A';         
    int num;                      
    int num2;                         
    for (num = 1; num <= 6; num++)                   
    {
           for (Aword,num2 = 1; num2 <= num;num2++,Aword+)
                printf("%c", Aword)                         
                printf("\n");                                  
    }
        return 0;
}
```


## 第五题

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
#include <stdlib.h>
int main(void)
{
        char w = 'A';       //放到VSIDE里可以更清晰的看出变量的作用
        char m;                                          
        int line;                                     
        int index;                                       
        char space;                        
        char word;                                         
        scanf("%c", &word);
        for (line = -1, space = word - 'A'; w <= word; w++, line++, space--)     
        {
               for (index = 0; index < space; index++)              
                       printf(" ");
               for (index = 0, w = 'A'; index <= line; index++, w++)                                                  
                       printf("%c", w);                              
               for (m = w; m >= 'A'; m--)                              
                       printf("%c", m);
               printf("\n");
        }
        return 0;
}
```



## 第六题

6.编写一个程序打印一个表格，每一行打印一个整数、该数的平方、该数的立方。
要求用户输入表格的上下限。使用一个for循环。

``` c
#include <stdio.h>
#include <stdlib.h>
int main(void)
{
        int start, over;
        printf("请输入开始的值");
        scanf("%d", &start);
        printf("请输入结束的值");
        scanf("%d", &over);
        for (start, over; start <= over;start++)
               printf("%5d的平方为：%5d 立方为：%5d\n",start,start*start,start*start*start);
        return 0;
}
```


## 第七题

7.编写一个程序把一个单词读入一个字符数组中，然后倒序打印这个单 词。
提示：strlen()函数（第4章介绍过）可用于计算数组最后一个字符的下标。

``` c
int main(void)
{
        char word[30];
        scanf("%s", word);
        int size = strlen(word) - 1;
        for (size; size >= 0; size--)
               printf("%c", word[size]);
        return 0;
}
```



## 第八题

8.编写一个程序，要求用户输入两个浮点数，并打印两数之差除以两数 乘积的结果。
在用户输入非数字之前，程序应循环处理用户输入的每对值。

``` c
#include <stdio.h>
#include <stdlib.h>
int main(void)
{
        float f1;
        float f2;
        printf("请输入两个数字");
        while (scanf("%f %f", &f1, &f2) == 2)  
        {
               printf("%f", (f1 - f2) / (f1 * f2));
               printf("请输入两个数字");  
        }
        printf("Bye!\n");
        return 0;
}
```



## 第九题

9.修改练习8，使用一个函数返回计算的结果。

``` c
#include <stdio.h>
#include <stdlib.h>
int process(float n, float m);               //该函数直接输出结果
float proces(float n, float m);              //该函数的返回值为结果，需另外输出返回值   运算成功，结果正确
int main(void)
{
        float f1;
        float f2;
        float rn;
        printf("请输入两个数字");
        while (scanf("%f %f", &f1, &f2) == 2)        
        {
               //process(f1,f2);         //调用函数直接得出的结果
               //printf("%f", (f1 - f2) / (f1 * f2));
               
               rn = handle(f1, f2);     //调用函数 以函数返回值得到结果
               printf("%f", rn);
               printf("请输入两个数字");   
        }
        printf("Bye!\n");                     
        return 0;
}

int process(float n, float m)       //调用函数直接得出的结果
{
        printf("%f", (n - m) / (n * m));
        return 0;
}

float handle(float n, float m)       //调用函数 以函数返回值得到结果
{
        float fin = (n - m) / (n*m);
        return (n - m) / (n * m);
}
```



## 第十题

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
#include <stdlib.h>
int calculation(int n1, int n2);
int main(void)
{
        int num1, num2, num3;
        printf("Enter　lower　and　upper　integer　limits :");
        scanf("%d %d", &num1, &num2);
        while (num1 < num2)
        {
               printf("The sums of the squares from %d to %d is ", num1 * num1, num2 * num2);
               calculation(num1, num2);      
               printf("Enter next set of limits :");
               scanf("%d %d", &num1, &num2);                                             
        }
        printf("Done!");
        return 0;
}
int calculation(int n1,int n2)
{
        int n3;
        for (n3 = 0; n1 <= n2; n1++)
               n3 += n1 * n1;
        printf("%d\n", n3);
}
```


## 第十一题

11.编写一个程序，在数组中读入8个整数，然后按倒序打印这8个整数。

``` c
#include <stdio.h>
#include <stdlib.h>
#define SIZE 8
int main(void)
{
        int index = 0;
        int number[SIZE];
        for (index = 0; index < SIZE; index++)
               scanf("%d", &number[index]);
               
        printf("\n");
        for (index = SIZE-1; index >= 0; index--)     
               printf("%d\n", number[index]);
        return 0;
}
```


## 第十二题



## 第十三题

13.编写一个程序，创建一个包含8个元素的int类型数组，分别把数组元 素设置为2的前8次幂。
使用for循环设置数组元素的值，使用do while循环显 示数组元素的值。

``` c
#include <stdio.h>
#include <stdlib.h>
#define SIZE 8
int main(void)
{
        int num[SIZE], index, n;
        for (index = 0,n = 1; index < SIZE; index++, n *= 2) 
               num[index] = n;                    
        index = 0;
        do
        { 
               printf("%d\n", num[index]);                      
               index++;
        }
        while (index < SIZE);                       
        return 0;
}
```