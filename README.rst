Fluent Python: example code
.. _Fluent Python: http://shop.oreilly.com/product/0636920032519.do 


 1.从upstream（远程仓库） fork 一个个人仓库     例如：https://github.com/rockyxiashilong/WeEvent.git
 
 2.本地 git clone https://github.com/rockyxiashilong/WeEvent.git  
        $ git remote -v      //克隆成功后，查看远程仓库，看到如下个人仓库
        origin  https://github.com/rockyxiashilong/WeEvent.git (fetch)
        origin  https://github.com/rockyxiashilong/WeEvent.git (push)

 
 3.添加远程仓库  git remote add upstream https://github.com/WeBankFinTech/WeEvent.git
    $ git remote -v 
    origin  https://github.com/rockyxiashilong/WeEvent.git (fetch)
    origin  https://github.com/rockyxiashilong/WeEvent.git (push)
    upstream        https://github.com/WeBankFinTech/WeEvent.git (fetch)
    upstream        https://github.com/WeBankFinTech/WeEvent.git (push)
    
4.更新远程仓库  git fetch upstream 
5.然后合入本地master     git rebase
    git log -3 查看最新三次提交，看看本地仓库是不是已经是最新的代码了
6.创建分支   git checkout -b add_testcase

7.修改代码后，提交本地分支到个人远程仓，然后提交pr请求合入主仓库
git push --set-upstream origin add_testcase 

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
   
14.set对象可以理解为去重的可迭代对象，可以直接字面值初始化、也可以用一个可以迭代的对象进行初始化。
    >>> a = {1,2,3,4}
    >>> a
    set([1, 2, 3, 4])
    >>> b = set([1,2,3,4,5,1,2,3])
    >>> b
    set([1, 2, 3, 4, 5])
    
15.dict对象为啥可以实现O(1)算法的数据查找，采用的是散列算法，d[key]时先算出hash(key),然后找到散列对象后，会调用__eq__方法，进行比较，看是否相等。


第四章 文本和字节序列
    ---人类使用文本，计算机使用字节序列

16 bytes  array.arrary struct     utf-8 utf-16 编码格式和解码格式需要保持一致，其中windows中文的默认编码格式是产cp1252，unix编码格式utf-8，windows读写文件时，最好指定编码集，防止出现乱码。 

第五章

1.map filter 高阶函数都有替代方案，可以用列表生成式来替代；高阶函数是指参数可以为函数对象或者返回值为函数对象的函数

2.匿名函数 lambda，不好阅读的lambda不建议使用，只是语法糖，完全可以用def函数来处理

3.callable()    一般而言，实例不是可调用对象，除非其实现了__call__方法。
4.函数也是对象，比普通对象多一些属性   __defaults__(返回参数的默认值) __code__   __name__函数名，注意，装饰器会破坏函数的上述对应信息

第6章
使用一等函数实现设计模式
策略模式和命令模式 可以用函数来替代，而不需要使用抽象类来实现


第12章 类和多重继承
12.1 cls.__mro__会显示类的解析顺序，类调用方法时，若无指定用哪个类的方法，会按照解析顺序进行调用。D（B，C）解析顺序中，B再前，C再后，遇到B/C中有同名的函数时，当D类实例调用是会先调用B中的方法。

12.2 设计方法
  1.把接口和实现继承区分开
  使用多重继承时，一定要明确一开始为什么创建子类。主要原因可 能有：
  继承接口，创建子类型，实现“是什么”关系
  继承实现，通过重用避免代码重复
  其实这两条经常同时出现，不过只要可能，一定要明确意图。通过 继承重用代码是实现细节，通常可以换用组合和委托模式。而接口 继承则是框架的支柱
  
  2.使用抽象基类显式表示接口
   现代的 Python 中，如果类的作用是定义接口，应该明确把它定义为 抽象基类。
   Python 3.4 及以上的版本中，我们要创建 abc.ABC 或其 他抽象基类的子类（如果想支持较旧的 Python 版本，参见 11.7.1 节）
   
 3.通过混入重用代码
  如果一个类的作用是为多个不相关的子类提供方法实现，从而实现重用，但不体现“是什么”关系，应该把那个类明确地定义为混入类（mixin class）。
  从概念上讲，混入不定义新类型，只是打包方法，便于重用。
  混入类绝对不能实例化，而且具体类不能只继承混入类。
  混入类应该提供某方面的特定行为，只实现少量关系非常紧 密的方法
  
 4.在名称中明确指明混入
 因为在 Python 中没有把类声明为混入的正规方式，所以强烈推荐在 名称中加入 ...Mixin 后缀。
 Tkinter 没有采纳这个建议，如果采 纳的话，XView 会变成 XViewMixin，Pack 会变成 PackMixin，图 12-3 中所有使用 «mixin» 标记的类都应该这么 做。
 
 5.抽象基类可以作为混入，反过来则不成立
   抽象基类可以实现具体方法，因此也可以作为混入使用。不过，抽 象基类会定义类型，而混入做不到。此外，抽象基类可以作为其他 类的唯一基类，而混入决不能作为唯一的超类，除非继承另一个更 具体的混入——真实的代码很少这样做。
抽象基类有个局限是混入没有的：抽象基类中实现的具体方法只能 与抽象基类及其超类中的方法协作。这表明，抽象基类中的具体方 法只是一种便利措施，因为这些方法所做的一切，用户调用抽象基 类中的其他方法也能做到。

06. 不要子类化多个具体类
   具体类可以没有，或最多只有一个具体超类。 也就是说，具体类 的超类中除了这一个具体超类之外，其余的都是抽象基类或混入。 例如，在下述代码中，如果 Alpha 是具体类，那么 Beta 和 Gamma 必须是抽象基类或混入：
   
07. 为用户提供聚合类
如果抽象基类或混入的组合对客户代码非常有用，那就提供一个 类，使用易于理解的方式把它们结合起来。Grady Booch 把这种类 称为聚合类（aggregate class）。
例如，下面是 tkinter.Widget 类的完整代码 （https://hg.python.org/cpython/file/3.4/Lib/tkinter/__init__.py#l2141）：
class Widget(BaseWidget, Pack, Place, Grid):    
"""Internal class.Base class for a widget which can be positioned with the    geometry managers Pack, Place or Grid."""    
  pass
Widget 类的定义体是空的，但是这个类提供了有用的服务：把四 个超类结合在一起，这样需要创建新小组件的用户无需记住全部混 入，也不用担心声明 class 语句时有没有遵守特定的顺序。 Django 中的 ListView 类是更好的例子，稍后在 12.5 节讨论

08. “优先使用对象组合，而不是类继承” 这句话引自《设计模式：可复用面向对象软件的基础》一书， 这 是我能提供的最佳建议。熟悉继承之后，就太容易过度使用它了。 出于对秩序的诉求，我们喜欢按整洁的层次结构放置物品，程序员 更是乐此不疲。
然而，优先使用组合能让设计更灵活。例如，对 tkinter.Widget 类来说，它可以不从全部几何管理器中继承方 法，而是在小组件实例中维护一个几何管理器引用，然后通过它调 用方法。毕竟，小组件“不是”几何管理器，但是可以通过委托使用 相关的服务。这样，我们可以放心添加新的几何管理器，不必担心
会触动小组件类的层次结构，也不必担心名称冲突。即便是单继 承，这个原则也能提升灵活性，因为子类化是一种紧耦合，而且较 高的继承树容易倒。
组合和委托可以代替混入，把行为提供给不同的类，但是不能取代 接口继承去定义类型层次结构




