---

title: C-Primer-Puls第八章复习题目和编程练习题的答案
date: 2019-09-03 14:31:00
tags: [题目,答案]
categories: C语言
cover: https://s1.ax1x.com/2020/04/26/JcBGNQ.png
---


本章内容为《C Primer Plus第六版》第八章复习题和编程练习题的答案


## 复习题
### 第一题
1. putchar(getchar())是一个有效表达式，它实现什么功能?getchar(putchar())是否也是有效表达式？

----------


### 第二题
2. 下面的语句分别完成什么任务？
        a.putchar('H');
        b.putchar('\007');
        c.putchar('\n');
        d.putchar('\b');

<!--more-->

----------


### 第三题
 3. 假设有一个名为 count 的可执行程序，用于统计输入的字符数。设计一个使用 count 程序统计essay文件中字符数的命令行，并把统计结果保存在 essayct文件中。

----------

### 第四题
4. 给定复习题3中的程序和文件，下面哪一条是有效的命令？
        a.essayct < essay
        b.count essay
        c.essay >count

----------

### 第五题
5. EOF是什么？

----------

### 第六题
6. 对于给定的输出（ch是int类型，而且是缓冲输入），下面各程序段的输出分别是什么？
        a.输入如下：
        If you quit, I will.[enter]
        程序段如下：
        while ((ch = getchar())!= 'i')
                putchar(ch);
        b.输入如下：
        Harhar[enter]
        程序段如下：
        while ((ch = getchar()) != '\n')
        {
                putchar(ch++);
                putchar(++ch);
        }

----------

### 第七题
7. C如何处理不同计算机系统中的不同文件和换行约定？

----------

### 第八题
8. 在使用缓冲输入的系统中，把数值和字符混合输入会遇到什么潜在的问题？


----------

## 编程练习

### 第一题
1. 设计一个程序，统计在读到文件结尾之前读取的字符数。
``` c
#include <stdio.h>
int main(void)
{
    char ch;
    int word = 0;
    while ((ch = getchar()) != EOF)
        word++;
    printf("%d", word - 1);
    return 0;
}
```
----------

### 第二题
2. 编写一个程序，在遇到 EOF 之前，把输入作为字符流读取。程序要打印每个输入的字符及其相应的ASCII十进制值。注意，在ASCII序列中，空格字符前面的字符都是非打印字符，要特殊处理这些字符。如果非打印字符 是换行符或制表符，则分别打印\n或\t。否则，使用控制字符表示法。例如,ASCII的1是Ctrl+A，可显示为^A。注意，A的ASCII值是Ctrl+A的值加上 64。其他非打印字符也有类似的关系。除每次遇到换行符打印新的一行之外，每行打印10对值。（注意：不同的操作系统其控制字符可能不同。）
``` c
#include <stdio.h>
int main(void) //还有一些BUG  换行符和制表符一块输出时会乱
{
	char ch;
	int index = 0, CR = 0, SP = 0;
	while ((ch = getchar()) != EOF)
	{
		if (ch == '\n')
		{
			index = 0;
			CR++;
			continue;
		}
		else if (ch == '\t')
		{
			SP++;
			continue; //统计制表符和换行符的个数 在else里统一输出
		}				//一个换行我直接忽略掉了 从两个开始输出
		else
		{
			for (int i = 2; i <= CR; i++)
			{
				printf("\\n ");
				index++;
				if ((index % 10) == 0)
					printf("\n");
			}
			for (int j = 1; j <= SP; j++)
			{
				printf("\\t ");
				index++;
				if ((index % 10) == 0)
					printf("\n");
			}
			CR = 0;
			SP = 0;
			printf("%c-%d ", ch, ch);
			index++;
		}
		if ((index % 10) == 0)
			printf("\n");
	}
	return 0;
}
```

----------

### 第三题
3. 编写一个程序，在遇到 EOF 之前，把输入作为字符流读取。该程序要报告输入中的大写字母和小写字母的个数。假设大小写字母数值是连续的。或者使用ctype.h库中合适的分类函数更方便。
``` c
#include <stdio.h>
#include <ctype.h>
int main(void)
{
    char ch;
    int _upper = 0;
    int _lower = 0;
    while ((ch = getchar()) != EOF)
    {
        if (isupper(ch))    //if (ch >= 'A' && ch <= 'Z');
            _upper++;
        else if (islower(ch))   //if (ch >= 'a' && ch <= 'z');
            _lower++;
    }
    if (_upper)
        printf("%d\n", _upper);
    if (_lower)
        printf("%d\n", _lower);
    return 0;
}
```
----------

### 第四题
4. 编写一个程序，在遇到EOF之前，把输入作为字符流读取。该程序要报告平均每个单词的字母数。不要把空白统计为单词的字母。实际上，标点符号也不应该统计，但是现在暂时不同考虑这么多（如果你比较在意这点，考虑使用ctype.h系列中的ispunct()函数）。
``` c
#include <stdio.h>
#include <ctype.h>
int main(void)
{
    int character = 0, word = 0;
    int ca = 0, wr = 0;
    char ch;
    while ((ch = getchar()) != EOF)
    {
        if (ch != ' ')
        {
            if (islower(ch) || isupper(ch))
            {
                character++;
                ca++;
                continue;
            }
        }
        word++;
        printf("第%d个单词有%d个字母\n", word, character);
        character = 0;
        wr++;
        if (ch == '\032')
            break;
    }
    printf("平均每个单词的字母数为%d\n", ca / wr);
    return 0;
}
```
----------

### 第五题
5. 修改程序清单8.4的猜数字程序，使用更智能的猜测策略。例如，程序最初猜50，询问用户是猜大了、猜小了还是猜对了。如果猜小了，那么下一次猜测的值应是50和100中值，也就是75。如果这次猜大了，那么下一次猜测的值应是50和75的中值，等等。使用二分查找（binary search）策略，如果用户没有欺骗程序，那么程序很快就会猜到正确的答案。
``` c
#include <stdio.h>
int main(void)
{
    int guess, start = 1, end = 100, ch;    //bug太多
    guess = (start + end) / 2;
    printf("选择一个 1 到 100 之间的整数\n结果为 %d\n如果大于结果请输入 > ，反之\n如果结果结果正确请输入 ！ \n", guess);
    while ((ch = getchar()) != '!')
    {
        while (getchar() != '\n')
            continue;
        if (ch == '>')
            end = guess;
        else if (ch == '<')
            start = guess;
        guess = (start + end) / 2;
        printf("结果为%d？\n", guess);
    }
    printf("结果为%d\n", guess);
    return 0;
}
```

----------

### 第六题
6. 修改程序清单8.8中的get_first()函数，让该函数返回读取的第1个非空白字符，并在一个简单的程序中测试。
``` c
/*
char get_first(void)	//程序清单8.8
{
    int ch;
    ch = getchar();
    while (getchar() != '\n')
        continue;
    return ch;
}
*/
#include <stdio.h>
char get_first(void);
int main(void)
{
    char ch;
    ch = get_first();
    printf("第一个非空白字符为%c", ch);
    return 0;
}
char get_first(void)
{
    char ch;
    while ((ch = getchar()) != '\n')
    {
        if ((ch == ' ') || (ch == '\t'))
            continue;
        else
            return ch;
    }
}
```
----------

### 第七题
7. 修改第7章的编程练习8，用字符代替数字标记菜单的选项。用q代替5作为结束输入的标记。

		参考第八题

----------

### 第八题
8. 编写一个程序，显示一个提供加法、减法、乘法、除法的菜单。获得用户选择的选项后，程序提示用户输入两个数字，然后执行用户刚才选择的操作。该程序只接受菜单提供的选项。程序使用float类型的变量储存用户输入的数字，如果用户输入失败，则允许再次输入。进行除法运算时，如果用户输入0作为第2个数（除数），程序应提示用户重新输入一个新值。该程序的一个运行示例如下：
``` c
#include <stdio.h>
double function(char);
void space(void);
int main(void)
{
    double answer = 0;
    float num1 = 0, num2 = 0;
    printf("请输入运算符 + - * / （输入q以退出）");
    while ((ch = getchar()) != 'q')
    {
        while (getchar() != '\n')
            continue;
        switch (ch)
        {
        case '+':
            answer = function('+');
            break;
        case '-':
            answer = function('-');
            break;
        case '*':
            answer = function('*');
            break;
        case '/':
            answer = function('/');
            break;
        default:
            printf("输入错误\n请输入运算符 + - * / (输入q以退出)\n");
            break;
        }
        printf("结果为%.2lf", answer);
        space();
    }
    return 0;
}
double function(char ch)
{
    float num1, num2;
    double result;
    printf("当前为 %c 运算请输入两个数字", ch);
    while (scanf("%f%f", &num1, &num2) == 2)
    {
        if (ch == '/')
        {
            if (num2 == 0)
            {
                printf("除数不能为零 请重新输入\n");
                printf("当前为 %c 运算请输入两个数字", ch);
                continue;
            }
        }
        break;
    }
    if (ch == '+')
        result = num1 + num2;
    else if (ch == '-')
        result = num1 - num2;
    else if (ch == '*')
        result = num1 * num2;
    else
        result = num1 / num2;
    return result;
}
void space(void)
{
    printf("\n请输入运算符 + - * / (输入q以退出)");
    while (getchar() != '\n')
        continue;
}
```