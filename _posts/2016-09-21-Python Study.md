---
layout: post
title: Python notebook
categories: [blog ]
tags: [leetcode, python ]
comments: true
---
# Python Notebook[Python2.7]
## 1.Function
```python
def my_abs(x):
    if x>0:
        return x
    else:
        return -x
```
请注意，函数体内部的语句在执行时，一旦执行到return时，函数就执行完毕，并将结果返回。因此，函数内部通过条件判断和循环可以实现非常复杂的逻辑。
如果想定义一个空的函数，可以在return处写pass;pass可以用作占位符以保证程序可以正常运行。
内置函数isinstace()函数可以进行数据类型检查。  
```python
if not isinstance(x, (int, float)):
    raise TypeError('bad operand type')
```
函数可以同时返回多个值，但其实就是一个tuple。在语法上，返回一个tuple可以省略括号，而多个变量可以同时接收一个tuple，按位置赋给对应的值，所以，Python的函数返回多值其实就是返回一个tuple，但写起来更方便。<br/>
### 1.1 递归函数
递归函数的优点是定义简单，逻辑清晰.
使用递归函数需要注意防止栈溢出。在计算机中，函数调用是通过栈（stack）这种数据结构实现的，每当进入一个函数调用，栈就会加一层栈帧，每当函数返回，栈就会减一层栈帧。由于栈的大小不是无限的，所以，递归调用的次数过多，会导致栈溢出。解决递归调用栈溢出的方法是通过尾递归优化，**尾递归是指，在函数返回的时候，调用自身本身，并且，return语句不能包含表达式。**这样，编译器或者解释器就可以把尾递归做优化，使递归本身无论调用多少次，都只占用一个栈帧，不会出现栈溢出的情况。
Example:
```python
def fact(n):
    return fact_var(n,1)

def fact_var(value, product):
    if value == 1:
        return product 
    return fact_var(value-1, product*value)
```


## 2.一些特性

### 2.1函数切片

```python
def slice():
    li=[1,2,3,4,5...10]
    print li[:3]
```
结果为：[1,2,3]
也可以进行倒序切片，
```python
printli[:-1]
```
则结果为[1,2,3]，记住倒数第一个元素的索引是-1.

```python
li[:10:2]
```
意为对Li的前10个数，每2个取1个，结果为[1,3,5,7,9]
可以对tuple进行切片操作，返回的结果仍然为tuple.

```python
(1,2,3,4,5)[:3]
```
 结果为(1,2,3)

### 2.2迭代
在Python代码中，给定一个tuple或者list，可以使用for循环来进行遍历，称之为迭代，使用**for ... in ...**语句。

```python
def iteration:
    Li=[1,2,3,4,6]
    for i in Li:
        print i+1
```
输出结果为[2,3,4,5,7]

```python
def iteration:
    li={'a':1, 'b':2, 'c':3}
    for key in li:
        print key
```
输出结果为[a,c,b]，结果是无序的。
若想根据value的值输出或者根据key，value一起输出，则：

```python
def iteration():
    li={'a':1, 'b':2, 'c':3}
    for value in li.values():
        print value
```
输出结果为：[1, 3, 2].

```python
def iteration():
    li={'a':1, 'b':2, 'c':3}
    for k, v in li.items():
        print k, v
```
输出结果为:{'a':1, 'b':2, 'c':3}

### 2.3 类
1.由于类可以起到模板的作用，因此，可以在创建实例的时候，把一些我们认为必须绑定的属性强制填写进去。**通过定义一个特殊的\_\_init\_\_方法，在创建实例的时候，就把name，score等属性绑上去：**

```python
 class student(object):
    def __init__(self, name, sex):
        self.name = name
        self.sex = sex
```

有了\_\_init\_\_方法，在创建实例的时候就不可以传递空的参数，必须传入与\_\_init\_\_方法配套的参数。但是self不需要传，函数可以自己匹配。
```python
   tem = student('allen', 'male')
    tem.name
    <<'allen'
    tem.sex
    <<'male'
```
类是创建实例的模板，实例是类的具体对象，各个实例的数据互相独立，互不影响。
方法是与实例绑定的函数，方法可以直接访问实例的数据。
通过在实例上调用方法，我们就直接操作了对象内部的数据，但无需知道方法内部的实现细节。

## 2.4 self的用法

1.Python类的方法和普通的函数的区别，**在类的方法必须有一个额外的第一个参数(self)**，但是在调用这个方法的时候不必为这个参数赋值。self代表的是类的试了。

2.Python中类的写法：

```python
class Parent:
    def par(self):
        print(self)
class Child(Parent):
    def chi(self):
        print(self)
>output:
c = Child()
c.chi()
c.par()
p = Parent()
p.par()
>result:
<__main__.Child object at 0x0000000002A47080>
<__main__.Child object at 0x0000000002A47080>
<__main__.Parent object at 0x0000000002A47240>
```

3.中序遍历非递归版本：

```python
class Solution(object):
def inorderTraversal(self, root):
	if not root:
		return []
	stack = []
	result = []
	cur = root
	while len(stack)>0 or cur:
		if cur:
			stack.append(cur)
             # using append to get the last element in list.
			cur = cur.left
		else: 
		    cur = stack.pop()
             # first need to pop the top element and then put it              			  into result.
		    result.append(cur.val)
		    cur = cur.right
	return result
```

