---
title: Python实现C-Primer-Puls第十七章复习题目和编程练习题的答案
tags:
  - python
categories: C Primer Plus
cover: 'https://s1.ax1x.com/2020/04/26/JcBGNQ.png'
abbrlink: c5b196d
date: 2020-06-23 10:44:00
---

本章内容为用Python实现《C Primer Plus第六版》第十七章复习题和编程练习题的答案

## 复习题
### 第一题
1. 定义一种数据类型涉及哪些内容？

----------


### 第二题
2. 为什么程序清单17.2 只能沿一个方向遍历链表？如何修改struct film定义才能沿两个方向遍历链表？

----------

### 第三题
3. 什么是ADT？

----------

### 第四题
4. QueueIsEmpty()函数接受一个指向queue结构的指针作为参数，但是也可以将其编写成接受一个queue结构作为参数。这两种方式各有什么优缺点？

----------

### 第五题
5. 栈（stack）是链表系列的另一种数据形式。在栈中，只能在链表的一端添加和删除项，项被“压入”栈和“弹出”栈。因此，栈是一种LIFO（即后进先出last in,first out）结构。
a.设计一个栈ADT
b.为栈设计一个C编程接口，例如stack.h头文件


### 第六题
6. 在一个含有3个项的分类列表中，判断一个特定项是否在该列表中，用顺序查找和二叉查找方法分别需要最多多少次？当列表中有1023个项时分别是多少次？65535个项是分别是多少次？

----------

### 第七题
7. 假设一个程序用本章介绍的算法构造了一个储存单词的二叉查找树。
假设根据下面所列的顺序输入单词，请画出每种情况的树：
a.nice food roam dodge gate office wave
b.wave roam office nice gate food dodge
c.food dodge roam wave office gate nice
d.nice roam office food wave gate dodge

----------

### 第八题
8. 考虑复习题7构造的二叉树，根据本章的算法，删除单词food之后，各树是什么样子？






----------

## 编程练习
### 第一题
1. 修改程序清单17.2，让该程序既能正序也能逆序显示电影列表。一种方法是修改链表的定义，可以双向遍历链表。另一种方法是用递归。
``` python
""" 非ADT双向链表 可正反向及递归反向打印电影列表 """


class Film(object):
    """类结构"""

    def __init__(self):
        self.title = None
        self.rating = None
        self.prev = None  # 记录 上一链
        self.next = None


Head = None  # 链头
Prev = None  # 记录 链尾
Current = None  # 当前链
print("Enter first movie title:")
title = input()
while title:
    if Head is None:  # 链头为空的情况
        Current = Film()
        Head = Current
    else:  # 不为空的情况
        Current = Film()
        Prev.next = Current  # 引入了链尾
        Current.prev = Prev  # 加入上一链 因为有链尾的存在,所以上一链很简单
    Current.title = title
    print("Enter your rating <0-10>:")
    Current.rating = input()  # 按照例题不能做私有变量保护
    print("Enter next movie title (empty line to stop):")
    Prev = Current
    title = input()
if Head is None:
    print("No data entered.")
else:
    print("Here is the movie list:")
Current = Head
while Current is not None:
    print("Movie: %s Rating: %s" % (Current.title, Current.rating))
    Current = Current.next

print("反向打印电影列表：")
Current = Prev
while Current.title:
    print("Movie: %s Rating: %s" % (Current.title, Current.rating))
    if Current.prev is not None:
        Current = Current.prev
    else:
        break

print("递归实现反向打印电影列表：")


def recursion(anything):
    """参数为链表 作用为逆序打印链表中项目的标题和等级"""
    if anything.next:
        recursion(anything.next)
    print("Movie: %s Rating: %s" % (anything.title, anything.rating))


Current = Head
recursion(Current)
print("Bye!")

```


----------

### 第二题
2. 假设list.h（程序清单17.3）使用下面的list定义：
``` c
typedef struct list
{
    Node * head;    /* 指向list的开头 */
    Node * end;     /* 指向list的末尾 */
} List;
```
重写 list.c（程序清单 17.5）中的函数以适应新的定义，并通过films.c（程序清单 17.4）测试最终的代码。

 解释一下 这样改 只是把list从指针改成了一个结构体 所以 各函数形参不用变 需要改变的使用List的代码
那么List原来是用来传递(指向)链表的 把用到的*plist 改成 plist.head 不就也是给了一个链头嘛
和film2相比 就是把链头和链尾做成了一个结构体 好处同样是在添加Item时可以直接借助end(prev)达到链尾
头文件中的几个函数都是需要对链表整体做一个检测之类的 遍历居多 所以这个end链尾暂时没有其二作用
这题太简单 其次是我看后面几题都没有要求写一个ADT的单向链表的 所以还是复习下python

 ``` python
"""ku.py 链表库"""


class Node(object):     # 因为GC机制所以EmptyTheList的“形式工作”就不写了
    """链表节点"""

    def __init__(self):
        self.title = {}
        self.rating = 0
        self.next = None


class Film(object):
    """一个可以存储电影和电影评级的链表"""

    def __init__(self):
        """初始化链头"""
        self.__head = None
        self.__prev = None

    def isempty(self):
        """链表是否为空 如是则返回1"""
        return self.__head is None

    @staticmethod
    def isfull():
        """链表是否已满 通过能否成功创建实例来判断 如是则返回1"""
        item = Node()
        return item is None

    def itemcount(self):
        """链表中有多少节点 返回一个整数数值"""
        link = self.__head
        count = 0
        while link:
            count += 1
            link = link.next
        return count

    def additem(self, node):  # 传过来一个现成的node 那么直接添加下来
        """在链尾中添加一个节点 执行完毕返回0"""
        if self.__head is None:  # 如果链头为空
            self.__head = node
            self.__prev = self.__head
        else:
            self.__prev.next = node  # 链尾添加node
            self.__prev = node  # 更新链尾
        return 0

    def traverse(self, function):
        """将传递来的函数作用于链表中的每一个节点"""
        link = self.__head
        while link:
            function(link)  # link就是一个node 没必要传入link.title和。。。
            link = link.next

```
``` python
"""测试ku"""
from ku import *


def showmovies(node):
    """打印node的两个属性"""
    print("Movie: %s Rating: %s" % (node.title, node.rating))


Link = Film()
if Link.isfull():
    print("No memory available! Bye!")
    exit(1)

print("Enter first movie title:")
movie = Node()
movie.title = input()

while movie.title:
    print("Enter your rating <0-10>:")
    movie.rating = input()
    if Link.additem(movie):
        print("Problem allocating memory")
        break
    if Link.isfull():
        print("The list is now full")
        break
    print("Enter next movie title (empty line to stop):")
    movie = Node()
    movie.title = input()

if Link.isempty():
    print("No data entered. ")
else:
    print("Here is the movie list:")
    Link.traverse(showmovies)

print("You entered %d movies." % (Link.itemcount()))
print("Bye!")

```

----------

### 第三题
3. 假设list.h（程序清单17.3）使用下面的list定义：
``` c
#define MAXSIZE 100
typedef struct list
{
    Item entries[MAXSIZE]; /* 内含项的数组 */
    int items;             /* list中的项数 */
} List;
```
重写 list.c（程序清单 17.5）中的函数以适应新的定义，并通过films.c（程序清单 17.4）测试最终的代码。

 做到最后工作才想起来 list就是一个完美链表
等于直接操作结构体中的数组 对于链表属性full empty这些items可以搞定
addanywhere和delanywhere 通过了测试 因list太智能 有些代码只能被简化
 ``` python
"""链表库 ku.py """


class Node(object):
    """为了Film干净一点就在这做了 有结构体内味了"""
    def __init__(self):
        """生成一个用来存储电影标题和电影评级的二维列表"""
        self.title = {}
        self.rating = 0
        self.result = [self.title, self.rating]  # node是一个列表 表中有两个变量


class Film(object):
    """用来处理node的类"""
    def __init__(self):
        """初始化链头"""
        # self.title = {}
        # self.rating = 0
        # self.node = [self.title, self.rating]
        self.nodes = [i for i in range(0, 10)]  # 列表推导式 在列表中生成100个列表
        # self.nodes = []
        self.items = 0  # 记录列表里有多少项目

    def isempty(self):
        """链表是否为空 如是则返回1"""
        return len(self.nodes) == 0
        # return self.items == 0

    def isfull(self):
        """链表是否已满 通过能否成功创建实例来判断 如是则返回1"""
        return len(self.nodes) == 100
        # return self.items == 100

    def itemcount(self):
        """链表中有多少节点 返回一个整数数值"""
        return len(self.nodes)
        # return self.items

    def additem(self, node):  # 传过来一个现成的node 那么直接添加下来
        """在链尾中添加一个节点 执行完毕返回0"""
        # node.result[0] = node.title
        # node.result[1] = node.rating
        # self.nodes[self.items] = node.result[:]

        self.nodes.append(node)
        self.items += 1
        return 0

    def traverse(self, function):
        """将传递来的函数作用于链表中的每一个节点"""
        for i in range(0, self.items):
            function(self.nodes[i])

# 这两个函数不能写的原因就是增加or删除list元素后会自动排放 我们给一个占位元素就好了
# 这样也算是把原理给写了出来 首先add是index右边的元素向后移 这里给一个切片
# 改的意义不是太大 因为这个切片光芒太耀眼 最重要的数组元素操作也给整简单了

    def addanywhere(self, index, node):
        """从任意位置插入数值"""
        # self.nodes.insert(index, node)
        node.result[0] = node.title
        node.result[1] = node.rating
        self.nodes[index + 1:] = self.nodes[index:] # 直接覆盖了一下 那么这个index就是一个占位元素
        self.nodes[index] = node.result[:]  # 上面那一步做完后 就算是清理出了index的位置 然后存放node
        self.items += 1
        return 0

    def delanywhere(self, index):
        """从任意位置删除数值"""
        # del self.nodes[index]
        self.nodes[index] = 0  # 这一步表示清除
        self.nodes[index:] = self.nodes[index + 1:]  # 然后index后的元素全部前移一个
        return 0

```
``` python
"""测试ku"""
from ku import *    # 和第二题一样


def showmovies(node):
    """打印node的两个属性"""
    print("Movie: %s Rating: %s" % (node.title, node.rating))


Link = Film()
if Link.isfull():
    print("No memory available! Bye!")
    exit(1)

print("Enter first movie title:")
movie = Node()
movie.title = input()

while movie.title:
    print("Enter your rating <0-10>:")
    movie.rating = input()
    if Link.additem(movie):
        print("Problem allocating memory")
        break
    if Link.isfull():
        print("The list is now full")
        break
    print("Enter next movie title (empty line to stop):")
    movie = Node()
    movie.title = input()

if Link.isempty():
    print("No data entered. ")
else:
    print("Here is the movie list:")
    Link.traverse(showmovies)

print("You entered %d movies." % (Link.itemcount()))
print("Bye!")

```

----------

### 第四题
4. 重写mall.c（程序清单17.7），用两个队列模拟两个摊位。
``` python
"""
那下一个版本就直接问要几个摊位 升级这个现在挺简单的
这个摊位变成两个 这个数据就有点小离谱  平均队列大小和等待时长居然不依靠数据提升上去
后来我发现 是因为用户咨询的时间太少了  把第二个摊位关闭掉就会符合这个程序需要的环境了
两点 队列上限10 用户咨询时长 3cycle   使用代码大概有30行 剩下都是类 方法和函数
"""
import random
from myqueue import Queue, Node


def newcustomer(x):
    """"判断是否有新顾客来"""
    if (random.randint(0, 32767) * x / 32767) < 1:
        return True
    else:
        return False


def customertime(when):
    """给新顾客设定参数 咨询时间和来的时间"""
    cust = Node()
    cust.processtime = random.randint(0, 32767) % 3 + 1
    cust.arrive = when
    return cust


class Stall(object):
    """摊位我给封装了"""

    def __init__(self, name):
        """初始化摊位"""
        self.name = name  # 这个实例的名称 方便print
        self.line = Queue()
        self.temp = Node()
        self.turnaways = 0  # 因这个摊位已满而被拒绝的顾客数量
        self.customers = 0  # 加入摊位的顾客数量
        self.served = 0  # 咨询过这个摊位的顾客数量
        self.wait_time = 0  # 顾客被踢出摊位的时间
        self.sum_line = 0  # 累计的队列总长
        self.line_wait = 0  # 队列累计的等待时间

    def addcustomers(self, c_cycle):
        """添加一个新顾客"""
        if self.line.isfull():
            self.turnaways += 1
        else:
            self.customers += 1
            self.temp = customertime(c_cycle)
            self.line.append(self.temp)

    def delcustomers(self, c_cycle):
        """循环更新数据以及踢出咨询完毕的客户"""
        if self.wait_time <= 0 and not self.line.isempty():
            self.line.delete(self.temp)
            self.wait_time = self.temp.processtime
            self.line_wait += (c_cycle - self.temp.arrive)
            self.served += 1
        if self.wait_time > 0:
            self.wait_time -= 1
        self.sum_line += self.line.itemcount()

    def printachievement(self):
        """打印这个摊位的所有信息"""
        if self.customers > 0:  # 不判断两个摊位全部打印
            print("---------------%s------------------" % self.name)
            print("customers accepted: %s" % self.customers)
            print("customers served: %s" % self.served)
            print("turnaways: %s" % self.turnaways)
            print("average queue size: %.2f" %
                  (float(self.sum_line) / cyclelimit))
            print("average wait time: %.2f minutes" %
                  (float(self.line_wait) / self.served))
        else:
            print("No customers!")


min_per_hr = 60.0  # 顾客到达的平均间隔时间
min_per_cust = 0.0  # 顾客到来的平均时间
hours = 0  # 模拟的小时数
perhour = 0  # 每小时平均多少位顾客
cycle = 0  # 循环计数器
cyclelimit = 0  # 计数器的上限
john = Stall("john")
david = Stall("david")  # 两个摊位

random.seed(None)  # 缺省值为当前系统时间
print("Case Study: Sigmund Lander's Advice Booth")
print("Enter the number of simulation hours:")
hours = input()
cyclelimit = min_per_hr * float(hours)
print("Enter the average number of customers per hour:")
perhour = input()
min_per_cust = min_per_hr / float(perhour)

for cycle in range(0, int(cyclelimit)):
    if newcustomer(min_per_cust):  # 如果当前cycle这一分钟有顾客来
        if john.customers <= david.customers:
            john.addcustomers(cycle)
        else:
            david.addcustomers(cycle)
    john.delcustomers(cycle)
    david.delcustomers(cycle)

john.printachievement()
david.printachievement()
print("Bye!")

```
``` python
"""队列模块"""
class Node(object):
    """队列节点"""
    def __init__(self):
        """初始化队列节点"""
        self.arrive = 0
        self.processtime = 0
        self.next = None


class Queue(object):
    """队列类"""
    def __init__(self):
        """初始化队列首尾"""
        self.front = None
        self.rear = None
        self.items = 0

    def isfull(self):
        """检测队列是否已满"""
        return self.items >= 10

    def isempty(self):
        """检测队列是否为空"""
        return self.items == 0

    def itemcount(self):
        """返回队列项目总数"""
        return self.items

    def append(self, node):
        """添加队列节点"""
        if self.isempty():
            self.front = node
            self.rear = node
        else:
            self.rear.next = node
        self.rear = node
        self.items += 1
        return True

    def delete(self, pitem):
        """删除队列节点"""
        pitem = self.front
        self.front = self.front.next
        self.items -= 1
        if self.isempty():  # 如果队头没了 那队尾也就没了
            self.rear = None
        return pitem

```

----------

### 第五题
5. 编写一个程序，提示用户输入一个字符串。然后该程序把该字符串的字符逐个压入一个栈（参见复习题5），然后从栈中弹出这些字符，并显示它们。结果显示为该字符串的逆序。
``` python
"""我的栈库"""


class Item(object):  # 我这个模块并没有做到node直接添加 做到了就是项目通用的效果
    """项目类"""  # 反正c也不行 有两点 传参使用和push添加的时候

    def __init__(self):  # 所以就像最后的二叉树一样 需要变动的有很多
        self.character = ""


class Stack(object):
    """栈类"""

    def __init__(self):
        """初始化栈"""
        self.temp = Item()
        self.array = [self.temp for i in range(0, 100)]
        self.top = 0  # 第一个空位的索引

    def isfull(self):
        """
        操作：　　　  检查栈是否已满
        前提条件：　　ps 指向之前已被初始化的栈
        后置条件：　　如果栈已满，该函数返回true；否则，返回false
        """
        if self.top >= 100:
            return True
        else:
            return False

    def isempty(self):
        """
        操作：　　　  检查栈是否为空
        前提条件：　　ps 指向之前已被初始化的栈
        后置条件：　　如果栈为空，该函数返回true；否则，返回false
        """
        if self.top == 0:
            return True
        else:
            return False

    def push(self, item):
        """
        操作：　　　 把项压入栈顶
        前提条件:　　ps 指向之前已被初始化的栈　item 是待压入栈顶的项
        后置条件:　　如果栈不满，把 item 放在栈顶，该函数返回ture；　
                     否则，栈不变，该函数返回 false
        """
        if not self.isfull():
            self.array[self.top] = item.character
            self.top += 1
            return True
        else:
            return False

    def pop(self, item):
        """
        操作：　　　 从栈顶删除项
        前提条件:  　ps 指向之前已被初始化的栈
        后置条件:　　如果栈不为空，把栈顶的item拷贝到*pitem，
                    删除栈顶的item，该函数返回ture；
                    如果删除操作之前栈为空，栈不变，该函数返回false
        """
        if not self.isempty():
            item = self.array[self.top - 1]
            self.array[self.top - 1] = None  # 这样就算清除了
            self.top -= 1
            return item
        else:
            return False
```
``` python
"""测试栈"""
from mystack import *

stack = Stack()  # 在这个类里存一个数组 自定义低级的那个
node = Item()  # Node的结构 里面就一个character  用来存一个字符

if stack.isfull():
    print("No memory available! Bye!")
    exit(1)

print("Enter an string")
# node.character = input()  # char用来接收分解字符
nodestring = input()

for character in nodestring:
    # 现在开始压入栈顶  压进去 这边要bool 判断就行了
    # 弹出那边用 返回值 然后打印出来
    node.character = character
    stack.push(node)

while not stack.isempty():
    character = ""
    stack.pop(character)
    print(character)
    # ！！！其实这里还是让函数返回bool 但是我传过去的
    # 变量取一个指针传值的作用

```


----------

### 第六题
6. 编写一个函数接受 3 个参数：一个数组名（内含已排序的整数）、该数组的元素个数和待查找的整数。如果待查找的整数在数组中，那么该函数返回 1；如果该数不在数组中，该函数则返回 0。用二分查找法实现。
``` python
"""二分查找 函数只给了两个参数 因为python有点强大"""
nums = [i for i in range(0, 100)]


def bin_search(num_s, num_):
    """二分查找函数参数为要查找的列表和要查找的数字"""
    num_ = int(num_)
    low = 0
    high = len(num_s) - 1
    while low <= high:
        middle = (low + high) // 2
        if num_ == num_s[middle]:
            return 1
        elif num_s[middle] > num_:
            high = middle - 1
        else:  # num > miidle
            low = middle + 1
    return 0


num = input("Please enter a number\n")
if bin_search(nums, num):
    print("True")
else:
    print("False")

```
----------

### 第七题
7. 编写一个程序，打开和读取一个文本文件，并统计文件中每个单词出现的次数。用改进的二叉查找树储存单词及其出现的次数。程序在读入文件后，会提供一个有3个选项的菜单。第1个选项是列出所有的单词和出现的次数。第2个选项是让用户输入一个单词，程序报告该单词在文件中出现的次数。第3个选项是退出。

``` python
"""二叉树的库"""


class Item(object):
    """树叶"""

    def __init__(self):
        self.char = ""
        self.count = 0


class Trnode(object):
    """树枝"""

    def __init__(self, item=None):  # 树叶加树枝时 给个初始值
        """初始化树枝"""
        self.item = item  # 一个初始化替代了 makenode
        self.left = None
        self.right = None


class Pair(object):
    """非公开类"""

    def __init__(self):
        self.parent = None
        self.child = None


class Tree(object):
    """树"""

    def __init__(self):
        """初始化树"""
        self.root = None
        self.size = 0

    def isempty(self):
        """检测树是否为空"""
        if self.root is None:
            return True
        else:
            return False

    def isfull(self):
        """检测树是否已满"""
        if self.size == 100:
            return True
        else:
            return False

    def itemcount(self):
        """返回树的大小"""
        return self.size

    def additem(self, pi):
        """添加一个树叶 参数pi是一个Item"""

        # 在所有事情开始前 要做一个 直接统计单词次数
        if self.intree(pi):  # 如果树中有这个叶子
            # 找到这个树枝的位置 然后count+1
            look = seekitem(pi, self.root)
            # 不出错look就是那个树枝
            look.child.item.count += 1
            return True

        # 下面是 如果是新单词
        if self.isfull():
            print("Tree is full")
            return False

        new_node = Trnode(pi)  # 创建了一个完整树枝
        if new_node is None:
            print("Couldn't create node")
            return False

        self.size += 1
        if self.root is None:
            self.root = new_node
        else:
            addnode(new_node, self.root)
        return True

    def traverse(self, pfun):
        """将pfun这个函数作用于每个树叶"""
        if self.root is not None:
            inorder(self.root, pfun)

    def deleteall(self):
        """删除所有树叶和树枝"""
        if self.root is not None:
            deleteallnodes(self.root)
            self.root = None
            self.size = 0

    def deleteitem(self, pi):
        """在树中删除pi这个树叶"""
        look = seekitem(pi, self.root)
        if look.child is None:
            return False
        if look.parent is None:  # 可能是技术问题 无法将deletenode作为一个方法直接调用
            # deletenode(self.root)               # 传入树枝
            if self.root is None:
                self.root = self.root.right
            elif self.root.right is None:
                self.root = self.root.left
            else:
                temp = self.root.left
                while temp.right is not None:
                    temp = temp.right
                    continue
                temp.right = self.root.right
                temp = self.root
                self.root = self.root.left
        elif look.parent.left == look.child:  # 没有直接删除
            # deletenode(look.parent.left)    # 只能动root的指向
            if look.parent.left.left is None:
                look.parent.left = look.parent.left.right
            elif look.parent.left.right is None:
                look.parent.left = look.parent.left.left
            else:
                temp = look.parent.left.left
                while temp.right is not None:
                    temp = temp.right
                    continue
                temp.right = look.parent.left.right
                temp = look.parent.left
                look.parent.left = look.parent.left.left
        else:  # look.parent.right == look.child
            # deletenode(look.parent.right)
            if look.parent.right.left is None:
                look.parent.right = look.parent.right.right
            elif look.parent.right.right is None:
                look.parent.right = look.parent.right.left
            else:
                temp = look.parent.right.left
                while temp.right is not None:
                    temp = temp.right
                    continue
                temp.right = look.parent.right.right
                temp = look.parent.right
                look.parent.right = look.parent.right.left
        self.size -= 1
        return True

    def intree(self, pi):
        """检查树中是否有pi这个树叶"""
        return not seekitem(pi, self.root).child is None

    def printcount(self, pi):
        """定制方法 打印pi的count"""
        look = seekitem(pi, self.root)
        if look.child is None:
            print("There is no such word")
        else:
            print("There are %d 个 %s words" %
                  (look.child.item.count, look.child.item.char))


def deletenode(ptr):
    """私有函数 删除ptr指向的节点"""
    temp = None
    if ptr.left is None:  # 删除右节点
        temp = ptr
        ptr = ptr.right
        del temp
    elif ptr.right is None:  # 删除左节点
        temp = ptr
        ptr = ptr.left
        del temp
    else:  # 删除两个节点
        temp = ptr.left
        while temp.right is not None:
            temp = temp.right
            continue
        temp.right = ptr.right
        temp = ptr
        ptr = ptr.left
        del temp


def deleteallnodes(root):
    """程序结束 删除所有节点"""
    if root is not None:
        pright = root.right
        deleteallnodes(root.left)
        root = None
        del root
        deleteallnodes(pright)


def inorder(root, pfun):
    """遍历树 并将pfun作用于每个item"""
    if root is not None:
        inorder(root.left, pfun)
        pfun(root.item)
        inorder(root.right, pfun)


def seekitem(pi, ptree):
    """在树中查找pi"""
    look = Pair()
    look.parent = None
    look.child = ptree

    if look.child is None:  # 空树
        return look

    while look.child is not None:
        if toleft(pi, look.child.item):  # 左节点对比
            look.parent = look.child
            look.child = look.child.left
        elif toright(pi, look.child.item):  # 左节点对比
            look.parent = look.child
            look.child = look.child.right
        else:  # 这个因情况而定
            break  # 这里是没有这个item
    return look


def addnode(new_node, root):  # 递归
    """root树中添加一个new_node节点"""
    if toleft(new_node.item, root.item):
        if root.left is None:
            root.left = new_node
            root.left.item.count += 1
        else:
            addnode(new_node, root.left)
    elif toright(new_node.item, root.item):
        if root.right is None:
            root.right = new_node
            root.right.item.count += 1
        else:
            addnode(new_node, root.right)
    else:
        print("location error in addnode()")
        exit(1)


def toleft(item1, item2):
    """对比item 决定树叶位置"""
    if item1.char < item2.char:
        return True
    else:
        return False


def toright(item1, item2):
    """对比item 决定树叶位置"""
    if item1.char > item2.char:
        return True
    else:
        return False
```
``` python
"""测试库"""
from mytree import *

fr = open("123.txt", "r")

index = 0
word = ""
wordlist = []
TwoT = Tree()

for line in fr.readlines():  # 把一行读取到line中 然后过滤line   取出一个单词append到列表中 逐次存入树中
    line = line.strip("\n")
    line = list(line)
    while index < len(line) and line[index]:
        if line[index] != " ":  # 空格以外的字符
            word += line[index]
            index += 1
        else:  # 遇到空格
            wordlist.append(word)
            word = ""
            index += 1
            continue
    if len(line) != 0:  # 遇到空行
        wordlist.append(word)
        index = 0
        word = ""
fr.close()

for word in wordlist:
    temp = Item()
    temp.char = word
    if TwoT.isfull():
        print("No data space")
    else:
        TwoT.additem(temp)


def menu():
    """菜单函数"""
    print(
        "\n-----------------------------------------------------------------------------------\n"
        "l) 列出所有的单词和出现的次数  i) 输入一个单词，程序报告该单词在文件中出现的次数  q)退出\n"
    )
    try:
        ch = input()
        while ch:
            ch.lower()
            if ch not in "liq":  # 判断
                print("Please enter an l, i, or q:")
            else:
                break
            ch = input()
    except EOFError:
        ch = "q"
    return ch


def printitem(citem):
    """定制函数 打印item"""
    print("There are %3d 个 %9s words" % (citem.count, citem.char))


def IASC():
    """input and scan count"""
    temp_ = Item()
    word_ = input("Please enter a word:\n")
    temp_.char = word_
    TwoT.printcount(temp_)


choice = menu()
while choice != "q":
    if choice == "l":
        TwoT.traverse(printitem)
    elif choice == "i":
        IASC()
    else:
        print("Switching error")
    choice = menu()
print("Bye.")
```
----------

### 第八题
8. 修改宠物俱乐部程序，把所有同名的宠物都储存在同一个节点中。当用户选择查找宠物时，程序应询问用户该宠物的名字，然后列出该名字的所有宠物（及其种类）。
```python
"""二叉树"""


class Item(object):
    """树叶类"""

    def __init__(self):
        """初始化树叶"""
        self.petname = ""
        self.petkind = ""
        self.petkinds = set()

    def printitem(self):
        """内置小方法 方便打印"""
        for kind in self.petkinds:
            print("petname：%s petkind：%s" % (self.petname, kind))


class Trnode(object):
    """树枝"""

    def __init__(self, item=None):  # 树叶加树枝时 可以给个初始值
        """初始化树枝"""
        self.item = item  # 一个初始化替代了 makenode
        self.left = None
        self.right = None


class Pair(object):
    """非公开类"""

    def __init__(self):
        self.parent = None
        self.child = None


class Tree(object):
    """树类"""
    def __init__(self):
        """初始化树"""
        self.root = None
        self.size = 0

    def isempty(self):
        """检测树是否为空"""
        if self.root is None:
            return True
        else:
            return False

    def isfull(self):
        """检测树是否已满"""
        if self.size == 10:
            return True
        else:
            return False

    def itemcount(self):
        """返回树的大小"""
        return self.size

    def additem(self, pi):
        """添加一个树叶 参数pi是一个Item"""
        if not pi.petname.isalpha() or not pi.petkind.isalpha():
            print("you mother fuck")
            exit(1)  # pi的字符串是不是空的
        if self.intree(pi):
            look = seekitem(pi, self.root)
            look.child.item.petkinds.add(pi.petkind)  # 如果存在即追加到集合中
            self.size += 1
            return True

        if self.isfull():
            print("Tree is full")
            return False

        new_node = Trnode(pi)  # 创建了一个完整树枝
        if new_node is None:
            print("Couldn't create node")
            return False

        self.size += 1
        if self.root is None:
            self.root = new_node
            self.root.item.petkinds.add(new_node.item.petkind)
            # kinds是由item中的kind组成的 逐次追加 这个树根追加
        else:
            addnode(new_node, self.root)
        return True

    def intree(self, pi):
        """检查树中是否有pi这个树叶"""
        return not seekitem(pi, self.root).child is None

    def traverse(self, pfun):
        """将function这个函数作用于每个树叶"""
        if self.root is not None:
            inorder(self.root, pfun)

    def deleteall(self):
        """删除所有树叶和树枝"""
        if self.root is not None:
            deleteallnodes(self.root)
            self.root = None
            self.size = 0

    def deleteitem(self, pi):
        """在树中删除pi这个树叶"""
        look = seekitem(pi, self.root)
        # 只判断petname是否存在
        if look.child is None:
            return False

        # 然后检测这个节点中的petkinds有没有要删除的那个
        if pi.petkind in look.child.item.petkinds:
            look.child.item.petkinds.remove(pi.petkind)

        if len(look.child.item.petkinds) == 0:
            # 删到petkinds为空是再做节点删除的操作
            if look.parent is None:
                if self.root is None:
                    self.root = self.root.right
                elif self.root.right is None:
                    self.root = self.root.left
                else:
                    temp = self.root.left
                    while temp.right is not None:
                        temp = temp.right
                        continue
                    temp.right = self.root.right
                    temp = self.root
                    self.root = self.root.left
            elif look.parent.left == look.child:
                if look.parent.left.left is None:
                    look.parent.left = look.parent.left.right
                elif look.parent.left.right is None:
                    look.parent.left = look.parent.left.left
                else:
                    temp = look.parent.left.left
                    while temp.right is not None:
                        temp = temp.right
                        continue
                    temp.right = look.parent.left.right
                    temp = look.parent.left
                    look.parent.left = look.parent.left.left
            else:  # look.parent.right == look.child
                if look.parent.right.left is None:
                    look.parent.right = look.parent.right.right
                elif look.parent.right.right is None:
                    look.parent.right = look.parent.right.left
                else:
                    temp = look.parent.right.left
                    while temp.right is not None:
                        temp = temp.right
                        continue
                    temp.right = look.parent.right.right
                    temp = look.parent.right
                    look.parent.right = look.parent.right.left
        self.size -= 1
        return True


def deletenode(ptr):
    """技术问题 这个函数没法用"""
    temp = None
    if ptr.left is None:  # 父左
        temp = ptr
        ptr = ptr.right
        del temp
    elif ptr.right is None:  # 父右
        temp = ptr
        ptr = ptr.left
        del temp
    else:  # 两个节点都不为空的话
        temp = ptr.left
        while temp.right is not None:
            temp = temp.right
            continue
        temp.right = ptr.right
        temp = ptr
        ptr = ptr.left
        del temp


def deleteallnodes(root):
    """程序结束 删除所有节点"""
    if root is not None:
        pright = root.right
        deleteallnodes(root.left)
        root = None
        del root
        deleteallnodes(pright)


def inorder(root, pfun):
    """遍历树 并将pfun作用于每个item"""
    if root is not None:
        inorder(root.left, pfun)
        pfun(root.item)
        inorder(root.right, pfun)


def seekitem(pi, ptree):  # 相比较原版的seekitem 这个只检测petname的存在
    """在树中查找pi"""
    look = Pair()  # 当然 toleft和toright也要改
    look.parent = None
    look.child = ptree
    if look.child is None:
        return look
    while look.child is not None:
        if toleft(pi, look.child.item):
            look.parent = look.child
            look.child = look.child.left
        elif toright(pi, look.child.item):
            look.parent = look.child
            look.child = look.child.right
        else:
            break
    return look


def addnode(new_node, root):  # 递归
    """root树中添加一个new_node节点"""
    if toleft(new_node.item, root.item):
        if root.left is None:
            root.left = new_node  # 这里 还有下面那个kind追加
            root.left.item.petkinds.add(new_node.item.petkind)
        else:
            addnode(new_node, root.left)
    elif toright(new_node.item, root.item):
        if root.right is None:
            root.right = new_node
            root.right.item.petkinds.add(new_node.item.petkind)
        else:
            addnode(new_node, root.right)
    else:
        print("location error in addnode()")
        exit(1)


def toleft(item1, item2):
    """只有petname的对比了"""
    if item1.petname < item2.petname:
        return True
    else:
        return False


def toright(item1, item2):
    """向右导航"""
    if item1.petname > item2.petname:
        return True
    else:
        return False

```
``` python
"""和第七题套路一样 不过需要适配的函数多了点"""
from mytree import *


class petclub(object):
    """方便使用创建的类"""

    def __init__(self):
        """初始化宠物俱乐部"""
        self.pets = Tree()

    def addpet(self):
        """添加宠物"""
        temp = Item()
        if self.pets.isfull():
            print("No room in the club!")
        else:
            print("Please enter name of pet:")
            temp.petname = input()
            print("Please enter pet kind:")
            temp.petkind = input()
            temp.petname = temp.petname.lower()
            temp.petkind = temp.petkind.lower()
            self.pets.additem(temp)

    def droppet(self):
        """丢掉宠物 这个功能的kind不是虚的"""
        temp = Item()
        if self.pets.isempty():
            print("No entries!")
            return
        print("Please enter name of pet you wish to delete:")
        temp.petname = input()
        print("please enter pet kind:")
        temp.petkind = input()
        temp.petname = temp.petname.lower()
        temp.petkind = temp.petkind.lower()
        print("%s the %s " % (temp.petname, temp.petkind))
        if self.pets.deleteitem(temp):
            print("is dropped from the club.")
        else:
            print("is not a member.")

    def showpets(self):
        """显示所有宠物"""
        if self.pets.isempty():
            print("No entries!")
        else:
            self.pets.traverse(printitem)  # 局部自建函数

    def findpet(self):
        """查找宠物 并打印所有同名但不同种类的其他宠物"""
        temp = Item()
        if self.pets.isempty():
            print("No entries!")
            return
        print("Please enter name of pet you wish to find:")
        temp.petname = input()
        print("please enter pet kind:")
        temp.petkind = input()
        temp.petname = temp.petname.lower()
        temp.petkind = temp.petkind.lower()
        print("%s the %s " % (temp.petname, temp.petkind))
        look = self.pets.intree(temp)
        if look is not None:
            look.item.printitem()  # 类自带方法
        else:
            print("is not a member")


def printitem(item):
    """traverse要用的函数"""
    for kind in item.petkinds:  # kind是个列表
        print("petname：%s petkind：%s" % (item.petname, kind))


def menu():
    """菜单函数"""
    print(
        "\n----------------------------------------------\n"
        "    Nerfville Pet Club Membership Program\n"
        "Enter the letter corresponding to your choice:\n"
        "a) add a pet             l) show list of pets\n"
        "n) number of pets        f) find pets\n"
        "d) delete a pet          q) quit"
    )
    try:
        ch = input()
        while ch:
            ch.lower()
            if ch not in "alrfndq":  # 判断
                print("Please enter an a, l, f, n, d, or q:")
            else:
                break
            ch = input()
    except EOFError:
        ch = "q"
    return ch


if __name__ == "__main__":
    pettree = petclub()
    choice = menu()
    while choice != "q":
        if choice == "a":
            pettree.addpet()
        elif choice == "l":
            pettree.showpets()
        elif choice == "f":
            pettree.findpet()
        elif choice == "n":
            print("%d pets in club" % (pettree.pets.itemcount()))
        elif choice == "d":
            pettree.droppet()
        else:
            print("Switching error")
        choice = menu()
    pettree.pets.deleteall()
    print("Bye.")

```
----------
