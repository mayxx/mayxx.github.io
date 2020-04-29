### python 笔记 

##字典
python 3.5 之前，
注意，即便遍历字典时，键-值对 的返回顺序也与存储顺序不同。Python 不关心 键-值对 的存储顺序，而只跟踪键和值之间的关联关系。

Starting in version 3.5 Python will preserve the order of keyword arguments as passed to a function. To accomplish this the collected kwargs will now be an OrderedDict rather than a dict.

This will apply only to functions for which the definition uses the **kwargs syntax for collecting otherwise unspecified keyword arguments. Only the order of those keyword arguments will be preserved.

##python学习--import sys模块
https://blog.csdn.net/u013203733/article/details/72540075
当Python执行import sys语句的时候，它在sys.path变量中所列目录中寻找sys.py模块。如果找到了这个文件，这个模块的主块中的语句将被运行，然后这个模块将能够被你 使用 。注意，初始化过程仅在我们 第一次 输入模块的时候进行。另外，“sys”是“system”的缩写。




Sys模块函数之多，我只能选取自己认为比较实用的一些函数列在此处。借马云找员工的说法,”找最合适的而不是最天才的”，这句话，我个人觉得在很多方面都能适应，学习也不在话下。Sys模块功能的确很多，但我们应该将重点放在那些功能才是最适合我们的，为此，我列的这些函数，就是我认为比较适合我以后开发的函数。

(1)sys.argv
很多人会想，我如何给我的程序在外部传递参数呢？这个，就可以实现。如：
Tesy.py

Import sys
Print sys.argv[number]

一般情况下，number为0是这个脚本的名字，1，2…则为命令行下传递的参数.如：
Test.py脚本内容：
import sys
 
print sys.argv[0]
print sys.argv[1]
print sys.argv[2]
print sys.argv[3]
那么
[root@databak scripts]# python test.py arg1 arg2 arg3
test.py
arg1
arg2
arg3
看到，对应的关系了吗？
sys模块中的argv变量通过使用点号指明——sys.argv——这种方法的一个优势是这个名称不会与任何在你的程序中使用的argv变量冲突。另外，它也清晰地表明了这个名称是sys模块的一部分。

sys.argv变量是一个字符串的 列表 （列表会在后面的章节详细解释）。特别地，sys.argv包含了 命令行参数 的列表，即使用命令行传递给你的程序的参数。

这里，当我们执行python using_sys.py we are arguments的时候，我们使用python命令运行using_sys.py模块，后面跟着的内容被作为参数传递给程序。Python为我们把它存储在sys.argv变量中。

记住，脚本的名称总是sys.argv列表的第一个参数。所以，在这里，'using_sys.py'是sys.argv[0]、'we'是sys.argv[1]、'are'是sys.argv[2]以及'arguments'是sys.argv[3]。注意，Python从0开始计数，而非从1开始。


(2)sys.platform
大家都知道，当今的程序比较流行的是跨平台。简单的说就是这段程序既可以在windows下，换到linux下也可以不加修改的运行起来，听起来就不错。所以，这个函数就可以派上用场了。
假设，我们想实现一个清除终端，linux下用clear, windows下用cls
Ostype=sys.platform()
If ostype==”linux” or ostype==”linux2”:
Cmd=”clear”
Else:
  Cmd=”cls”

(3) sys.exit(n)
执行至主程序的末尾时,解释器会自动退出. 但是如果需要中途退出程序, 你可以调用sys.exit 函数, 它带有一个可选的整数参数返回给调用它的程序. 这意味着你可以在主程序中捕获对sys.exit 的调用。（注：0是正常退出，其他为不正常，可抛异常事件供捕获!）
sys.exit从python程序中退出，将会产生一个systemExit异常，可以为此做些清除除理的工作。这个可选参数默认正常退出状态是0，以数值为参数的范围为：0-127。其他的数值为非正常退出，还有另一种类型，在这里展现的是strings对象类型。



(4)sys.path
大家对模块都有一定了解吧？大家在使用模块的某一个功能前，是不是需要导入呢？答案是需要。那import,__import__命令就不用提干嘛的了吧。那大家在执行import module_name的时候，python内部发生了什么呢？简单的说，就是搜索module_name。根据sys.path的路径来搜索module.name
>>> sys.path
['', '/usr/local/lib/python24.zip', '/usr/local/lib/python2.4', '/usr/local/lib/python2.4/plat-freebsd4', '/usr/local/lib/python2.4/lib-tk', '/usr/local/lib/python2.4/lib-dynload', '/usr/local/lib/python2.4/site-packages']
大家以后写好的模块就可以放到上面的某一个目录下，便可以正确搜索到了。当然大家也可以添加自己的模块路径。Sys.path.append(“mine module path”).

sys.path包含输入模块的目录名列表。我们可以观察到sys.path的第一个字符串是空的——这个空的字符串表示当前目录也是sys.path的一部分，这与PYTHONPATH环境变量是相同的。这意味着你可以直接输入位于当前目录的模块。否则，你得把你的模块放在sys.path所列的目录之一。首先，我们利用import语句 输入 sys模块。基本上，这句语句告诉Python，我们想要使用这个模块。sys模块包含了与Python解释器和它的环境有关的函数。



(5)sys.modules
This is a dictionary that maps module names to modules which have already been loaded. This can be manipulated to force reloading of modules and other tricks.
Python.org手册里已经说的很明白了。
For names in sys.modules.keys():
If names != ’sys’:
    ……
(6)sys.stdin,sys.stdout,sys.stderr
stdin , stdout , 以及stderr 变量包含与标准I/O 流对应的流对象. 如果需要更好地控制输出,而print 不能满足你的要求, 它们就是你所需要的. 你也可以替换它们, 这时候你就可以重定向输出和输入到其它设备( device ), 或者以非标准的方式处理它们


当Python执行import sys语句的时候，它在sys.path变量中所列目录中寻找sys.py模块。如果找到了这个文件，这个模块的主块中的语句将被运行，然后这个模块将能够被你 使用 。注意，初始化过程仅在我们 第一次 输入模块的时候进行。另外，“sys”是“system”的缩写。





sys模块中的argv变量通过使用点号指明——sys.argv——这种方法的一个优势是这个名称不会与任何在你的程序中使用的argv变量冲突。另外，它也清晰地表明了这个名称是sys模块的一部分。


sys.argv变量是一个字符串的 列表 （列表会在后面的章节详细解释）。特别地，sys.argv包含了 命令行参数 的列表，即使用命令行传递给你的程序的参数。


如果你使用IDE编写运行这些程序，请在菜单里寻找一个指定程序的命令行参数的方法。


这里，当我们执行python using_sys.py we are arguments的时候，我们使用python命令运行using_sys.py模块，后面跟着的内容被作为参数传递给程序。Python为我们把它存储在sys.argv变量中。


记住，脚本的名称总是sys.argv列表的第一个参数。所以，在这里，'using_sys.py'是sys.argv[0]、'we'是sys.argv[1]、'are'是sys.argv[2]以及'arguments'是sys.argv[3]。注意，Python从0开始计数，而非从1开始。


sys.path包含输入模块的目录名列表。我们可以观察到sys.path的第一个字符串是空的——这个空的字符串表示当前目录也是sys.path的一部分，这与PYTHONPATH环境变量是相同的。这意味着你可以直接输入位于当前目录的模块。否则，你得把你的模块放在sys.path所列的目录之一。
————————————————
版权声明：本文为CSDN博主「端午过后的猪」的原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/u013203733/article/details/72540075


##Python  列表list中pop()、remove()、 del()
1. pop(index) 是按索引号来删除列表中对应的元素，并返回该元素。

该函数的参数是索引号，也可以是空的，即pop(), 这时将最后一个元素删除。

>>> listA = ['a', 'b', 'c','a', 'b', 'c', 'a', 'b','c']
>>> w = listA.pop(3)
>>> w
'a'
>>> print(listA)
['a', 'b', 'c', 'b', 'c', 'a', 'b', 'c']
2. remove(参数) 是根据参数在列表中查找，若找到某个元素的值和参数相等，则将该元素删除，若没有找到，则抛出异常，该函数的参数不能为空，函数没有返回值。

>>> listA = ['a', 'b', 'c','a', 'b', 'c', 'a', 'b','c']
>>> w = listA.remove('a')
>>> print(w)
None
>>> print(listA)
['b', 'c', 'a', 'b', 'c', 'a', 'b', 'c']
3.del函数用于字符串的删除操作。

>>> del listA[1]
>>> print(listA)
['a', 'c', 'a', 'b', 'c', 'a', 'b', 'c']
>>> del listA[1:4]
>>> print(listA)
['a', 'c', 'a', 'b', 'c']
>>> del listA
>>> id(listA)
Traceback (most recent call last):
  File "<pyshell#6>", line 1, in <module>
    id(listA)
NameError: name 'listA' is not defined
 

##Python3 字典 pop() 方法

描述
Python 字典 pop() 方法删除字典给定键 key 所对应的值，返回值为被删除的值。key值必须给出。 否则，返回default值。

语法
pop()方法语法：

pop(key[,default])
#参数
key: 要删除的键值
default: 如果没有 key，返回 default 值
#返回值
返回被删除的值。

#实例
以下实例展示了 pop() 方法的使用方法：

>>> site= {'name': '菜鸟教程', 'alexa': 10000, 'url': 'www.runoob.com'}
>>> pop_obj=site.pop('name')
>>> print(pop_obj)
菜鸟教程


##Python Set pop() 方法
Python3 列表 Python 集合

描述
pop() 方法用于随机移除一个元素。

语法
pop() 方法语法：

set.pop()
#参数
无
#返回值
返回移除的元素。

#实例
随机移除一个元素：

实例 1
fruits = {"apple", "banana", "cherry"}
 
fruits.pop() 
 
print(fruits)
输出结果为：

{'apple', 'banana'}
输出返回值：

实例 1
fruits = {"apple", "banana", "cherry"}
 
x = fruits.pop() 
 
print(x)
输出结果为：

banana


##python 装饰器
##装饰器是用来给函数增加新功能的，对于支持高阶函数的语言，函数参数直接穿进去就好了。但是Python提供了更为优雅的解决方案，只需要一个@就能搞定。

装饰器函数需要单独写出来，两层，第一层接受一个函数function就可以了，第二层构造一个函数来接受function的参数然后再内部完成需要添加的功能并且正确调用函数，然后在第一层里返回第二层构造的这个函数。例如写好了一个很蛋疼的代码之后想测测时间……

# 这是 python2 的例子    encoding: utf-8
 
import time
 
def timer(function):
    def decorator(*args,**kwargs):
        start=time.time()
        Return=function(*args,**kwargs)
        print 'cost %s'%(time.time()-start)
        return Return
    return decorator
 
@timer
def mul(row,column):
    for i in xrange(row):
        for j in xrange(column):
            print i,j,i*j
 
if __name__=='__main__':
    mul(100,100)
运行结果显而易见：
99 96 9504
99 97 9603
99 98 9702
99 99 9801
cost 0.34299993515
这种直接在内部构造函数，然后将函数返回的做法，返回得到的函数具有自己的参数列表，所以也就构成了从内向外展开的结构。
然后就是在这种记忆化用法，最典型的就是那个递归写法的斐波拉契，用装饰器造一个缓存搞搞就行了……

# encoding: utf-8
 
import time
 
def memorize(function):
    Return={}
    def decorator(*args):
        if args not in Return:
            print args
            Return[args]=function(*args)
        return Return[args]
    return decorator
 
@memorize
def fib(n):
    if n==0:
        return 1
    elif n==1:
        return 1
    else:
        return fib(n-1)+fib(n-2)
    
def timer(function):
    def decorator(*args,**kwargs):
        start=time.time()
        Return=function(*args,**kwargs)
        print 'cost %s'%(time.time()-start)
        return Return
    return decorator
 
@timer
def cal(n):
    return fib(n)
 
if __name__ == '__main__':
    cal(100)
    cal(100)
可以注意到这几个问题：
缓存是全局有效的，这个字典会一直存在，以后再次调用也是一样从里面读取数据。这也同样带来一个问题，一个缓存装饰器只能给一个函数用，不然会混淆。
装饰器是在每次调用这个函数的时候进入，对于测时间这种我只想要一个最后结果的东西，是不是还是需要手动用另外一个函数启动递归然后装饰这个函数？
————————————————
版权声明：本文为CSDN博主「Speedcell」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/speedcell4/article/details/18373289

python装饰器–原来如此简单
今天整理装饰器，内嵌的装饰器、让装饰器带参数等多种形式，非常复杂，让人头疼不已。但是突然间发现了装饰器的奥秘，原来如此简单。。。。

第一步 ：从最简单的例子开始
# -*- coding:gbk -*-
'''示例1: 使用语法糖@来装饰函数，相当于“myfunc = deco(myfunc)”
但发现新函数只在第一次被调用，且原函数多调用了一次'''

def deco(func):
    print("before myfunc() called.")
    func()
    print("  after myfunc() called.")
    return func

@deco
def myfunc():
    print(" myfunc() called.")

myfunc()
myfunc()

这是一个最简单的装饰器的例子，但是这里有一个问题，就是当我们两次调用myfunc()的时候，发现装饰器函数只被调用了一次。为什么会这样呢？要解释这个就要给出破解装饰器的关键钥匙了。
这里@deco这一句，和myfunc = deco(myfunc)其实是完全等价的，只不过是换了一种写法而已
一定要记住上面这句！！！！
好了，从现在开始，只需要做替换操作就可以了。
将@deco 替换为 myfunc = deco(myfunc)
程序首先调用deco(myfunc)，得到的返回结果赋值给了myfunc （注意：在Python中函数名只是个指向函数首地址的函数指针而已）
而deco(myfunc)的返回值就是函数myfunc()的地址
这样其实myfunc 没有变化，也就是说，最后的两次myfunc()函数调用，其实都没有执行到deco()。
有同学就问了，明明打印了deco()函数里面的内容啊，怎么说没有调用到呢。这位同学一看就是没有注意听讲，那一次打印是在@deco 这一句被执行的。大家亲自动手试一下就会发现” myfunc() called.” 这句打印输出了三次。多的那次就是@deco这里输出的，因为@deco 等价于myfunc = deco(myfunc)，这里已经调用了deco()函数了。

第二步 ：确保装饰器被调用
怎么解决装饰器没有被调用的问题呢

# -*- coding:gbk -*-
'''示例2: 使用内嵌包装函数来确保每次新函数都被调用，
内嵌包装函数的形参和返回值与原函数相同，装饰函数返回内嵌包装函数对象'''

def deco(func):
    def _deco():
        print("before myfunc() called.")
        func()
        print("  after myfunc() called.")
        # 不需要返回func，实际上应返回原函数的返回值
    return _deco

@deco
def myfunc():
    print(" myfunc() called.")
    return 'ok'

myfunc()
myfunc()

这里其实不需要我解释了，还是按照第一步中的方法做替换就可以了。还是啰嗦几句吧。。
@deco 替换为 myfunc = deco(myfunc)
程序首先调用deco(myfunc)，得到的返回结果赋值给了myfunc ，这样myfunc 就变成了指向函数_deco()的指针
以后的myfunc()，其实是调用_deco()

第三步 ：对带参数的函数进行装饰
破案过程和第一步、第二步完全一致，不再重复了

# -*- coding:gbk -*-
'''示例5: 对带参数的函数进行装饰，
内嵌包装函数的形参和返回值与原函数相同，装饰函数返回内嵌包装函数对象'''

def deco(func):
    def _deco(a, b):
        print("before myfunc() called.")
        ret = func(a, b)
        print("  after myfunc() called. result: %s" % ret)
        return ret
    return _deco

@deco
def myfunc(a, b):
    print(" myfunc(%s,%s) called." % (a, b))
    return a + b

myfunc(1, 2)
myfunc(3, 4)

第四步 ：让装饰器带参数
# -*- coding:gbk -*-
'''示例7: 在示例4的基础上，让装饰器带参数，
和上一示例相比在外层多了一层包装。
装饰函数名实际上应更有意义些'''

def deco(arg):
    def _deco(func):
        def __deco():
            print("before %s called [%s]." % (func.__name__, arg))
            func()
            print("  after %s called [%s]." % (func.__name__, arg))
        return __deco
    return _deco

@deco("mymodule")
def myfunc():
    print(" myfunc() called.")

@deco("module2")
def myfunc2():
    print(" myfunc2() called.")

myfunc()
myfunc2()

这种带参数的装饰器怎么解释呢。其实是一样的，还是我们的替换操作
@deco(“mymodule”)替换为myfunc = deco(“mymodule”)(myfunc )
注意啊，这里deco后面跟了两个括号。
有同学要问了，这是什么意思？
其实很简单，先执行deco(“mymodule”)，返回结果为_deco
再执行_deco(myfunc)，得到的返回结果为__deco
所以myfunc = __deco

破案！
————————————————
版权声明：本文为CSDN博主「卢纯清」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/u013858731/article/details/54971762


##13 python3 中使用map函数返回相应的列表（python2和3返回结果不同的问题）

NewGuy_Theasia 2018-08-11 13:47:15  1206  收藏 1
展开
map()是 Python 内置的高阶函数，它接收一个函数 f 和一个 list，并通过把函数 f 依次作用在 list 的每个元素上，得到一个新的 list 并返回。

例如：将列表中的数据都平方

def f(x):
    return x*x
print  map(f, [1, 2, 3,])

python2 输出

[1, 4, 9,]

python3输出

<map object at 0x0000022E1412A080>

python3中使用map函数与python2中使用map函数返回的内容不一致
使用python3的代码调用map函数发现返回的并不是列表，而是这样的

<map object at 0x000002A56FDDA048>

为了让他显示正常，我到网上查找发现有大神解决了这个问题,使用list转换成列表既可以显示正常
如下：

def f(x):
    return x*x
print  (list(map(f, [1, 2, 3,])))

输出：

[1, 4, 9,]

例2：将list1中的数据转换成整型数据

 def  f(x):
     x = int(x)
     return x
list1= ['1','2','3']
print('原列表为字符串:',list1)
list2 =  map(f,list1)
print('新列表为整型数据:',list(list2))
————————————————
版权声明：本文为CSDN博主「NewGuy_Theasia」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/qq_42397914/article/details/81586060


##Python2.x 和 Python3.x 中 raw_input( ) 和 input( ) 区别
1、在 Python2.x 中 raw_input( ) 和 input( )，两个函数都存在，其中区别:
raw_input( ) 将所有输入作为字符串看待，返回字符串类型。
input( ) 只能接收"数字"的输入，在对待纯数字输入时具有自己的特性，它返回所输入的数字的类型（ int, float ）。
2、在 Python3.x 中 raw_input( ) 和 input( ) 进行了整合，去除了 raw_input( )，仅保留了 input( ) 函数，其接收任意任性输入，将所有输入默认为字符串处理，并返回字符串类型。


##Python map() 函数
Python 内置函数 
描述
map() 会根据提供的函数对指定序列做映射。

第一个参数 function 以参数序列中的每一个元素调用 function 函数，返回包含每次 function 函数返回值的新列表。

语法
map() 函数语法：

map(function, iterable, ...)
参数
function -- 函数
iterable -- 一个或多个序列
返回值
Python 2.x 返回列表。

Python 3.x 返回迭代器。

实例
以下实例展示了 map() 的使用方法：

>>>def square(x) :            # 计算平方数
...     return x ** 2
... 
>>> map(square, [1,2,3,4,5])   # 计算列表各个元素的平方
[1, 4, 9, 16, 25]
>>> map(lambda x: x ** 2, [1, 2, 3, 4, 5])  # 使用 lambda 匿名函数
[1, 4, 9, 16, 25]
 
# 提供了两个列表，对相同位置的列表数据进行相加
>>> map(lambda x, y: x + y, [1, 3, 5, 7, 9], [2, 4, 6, 8, 10])
[3, 7, 11, 15, 19]


##Python eval() 函数
Python 内置函数 

描述
eval() 函数用来执行一个字符串表达式，并返回表达式的值。

语法
以下是 eval() 方法的语法:

eval(expression[, globals[, locals]])
参数
expression -- 表达式。
globals -- 变量作用域，全局命名空间，如果被提供，则必须是一个字典对象。
locals -- 变量作用域，局部命名空间，如果被提供，可以是任何映射对象。
返回值
返回表达式计算结果。

实例
以下展示了使用 eval() 方法的实例：

>>>x = 7
>>> eval( '3 * x' )
21
>>> eval('pow(2,2)')
4
>>> eval('2 + 2')
4
>>> n=81
>>> eval("n + 4")
85


##Python3 zip() 函数
Python3 内置函数 

描述
zip() 函数用于将可迭代的对象作为参数，将对象中对应的元素打包成一个个元组，然后返回由这些元组组成的对象，这样做的好处是节约了不少的内存。

我们可以使用 list() 转换来输出列表。

如果各个迭代器的元素个数不一致，则返回列表长度与最短的对象相同，利用 * 号操作符，可以将元组解压为列表。

zip 方法在 Python 2 和 Python 3 中的不同：在 Python 2.x zip() 返回的是一个列表。

如果需要了解 Pyhton2 的应用，可以参考 Python zip()。

语法
zip 语法：

zip([iterable, ...])
参数说明：

iterabl -- 一个或多个迭代器;
返回值
返回一个对象。

实例
以下实例展示了 zip 的使用方法：

>>>a = [1,2,3]
>>> b = [4,5,6]
>>> c = [4,5,6,7,8]
>>> zipped = zip(a,b)     # 返回一个对象
>>> zipped
<zip object at 0x103abc288>
>>> list(zipped)  # list() 转换为列表
[(1, 4), (2, 5), (3, 6)]
>>> list(zip(a,c))              # 元素个数与最短的列表一致
[(1, 4), (2, 5), (3, 6)]
 
>>> a1, a2 = zip(*zip(a,b))          # 与 zip 相反，zip(*) 可理解为解压，返回二维矩阵式
>>> list(a1)
[1, 2, 3]
>>> list(a2)
[4, 5, 6]
>>>

##Python3 tuple 函数
Python3 内置函数 

描述
tuple 函数将可迭代系列（如列表）转换为元组。

语法
以下是 tuple 的语法:

tuple( iterable )
参数
iterable -- 要转换为元组的可迭代序列。
返回值
返回元组。

实例
以下展示了使用 tuple 的实例：

实例
>>>list1= ['Google', 'Taobao', 'Runoob', 'Baidu']
>>> tuple1=tuple(list1)
>>> tuple1
('Google', 'Taobao', 'Runoob', 'Baidu')
Python3 内置函数 Python3 内置函数


##print() 函数默认“在输出结尾自动包含换行”，而添加 end=’ ’ 参数可以在输出末尾添加空字符，就不会再自动添加一个换行符
这个只有 Python3 有用，Python2 不支持。如下所示：

str = 'abcdefg'
for word in str:
    #print(word) # a/n b/n c/n d/n e/n f/n g/n
    print(each,end='') #输出abcdefg end=参数不设置，默认为末尾换行/n，end=''末尾为
————————————————
版权声明：本文为CSDN博主「sunzq55」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/weixin_41474364/article/details/96314960



##迭代器
简介：迭代器是python里面可以记住遍历位置的对象，迭代器只能往前不能往后，使用iter()创建一个迭代器，使用next()返回一个迭代器里面的元素。
应用场景：数列的数据规模巨大，或者数列有规律，但是通过列表推导式推导不出来
#!/usr/local/bin/python3
  import sys
  it = iter([1,32,43,2])
  while True:
           try:
                  print(next(it))
           except StopIteration:
                   sys.exit()
迭代器协议
迭代器协议是使用__next__()和__iter__()实现的


##生成器
简介：在python里面使用了yield的函数称为生成器，生成器返回一个迭代器，在调用生成器运行的过程中，每次遇到 yield 时函数会暂停并保存当前所有的运行信息，返回 yield 的值, 并在下一次执行 next() 方法时从当前位置继续运行。调用一个生成器函数，返回的是一个迭代器对象
应用场景：

列表所有数据都在内存中，如果有海量数据的话将会非常耗内存。
如：仅仅需要访问前面几个元素，那后面绝大多数元素占用的空间都白白浪费了。
在Python中，这种一边循环一边计算的机制，称为生成器：generator
generator保存的是算法，每次调用next(g)，就计算出g的下一个元素的值，直到计算到最后一个元素，没有更多的元素时，抛出StopIteration的错误。
简单一句话：我又想要得到庞大的数据，又想让它占用空间少，那就用生成器
>>> g = (x * x for x in range(10))
>>> g
<generator object <genexpr> at 0x1022ef630>
1
2
3
#!/usr/bin/python3
 
import sys
 
def fibonacci(n): # 生成器函数 - 斐波那契
    a, b, counter = 0, 1, 0
    while True:
        if (counter > n): 
            return
        yield a
        a, b = b, a + b
        counter += 1
f = fibonacci(10) # f 是一个迭代器，由生成器返回生成
 
while True:
    try:
        print (next(f), end=" ")
    except StopIteration:
        sys.exit()


##装饰器
函数也是变量，我们那些普通的变量，比如定义x=1的时候，我们1会实实在在地存在内存里面，然后把x指向1，当在赋值x=y的时候，就把y也指向1了。当我们使用del去删除x和y的时候，那么就没有变量指向1这个内存地址了，这个1就会被Python解释器回收掉，那么如果没有被删的话，它会不会被回收呢，答案是不会，除非程序运行结束了，如果没有被删的话，它会一直贮存在内存里面，不会被回收，只要这个x变量存在，它就永远不会被删除，因为x已经用了这个内存了，就是说1是有人用了的，也就是其实他内存里面有个计数器，它每隔多长时间，就(相当于)刷新一下，看哪些没有被引用就把它清除，直到程序结束就都清空了，我们del的时候是吧x这个引用摘掉了，但那个1还在内存里面，然后Python垃圾回收发现这个1哎它没有引用，就把它删掉。
装饰器对被装饰函数是完全透明的，也就是说，装饰器不会对要加功能的函数的源代码进行修改，而且也不会改变函数的调用方式。
装饰器其实就是使用了嵌套函数和高阶函数的知识，可以看本博的装饰器进阶的部分，都嵌套两层了
简介：装饰器本质上就是一个函数，它用来给别的函数增加功能。装饰器可以在代码运行期间动态地增加函数的功能，当我们想要给多个函数增加相同的功能，一个一个地区修改这些函数效率很低，而且代码混乱，我们可以采用装饰器

=	简单的赋值运算符	c = a + b 将 a + b 的运算结果赋值为 c
+=	加法赋值运算符	c += a 等效于 c = c + a
-=	减法赋值运算符	c -= a 等效于 c = c - a
*=	乘法赋值运算符	c *= a 等效于 c = c * a
/=	除法赋值运算符	c /= a 等效于 c = c / a
%=	取模赋值运算符	c %= a 等效于 c = c % a
**=	幂赋值运算符	c **= a 等效于 c = c ** a
//=	取整除赋值运算符	c //= a 等效于 c = c // a
没有 ++ --

##数字运算
运算会根据结果自动判断结果是int还是float
用到除法的时候，结果自动输出为float
双斜杠//得到的结果是int
取模(余数)还是%
赋值 =
多次方 2**7 2的7次方
完全支持浮点型和整型混合运算
最后一个值会被被赋给变量_,
保留小数点,如保留2位round(num,2)