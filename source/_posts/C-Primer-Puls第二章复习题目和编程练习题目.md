---

title: C-Primer-Puls第二章复习题目和编程练习题目
date: 2019-08-22 13:00:00
tags: [题目]
categories: C语言
cover: https://s1.ax1x.com/2020/04/26/JcBGNQ.png
---


本章内容为《C Primer Plus第六版》第二章复习题和编程练习题

## 复习题

### 第一题
1. C语言的基本模块是什么？

----------

### 第二题
2. 什么是语法错误？写出一个英语例子和C语言例子。

<!--more-->
----------

### 第三题
3. 什么是语义错误？写出一个英语例子和C语言例子。


----------

### 第四题
4. Indiana Sloth编写了下面的程序，并征求你的意见。请帮助他评定。
        include studio.h
        int main{void} /* 该程序打印一年有多少周 /*
        (
            int s s := 56;
            print(There are s weeks in a year.);
            return 0;

----------

### 第五题
5. 假设下面的4个例子都是完整程序中的一部分，它们都输出什么结果？
        a. printf("Baa Baa Black Sheep.");
        printf("Have you any wool?\n");
        b. printf("Begone!\nO creature of lard!\n");
        c.printf("What?\nNo/nfish?\n");
        d.int num;
        num = 2;
        printf("%d + %d = %d", num, num, num + num);

----------

### 第六题
6. 在main、int、function、char、=中，哪些是C语言的关键字？

----------

### 第七题
7. 如何以下面的格式输出变量words和lines的值（这里，3020和350代表两个变量的值）？
There were 3020 words and 350 lines.

----------

### 第八题
8. 考虑下面的程序：
        #include <stdio.h>
        int main(void)
        {
            int a, b;
            a = 5;
            b = 2; /* 第7行 */
            b = a; /* 第8行 */
            a = b; /* 第9行 */
            printf("%d %d\n", b, a);
            return 0;
        }
 请问，在执行完第7、第8、第9行后，程序的状态分别是什么？

 ----------

### 第九题
9. 考虑下面的程序：
        #include <stdio.h>
        int main(void)
        {
        int x, y;
        x = 10;
        y = 5;/* 第7行 */
        y = x + y; /*第8行*/
        x = x*y;/*第9行*/
        printf("%d %d\n", x, y); return 0;
        }
请问，在执行完第7、第8、第9行后，程序的状态分别是什么？

----------


## 编程练习

### 第一题
1. 编写一个程序，调用一次printf()函数，把你的姓名打印在一行。再调用一次printf()函数，把你的姓名分别打印在两行。然后，再调用两次printf()函数，把你的姓名打印在一行。输出应如下所示（当然要把示例的内容换成你的姓名）：
        Gustav Mahler   <-第 1 次打印的内容
        Gustav          <-第 2 次打印的内容
        Mahler          <-仍是第 2 次打印的内容
        Gustav Mahler   <-第 3 次和第 4 次打印的内容

----------

### 第二题
2. 编写一个程序，打印你的姓名和地址。

----------

### 第三题
3. 编写一个程序把你的年龄转换成天数，并显示这两个值。这里不用考虑闰年的问题。

----------

### 第四题
4. 编写一个程序，生成以下输出：
         For he's a jolly good fellow!
         For he's a jolly good fellow!
         For he's a jolly good fellow!
         Which nobody can deny!
 除了 main()函数以外，该程序还要调用两个自定义函数：一个名为jolly()，用于打印前 3 条消息，调用一次打印一条；另一个函数名为 deny()，打印最后一条消息。

----------

### 第五题
5. 编写一个程序，生成以下输出：
        Brazil, Russia, India, China
        India, China,
        Brazil, Russia
除了main()以外，该程序还要调用两个自定义函数：一个名为br()，调
用一次打印一次“Brazil, Russia”；另一个名为ic()，调用一次打印一次“India, China”。其他内容在main()函数中完成。

----------

### 第六题
6. 编写一个程序，创建一个整型变量toes，并将toes设置为10。程序中还要计算toes的两倍和toes的平方。该程序应打印3个值，并分别描述以示区分。

----------

### 第七题
7. 许多研究表明，微笑益处多多。编写一个程序，生成以下格式的输出：
        Smile!Smile!Smile!
        Smile!Smile!
        Smile!
该程序要定义一个函数，该函数被调用一次打印一次“Smile!”，根据程序的需要使用该函数。

----------

### 第八题
8. 在C语言中，函数可以调用另一个函数。编写一个程序，调用一个名为one_three()的函数。该函数在一行打印单词“one”，再调用第2个函数two()，然后在另一行打印单词“three”。two()函数在一行显示单词“two”。 main()函数在调用 one_three()函数前要打印短语“startingnow:”，并在调用完毕后显示短语“done!”。因此，该程序的输出应如下所示：
        starting now:
        one
        two
        three
        done!
