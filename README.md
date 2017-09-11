# Python基础面试题 #

[TOC]

## 1.Python反转序列(列表、元组、字符串)的几种方法 ##
### 使用reversed(seq)内置函数 ###
reversed(seq)是将序列（seq）反转，返回一个迭代器。
```python
# reverse list
>>> l = ['A', 'B', 'C']
>>> x  = list(reversed(l))
>>> x
['C', 'B', 'A']

# reverse tuple
>>> t = ('A', 'B', 'C')
>>> y = tuple(reversed(t))
>>> y
('C', 'B', 'A')

# reverse str
>>> s = 'ABC'
>>> z = ''.join(reversed(s))
>>> z
'CBA'
>>> 
```
注意一点，reversed(seq)函数并没有改变seq序列本身，如需改动seq序列本身，将结果赋值给seq即可。以列表为例：
```python
# reverse list in place
>>> l = ['A', 'B', 'C']
>>> l  = list(reversed(l))
>>> l
['C', 'B', 'A']
```
### 使用切片操作[::-1] ###
切片用法`[<start>:<end>:<step>]`，其中start默认值是0，end默认值是len(seq)，step默认值是1。此处省略了start和end，步长为-1代表反向切片（从右向左每次前进1步）。
```python
# reverse list
>>> l = ['A', 'B', 'C']
>>> x = l[::-1]
>>> x
['C', 'B', 'A']

# reverse tuple
>>> t = ('A', 'B', 'C')
>>> y = t[::-1]
>>> y
('C', 'B', 'A')

# reverse str
>>> s = 'ABC'
>>> z = s[::-1]
>>> z
'CBA'
>>> 
```
由于切片操作返回的是与序列类型相同的新对象，也不会改变原始的序列，如需改变，将结果赋值原始序列。以字符串为例：
```python
# reverse str in place
>>> s = 'ABC'
>>> s = s[::-1]
>>> s
'CBA'
>>> 
```
### 列表的原地反转reverse()方法 ###
由于列表是可变类型，其reverse()方法可以原地反转列表中元素，无返回值（通常来讲原地改变对象的方法都没有返回值或是说返回值都是None），元组和字符串都是不可变类型，因此都没有reverse()方法。
```python
# reverse list in place
>>> l = ['A', 'B', 'C']
>>> l.reverse()
>>> l
['C', 'B', 'A']
>>> 
```
原文参考：[Python反转序列(列表、元组、字符串)的几种方法](http://www.revotu.com/reverse-sequence-list-tuple-str-in-python.html)
## 2.Python矩阵转置方法(二维列表行列互换) ##
有列表如下：
```python
matrix = [[1, 2, 3, 4], [5, 6, 7, 8], [9, 10, 11, 12]]
```
转置（行列互换）后的结果如下：
```python
[[1, 5, 9], [2, 6, 10], [3, 7, 11], [4, 8, 12]]
```
### 方法一：嵌套的列表推导式 ###
```python
>>> matrix = [[1, 2, 3, 4], [5, 6, 7, 8], [9, 10, 11, 12]]
>>> [[row[col] for row in matrix] for col in range(len(matrix[0]))]
[[1, 5, 9], [2, 6, 10], [3, 7, 11], [4, 8, 12]]
>>> 
```
原理很简单：先循环列，在固定列上循环每一行。
### 方法二：zip迭代 + map映射 ###
在Python2中：
```python
>>> matrix = [[1, 2, 3, 4], [5, 6, 7, 8], [9, 10, 11, 12]]
>>> map(list, zip(*matrix))
[[1, 5, 9], [2, 6, 10], [3, 7, 11], [4, 8, 12]]
>>> 
```
如在Python3下，map函数返回的是迭代器不是列表，将结果用list函数构造成列表：
```python
>>> matrix = [[1, 2, 3, 4], [5, 6, 7, 8], [9, 10, 11, 12]]
>>> list(map(list, zip(*matrix)))
[[1, 5, 9], [2, 6, 10], [3, 7, 11], [4, 8, 12]]
>>> 
```
原理也很清晰：先用zip并行迭代每一个列表元素，然后再用map将结果中的元组转成列表。

原文参考：[Python矩阵转置方法(二维列表行列互换)](http://www.revotu.com/matrix-transpose-in-python.html)