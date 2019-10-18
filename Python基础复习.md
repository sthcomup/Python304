### Python基础复习

##### python标准库都有那一些:

os操作系统,time时间,random随机,pymysql连接数据库,threading线程,multiprocessing进程,queue队列

第三方库:

django和flask也是第三方库,requests,virtualenv, selenium, scrapy,xadmin,celery,

re,hashlib,md5

#### 赋值,浅拷贝和深拷贝的区别

* 赋值:

  在python中,对象的赋值就是简单的对象引用, 这点和C++不同,如下:

  ```python
  a = [1,2"hello",['python','C++']]
  b = a
  ```

  在上面示列中,a和b是一样,他们指的是同一片内存,b只不过用了a的别名,是引用

  赋值操作(包括对象作为参数、返回值)不会开辟新的内存空间，它只是复制了对象的引用。也就是 

  说除了 b 这个名字之外，没有其他的内存开销。修改了 a，也就影响了 b，同理，修改了 b，也就影响了a.

* 浅拷贝:

  ```python
  import copy
  a = [1,2,"hello",[4,3]]
  
  # 1.切片操作
  # b = a[:]
  
  # 2.工厂函数
  # b = list(a)
  
  # 3.copy函数
  # b = copy.copy(a)
  
  # 4.意外情况修改a列表中嵌套的list表:
  # a[3].append('jave')
  # b = a[:]
  
  # 5.查看浅拷贝后的里面元素是否是同个内存地址
  b = a[:]
  j = [id(x) for x in a]
  p = [id(x) for x in b]
  
  
  print(id(a))
  print(id(b))
  print(b)
  print(p)
  print(j)
  ```

  从上面的代码可以得到结论是浅拷贝产生的b不在是a列表了,使用id可以确定看见他们不会指定在同一内存地址中,但在(5)的是实例中可以查看里面的元素内存地址是一样的.

* 深拷贝:

  深拷贝只有一种形式,copy中deepcopy()函数.

  深拷贝和浅拷贝对应,深拷贝拷贝了对象的所有元素,包括多层嵌套的元素.因此,它的空间开销和时间开销要高.

  ```python
  import copy
  a = [1,2,"hello",[4,3]]
  a.append('ww')
  b = copy.deepcopy(a)
  
  print(a)
  print(b)
  print(id(a))
  print(id(b))
  ```

  在去修改b列表都不会影响到a列表,即使里有在深的嵌套,也不会有任何影响,因为深拷贝拷贝出来的对象根本就是一个全新的对象,不在与原来的对象产生任何的关联.

  ** 拷贝注意点:

  * 对于非容器类型，如数字、字符，以及其他的“原子”类型，没有拷贝一说，产生的都是原对象的引用。 

    如果元组变量值包含原子类型对象，即使采用了深拷贝，也只能得到浅拷贝。

#### python中的`__init__`和`__new__`的区别:

* init 在对象创建后,对对象进行初始化.
* new 是在对象创建之前创建一个对象,并将该对象返回给init.

#### python 里面如何创建随机数:

创建随机数的模块是random,在使用前需要import

* random.random():生成一个0-1之间的随机浮动数
* random.uniform(a, b)：生成[a,b]之间的浮点数； 
* random.randint(a, b)：生成[a,b]之间的整数； 
* random.randrange(a, b, step)：在指定的集合[a,b)中，以 step 为基数随机取一个数；
* random.choice(sequence)：从特定序列中随机取一个元素，这里的序列可以是字符串,列表,元组等。

#### 说明一下 os.path 和 sys.path 分别代表什么

* os.path 主要是用于对系统路径文件的操作。 

* sys.path 主要是对 Python 解释器的系统环境参数的操作（动态的改变 Python 解释器搜索路径）。

#### Python 中的 os 模块常见方法

* os.remove()删除文件 

* os.rename()重命名文件 

* os.walk()生成目录树下的所有文件名 

* os.chdir()改变目录

#### Python 的 sys 模块常用方法？

* sys.argv 命令行参数 List，第一个元素是程序本身路径 

* sys.modules.keys() 返回所有已经导入的模块列表 

* sys.exc_info() 获取当前正在处理的异常类,exc_type、exc_value、exc_traceback 当前处理的异常详细信息

#### unittest 是什么？

* 在 Python 中，unittest 是 Python 中的单元测试框架。它拥有支持共享搭建、自动测试、在测试中暂停代码、将不同测试迭代成一组，等的功能

#### 模块和包是什么

* 在 Python 中，模块是搭建程序的一种方式。每一个 Python 代码文件都是一个模块，并可以引用其他的模块，比如对象和属性。 
* 一个包含许多 Python 代码的文件夹是一个包。一个包可以包含模块和子文件夹。

### Python 特性

Python 是强类型的动态脚本语言。 

强类型：不允许不同类型相加。 

动态：不使用显示数据类型声明，且确定一个变量的类型是在第一次给它赋值的时候。 

脚本语言：一般也是解释型语言，运行代码只需要一个解释器，不需要编译。 

### 谈一下什么是解释性语言，什么是编译性语言?

* 计算机是不能够理解高级语言的,只能理解机器语言,所有需要将高级语言翻译成机器语言,计算机才能执行高级语言编写的程序.

* 解释性语言在运行程序的时候才会进行翻译
* 编译性语言写的程序之前,需要一个专门的编译过程,把程序编译成机器语言(可执行文件)

#### Python日记

python自带logging模块,调用logging.basicConfig()方法,配置需要的日志等级和相应的参数,python 解释器会按照配置的参数生成相应的日志

#### Python2 与 Python3 的区别

* Python3 对 Unicode 字符的原生支持。

* Python2 中使用 ASCII 码作为默认编码方式导致 string 有两种类型 str 和 unicode，Python3 只支持 unicode 的 string。

* Python3 采用的是绝对路径的方式进行 import。Python2 中相对路径的 import 会导致标准库导入变得困难。Python3 中这一点将被修改，如果还需要导入同一目录的文件必 

  须使用绝对路径，否则只能使用相关导入的方式来进行导入.

* Python2中存在老式类和新式类的区别，Python3统一采用新式类。新式类声明要求继承object,必须用新式类应用多重继承。 

* Python3 使用更加严格的缩进。Python2 的缩进机制中，1 个 tab 和 8 个 space 是等价的，所以在缩进中可以同时允许 tab 和 space 在代码中共存。这种等价机制会导致部分 IDE 使用存在问题。 

  Python3 中 1 个 tab 只能找另外一个 tab 替代，因此 tab 和 space 共存会导致报错：TabError:  

  inconsistent use of tabs and spaces in indentation.

废弃类差异

* print 语句被 Python3 废弃，统一使用 print 函数
* exec 语句被 python3 废弃，统一使用 exec 函数
* execfile 语句被 Python3 废弃，推荐使用 exec(open("./filename").read())
* 不相等操作符"<>"被 Python3 废弃，统一使用"!="
* long 整数类型被 Python3 废弃，统一使用 int
* xrange 函数被 Python3 废弃，统一使用 range，Python3 中 range 的机制也进行修改并提高了大数据集生成效率
* 异常 StandardError 被 Python3 废弃，统一使用 Exception

#### 关于 Python 程序的运行方面，有什么手段能提升性能

1.使用多进程,充分利用机器的多核性能

2.对于性能影响较大的部分代码,可以用c 或者 c++ 编写

3.对于IO阻塞的性能影响,可以使用IO多路复用来解决

4.尽量用python的内建函数

5.尽量使用局部变量

#### 什么是 Python

* Python是一种编程语言,它有对象,模块,线程,异常处理和自动内存管理,可以加入其他语言对比
* Python是一种解释型语言,Python在代码运行之前不需要解释
* Python还是一种动态语言,在声明对象时,不需要说明变量的类型
* Python适合面向对象的编程,因为他支持通过组合与继承的方式定义类
* 在Python语言中,函数是第一类对象
* Python代码编程快,但运行速度比编译型语言慢

#### 什么是 Python 自省

Python 自省是 Python 具有的一种能力，使程序员面向对象的语言所写的程序在运行时,能够获得对象的类型。Python 是一种解释型语言，为程序员提供了极大的灵活性和控制力。 

