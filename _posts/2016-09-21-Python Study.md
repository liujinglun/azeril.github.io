---
layout: post
title: Python notebook
categories: [blog ]
tags: [leetcode, python ]
comments: true
---
# Python Notebook[Python2.7]
## 1.函数

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
    li=[1,2,3,4,5]
    print li[:3]
```
结果为：[1,2,3]
也可以进行倒序切片:
```python
print li[0:]
<<[1,2,3,4,5]

print li[:0]
<<[]--It is a empty list.

print li[1:]
<<[2,3,4,5]
## Get li[1] to li[len(li)-1]

print li[-1:]
<<[5]
##Get li[-1]

print li[:1]
<<[5]
##Get li[len(li)-1]

print li[:-1]
<<[1,2,3,4]
##Get li[0]to li[len(li) - 1 - 1]
```

可以对数组进行周期性筛取：

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

## 2.5Python中类的写法：

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

## 2.6.Python中enumerate的用法

```python
import sys
list1 = {'1', '2', '3'}
for index, item in enumerate(list1):
    print index, item
```
输出结果为：

>0 1
>1 3
>2 2

使用enumerate()函数可以同时遍历索引和函数值。相当于map的用法。

## 2.7.Python新建一个map类型:

```python
nums=[1,2,3]
dic = {}
for i in nums:
    dic[i] = False
```
> 输出结果为：
>
> {1: False, 2: False, 3: False, 5: False}
>
> dic是{key, value}类型，若想只输出key，则直接print key，若想输出value，则print dic[key].

## 2.8.Python在list中删除一个元素x:

```python
list1.discard(x)
list1.remove(x)
```
## 2.9.Python在dict中获取value对应的key值：

```python
print dic.values().index(num)
```
## 2.10.若需要将几个数字插入到list中，并计算和，则可以写成：

```python
list1 = [nums[i], nums[j], nums[k]]
get_Sum = sum(list1)
```

## 11.九宫格中每个square中的元素表示：

```python
for i in range(0, 9):
    for j in range(0, 9):
        element = board[i/3*3+j/3][i%3*3+j%3]
```
## 12.Python中的copy函数：

```python
#浅拷贝，只拷贝父对象，不会拷贝对象内部的子对象；
copy.copy
#深拷贝，拷贝对象及其子对象；
copy.deepcopy
'''
一个例子
'''
import copy
a = [1,2,['a','b']] #原始对象
b = a #赋值，传对象的引用
c = copy.copy(a) #对象拷贝，浅拷贝
d = copy.deepcopy(a) #对象拷贝，深拷贝
a.append(2) #修改对象
a[2].append('c') #修改对象a中的['a', 'b']数组
print 'a:', a # a = [1,2,['a','b','c'], 3]
print 'b', b # b = [1,2,['a', 'b', 'c'], 3]
print 'c', c # c = [1,2,['a', 'b', 'c']]
print 'd', d # d = [1,2, ['a', 'b']]

#另外一种浅拷贝：
a = set(a)
dict.copy(d) = dict(d)
```
## 13.

- 对于list，使用append(value)函数插入数值到list中；
- 对于set，使用add(value)函数插入数值到set中。

## 14.Python中的函数调用

- 注意被调用的函数参数第一位应该是**self**，在其他函数调用该函数时**需要在函数名前面写self,在参数中不需要写self**。

```python
class Solution(object):
  def getNext(self, nums, k):
      le = len(nums)
      targetPosition = -1
      for i in range(le-1, 0, -1):
          if nums[i-1] < nums[i]:
              targetPosition = i - 1
              break
      for i in range(le-1, targetPosition, -1):
          if nums[i] > nums[targetPosition]:
              temp = nums[i]
              nums[i] = nums[targetPosition]
              nums[targetPosition] = temp
              break
      reversed(nums[targetPosition+1:])
      nums[targetPosition+1:] = reversed(nums[targetPosition+1:])
      return nums
      
  def getPermutation(self, n, k):
    self.getNext(nums, k)
```

## 15.Python中“//”表示整数除法。

```python
print 4//2
>> 输出结果为 2.
print 4//3
>> 输出结果为 1.
```
## 16.recursion 递归的理解

可见Leetcode相关题目：

[Permutations](https://leetcode.com/problems/permutations/)

具体思想：

题目为找出[1,2,3]能组成的所有三位数，每个数字只能用一次。

递归的思想是不断化简，由复杂到简单。

- 若1确定的情况下，则考虑2，3组成的二位数；

  - 若2确定的情况下，则考虑3组成的一位数
    - 返回[3]
    - 返回[2, 3]
  - 若3确定的情况下，同理，返回[3,2]
  - 在1确定的情况下，返回[1, 2, 3]和[1, 3, 2].

  递归函数一定有一个条件，达到此条件后函数开始从底向上执行，常见的条件有**nums内元素个数为1**，之后会开始回溯。

  ## 17.Python判断字符串中子字符串的起始位置

  ```python
  needle = "asdf"
  haystack = "basdasdf"
  if needle in haystack:
      print haystack.find(needle)
  << output:4
  ```

## int 边界

在Python中，int类型的最大值为2147483647;

在Python中，int类型的最小值为-2147483648.