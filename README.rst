Fluent Python: example code
===========================

Example code for the book `Fluent Python`_ by Luciano Ramalho (O'Reilly, 2014).

   **BEWARE**: This is a work in progress, like the book itself.

* Code here may change and disappear without warning. 

* If a piece of code is not yet in the ebook, it's likely to be broken.

* A major reorganization may happen when the last chapter is done. 

* No promises. No guarantees. Use at own risk.

.. _Fluent Python: http://shop.oreilly.com/product/0636920032519.do 


学习笔记
第1-2章
1.一致性的感念理解：python中的一切都是对象，对象的基类是object，提供了一些包含类似__len__de 用法，当用户调用len(obj)时，其实调用的是obj.__len_()方法
主要包含的pythonic方法，算术运算符、__getitem__;__setitem__支持索引和切片；__get__;__set__用于属性管理；__init__、__new__用于进行类的初始化管理

第3章 容器类型
2.生成器和迭代器[]{}()中不需要用转义符进行换行，列表推导式生成的是一个列表，生成器生成的是一个生成器对象，更省内存，需要的时候才生成元素，都实现了__iter__方法，可迭代对象都支持拆包操作，即支持for循环拆包和赋值拆包

3.列表按数据是否连续存放可以分成扁平化列表和非扁平化列表，例如list、tuple都是非扁平化列表，str和byte都是扁平化列表；依据是否支持__setitem__,可以分成可变列表（list、dict）和不可变（tuple、str）

4.还可以用 * 运算符把一个可迭代对象拆开作为函数的参数page64+：
  >>> divmod(20, 8) 
  (2, 4) 
  >>> t = (20, 8) 
  >>> divmod(*t) 
  (2, 4) 
  >>> quotient, remainder = divmod(*t) 
  >>> quotient, remainder 
  (2, 4)
5.序列支持切片操作，支持切片赋值操作，切片赋值操作的右值必须是一个可以迭代的对象，序列操作的+、*操作符都会产生一个新的序列对象， += 、*= 操作才会
就地返回。
  >>> l = list(range(10)) 
  >>> l 
  [0, 1, 2, 3, 4, 5, 6, 7, 8, 9] 
  >>> l[2:5] = [20, 30] 
  >>> l 
  [0, 1, 20, 30, 5, 6, 7, 8, 9] 
  >>> del l[5:7] 
  >>> l 
  [0, 1, 20, 30, 5, 8, 9] 
  >>> 
  l[3::2] = [11, 22] 
  >>> l 
  [0, 1, 20, 11, 5, 22, 9] 
  >>> l[2:5] = 100  ➊ 
  Traceback (most recent call last):  File "<stdin>", line 1, in <module> TypeError: can only assign an iterable 
  >>> l[2:5] = [100] 
  >>> l 
  [0, 1, 100, 22, 9]
  
  6.如果一个函数或者方法对对象进行的是就地改动，那它就应该返回 None，好让调用者知道传入的参数发生了变动，而且并未产生新的对象
  
  7.collections.abc 模块中有 Mapping 和 MutableMapping 这两个 抽象基类,定义了字段的接口
  
  8.字典推导{}
     >>> b = {key:value for key,value in (("one",1),("two",2))}
    >>> b
    {'one': 1, 'two': 2}
    
 9.dict、collections.defaultdict和 collections.OrderedDict
 
 10.d[key] 和d.get(key)的主要区别 前者key不存在会返回KeyError，后者会返回default或者None
 
 11.__missing__ 方法，当__getitem__方法找不到key时，返回会调用该方法再进行一次处理
 
 12.collections.OrderedDict 有序字典   collections.ChainMap 多个字段的组合    collections.Counter  计数字典，初始化时传入一个可迭代对象，
 构造出一个key 为迭代对象，值为对应key出现次数的字典   colllections.UserDict 抽象类，用于继承和实现
 
 13、不可变对象MappingProxyTyp
   >>> from types import MappingProxyType 
   >>> d = {1:'A'} 
   >>> d_proxy = MappingProxyType(d) 
   >>> d_proxy mappingproxy({1: 'A'}

