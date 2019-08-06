---
title: C-Primer-Puls第七章编程练习答案
date: 2019-05-19 20:07:00
tags: [C语言,答案]

---



本文章为《C Primer Plus第六版》第七章编程练习的答案


## 第一题

1.编写一个程序读取输入，读到#字符停止，然后报告读取的空格数、 换行符数和所有其他字符的数量。

    #include <stdio.h>
    #include <stdlib.h>
    #include <ctype.h>
    int main(void)
    {
    	char ch;
    	int n_word = 0;
    	int n_space = 0;						
    	int n_hh = 1;
    	while ((ch  = getchar()) != '#')		
    	{
    		n_word += 1;
    		if (ch == ' ')						
    		{
    			n_space += 1;
    			continue;						
    		}				
    		else if (ch == '\n')
    		{
    			n_hh += 1;
    			continue;
    		}
    	}
    	printf("这段字符串中有%d个空格，%d个换行符，总共%d个字符", n_space, n_hh, n_word);
    	return 0;
    }

<!--more-->

## 第二题


2.编写一个程序读取输入，读到#字符停止。程序要打印每个输入的字符以及对应的ASCII码（十进制）。
一行打印8个字符。建议 : 使用字符计数 和求模运算符（%）在每8个循环周期时打印一个换行符。

    #include <stdio.h>
    #include <stdlib.h>
    int main(void)	
    {
    		char c;			
    		int i = 0;		
    		while ((c = getchar()) != '#')					
    		{												
    			if (c == '\n')								
    				continue;	
    			i++;
    				printf("%c-%d ", c, c);					
    			if (i % 8 == 0)
    				printf("\n");
    		}
    	return 0;
    }
    
    
    
## 第三题
    
3.编写一个程序，读取整数直到用户输入0。
输入结束后，程序应报告 用户输入的偶数（不包括 0）个数、这些偶数的平均值、输入的奇数个数及 其奇数的平均值。

    #include <stdio.h>
    #include <stdlib.h>
    #define zero 0
    int main(void)
    {
    	int      num = 0;	//接收指定值
    	int   n_even = 0;	//偶数的个数
    	int even_num = 0;	//偶数的总和
    	int    n_odd = 0;	//奇数的个数
    	int  odd_num = 0;	//奇数的总和
    	//while ((num = getchar()) != 'o')			//不能用getchar 因为它一次只会吃一个字符
    	while (scanf("%d", &num), num != zero)
    	{
    		if (num == '\n')
    			continue;
    		if (num % 2 == 0)
    		{
    			n_even++;			
    			even_num += num;
    			continue;			//提升程序运行速度
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

## 第四题

4.使用if else语句编写一个程序读取输入，读到#停止。
用感叹号替换句 号，用两个感叹号替换原来的感叹号，最后报告进行了多少次替换。
    
    #include <stdio.h>
    #include <stdlib.h>
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


## 第五题

5.使用switch重写练习4。
    
    #include <stdio.h>
    #include <stdlib.h>
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
    	printf("其中 . 符号替换了%d次 ！ 符号替换了%d次\n",one, two);
    	return 0;
    }


## 第六题


6.编写程序读取输入，读到#停止，报告ei出现的次数。
注意该程序要记录前一个字符和当前字符。用“Receive your eieio award”这样的输入来测试

    #include <stdio.h>
    #include <stdlib.h>
    int main(void)
    {
    	char ch;
    	char ar;				//ar就是上一个值的载体
    	int fre = 0;
    	while ((ch = getchar()) != '#')
    	{
    		if (ch == 'i' && ar == 'e')
    			fre++;
    			ar = ch;				//ar不能被立即（覆）赋值 否则它根本无法保存上一个值
    	}
    	printf("%d", fre);
    	return 0;
    }