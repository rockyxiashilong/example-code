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

1.一致性的感念理解：python中的一切都是对象，对象的基类是object，提供了一些包含类似__len__de 用法，当用户调用len(obj)时，其实调用的是obj.__len_()方法
主要包含的pythonic方法，算术运算符、__getitem__;__setitem__支持索引和切片；__get__;__set__用于属性管理；__init__、__new__用于进行类的初始化管理

2.生成器和迭代器[]{}()中不需要用转义符进行换行，列表推导式生成的是一个列表，生成器生成的是一个生成器对象，更省内存，需要的时候才生成元素，都实现了__iter__方法，可迭代对象都支持拆包操作，即支持for循环拆包和赋值拆包

3.列表按数据是否连续存放可以分成扁平化列表和非扁平化列表，例如list、tuple都是非扁平化列表，str和byte都是扁平化列表；依据是否支持__setitem__,可以分成可变列表（list、dict）和不可变（tuple、str）

4.还可以用 * 运算符把一个可迭代对象拆开作为函数的参数：
  >>> divmod(20, 8) 
  (2, 4) 
  >>> t = (20, 8) 
  >>> divmod(*t) 
  (2, 4) 
  >>> quotient, remainder = divmod(*t) 
  >>> quotient, remainder 
  (2, 4)
