---
layout: post
title: Code Skill
categories: [blog ]
tags: [leetcode, python ]
comments: true
---
#python Notebook[Python3.0]
## 1.function
    def my_abs(x):
        if x>0:
            return x
        else:
            return -x
            
请注意，函数体内部的语句在执行时，一旦执行到return时，函数就执行完毕，并将结果返回。因此，函数内部通过条件判断和循环可以实现非常复杂的逻辑。<br/>
如果想定义一个空的函数，可以在return处写pass;pass可以用作占位符以保证程序可以正常运行。<br/>
内置函数isinstace()函数可以进行数据类型检查。     
          
    if not isinstance(x, (int, float)):
        raise TypeError('bad operand type')
函数可以同时返回多个值，但其实就是一个tuple。在语法上，返回一个tuple可以省略括号，而多个变量可以同时接收一个tuple，按位置赋给对应的值，所以，Python的函数返回多值其实就是返回一个tuple，但写起来更方便。<br/>
### 1.1 递归函数
递归函数的优点是定义简单，逻辑清晰.<br/>
使用递归函数需要注意防止栈溢出。在计算机中，函数调用是通过栈（stack）这种数据结构实现的，每当进入一个函数调用，栈就会加一层栈帧，每当函数返回，栈就会减一层栈帧。由于栈的大小不是无限的，所以，递归调用的次数过多，会导致栈溢出。解决递归调用栈溢出的方法是通过尾递归优化，**尾递归是指，在函数返回的时候，调用自身本身，并且，return语句不能包含表达式。**这样，编译器或者解释器就可以把尾递归做优化，使递归本身无论调用多少次，都只占用一个栈帧，不会出现栈溢出的情况。<br/>
Example:
    
    def fact(n):
        return fact_var(n,1)
        
    def fact_var(value, product):
        if value == 1:
            return product 
        return fact_var(value-1, product*value)
        
##2.一些特性：
###2.1函数切片:<br/>

    def slice():
        li=[1,2,3,4,5...10]
        print li[:3]
        
结果为：[1,2,3]<br/>
也可以进行倒序切片，
    
    printli[:-1]
则结果为[1,2,3]，记住倒数第一个元素的索引是-1.<br/>

    li[:10:2]
意为对Li的前10个数，每2个取1个，结果为[1,3,5,7,9]
    
可以对tuple进行切片操作，返回的结果仍然为tuple.

    (1,2,3,4,5)[:3]
 结果为(1,2,3)<br/>
 
###2.2迭代
在Python中，给定一个tuple或者list，可以使用for循环来进行遍历，称之为迭代，使用**for ... in ...**语句。<br/>

    def iteration:
        Li=[1,2,3,4,6]
        for i in Li:
            print i+1
            
输出结果为[2,3,4,5,7]<br/>

    def iteration:
        li={'a':1, 'b':2, 'c':3}
        for key in li:
            print key
输出结果为[a,c,b]，结果是无序的。<br/>
若想根据value的值输出或者根据key，value一起输出，则：<br/>

    def iteration():
        li={'a':1, 'b':2, 'c':3}
        for value in li.values():
            print value
输出结果为：[1, 3, 2].

    def iteration():
        li={'a':1, 'b':2, 'c':3}
        for k, v in li.items():
            print k, v
输出结果为:{'a':1, 'b':2, 'c':3}

    
 
 
    




       



