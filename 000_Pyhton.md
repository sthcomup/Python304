### 魔法方法

- `__init__` 构造器，当一个实例被创建的时候初始化的方法。但是它并 不是实例化调用的第一个方法

- `__new__ `才是实例化对象调用的第一个方法，它只取下 cls 参数，并把 其他参数传给``` __init__```。``` __new__```很少使 用，但是也有它适合的场景，尤其 是当类继承自一个像元组或者字符串这样不经常改变的类型的时候。

  - 单例

  - ```python
    class A(object):
    	__instance = None
    	def __new__(cls， *args， **kwargs):
    		if cls.__instance is None:
    			cls.__instance = object.__new__(cls)
    			return cls.__instance 
    		else:
    			return cls.__instance
    ```

- `__iter__` 可迭代对象,返回一个容器迭代器
- `__next__` 返回迭代器的下一个元素
- `__call__` 可调用 对应(),允许一个类像函数一样被调用
- `__getitem__` 定义获取容器中指定元素的行为，相当于 self[key]
- `__enter__` 进入对象执行
- `__exit__` 使用完成退出对象执行 (上下文管理器)
- ```__getattr__ ```定义当用户试图访问一个不存在属性的时候的行为 。
- ```__setattr__ ```定义当一个属性被设置的时候的行为 。
- ```__getattribute__``` 定义当一个属性被访问的时候的行为 。
- `__doc__` 打印注释
- `__str__` print对象
- `__del__` 内存回收执行



---

### 线程,进程,协程

- 进程:`processing`

  ```python
  import os
  from multiprocessing import Process 
  import time
  def pro_func(name, age, **kwargs):
  	for i in range(5):
  		print("子进程正在运行中,name=%s, age=%d, pid=%d" %(name, age, os.getpid()))
  		print(kwargs)
  		time.sleep(0.2)
  if __name__ == '__main__':
   	# 创建 Process 对象
  	p = Process(target=pro_func, args=('小明',18), kwargs={'m': 20})
   	# 启动进程
  	p.start()
    time.sleep(1)
    p.terminate()
    p.join()
  ```

- 线程:`threating`

- 进程与线程的使用场景

  > 多进程适合在 CPU 密集型操作(cpu 操作指令比较多，如位数多的浮点运算)。 
  >
  > 多线程适合在 IO 密集型操作(读写数据操作较多的，比如爬虫)。

- 协程:`yield`?

- 猴子补丁:

- 使用协程时，通常在模块头部加入：gevent.monkey.patch_all()



---



### 类方法(属性),实例方法(属性),静态方法

- 类属性: 实例化对象共享

- 类方法:`@classmethod` 参数为 `cls`

- 类方法一般用在需要对传入的参数进行处理的地方

- 实例属性:

- 一般放在`__init__`里

- `self.var`

- 实例方法:

- `def func(self)`

- `@property` 将方法转为属性,使属性不会被随便修改

- 静态方法:`@staticmethod`

---

### 生成器,迭代器

- 生成器:

- `type() -> genetator`

- 每次调用 next() 生成下一个结果

- 生成器也是可迭代对象

- 迭代器:

可以被next()函数调用并不断返回下一个值的对象称为迭代器：Iterator



- 可迭代对象 Iterable
- isinstance(iter, Iterable) -> True
- 可以直接作用于for循环的对象统称为可迭代对象



---



### 内存管理,垃圾回收

- 引用计数机制

  - 引用数为0则回收

- 标记清除

  - 循环引用的对象 先将循环引 用摘掉再回收

- 分代回收
>
分代回收是一种以空间换时间的操作方式，Python将内存根据对象的存活时间划分为不同的集合，每个集合称为一个代，Python将内存分为了3“代”，分别为年轻代（第0代）、中年代（第1代）、老年代（第2代），他们对应的是3个链表，它们的垃圾收集频率与对象的存活时间的增大而减小。新创建的对象都会分配在年轻代，年轻代链表的总数达到上限时，Python垃圾收集机制就会被触发，把那些可以被回收的对象回收掉，而那些不会回收的对象就会被移到中年代去，依此类推，老年代中的对象是存活时间最久的对象，甚至是存活于整个系统的生命周期内。同时，分代回收是建立在标记清除技术基础之上。分代回收同样作为Python的辅助垃圾收集技术处理那些容器对象


- 内存管理,金字塔形:

  - -1,-2 系统操作

  - 0 c语言操作

  - 1,2 内存池PyMem_Malloc 函数实现,python操作

  - 3 应用层,用户操作

---



### 高级函数

- filter

- map

- lambda 参数1,参数2..:参数表达式

---



### 正则re

- match与search的区别

  >match()函数只检测 RE 是不是在 string 的开始位置匹配，search()会扫描整个 string 查找匹配;
  >也就是说 match()只有在 0 位置匹配成功的话才有返回， 如果不是开始位置匹配成功的话，match()就返回 none。
  
- Python字符串查找和替换

  > re.findall(r’目的字符串’，’原有字符串’) #查询
  >
  > re.findall(r'cast'，'itcast.cn')[0]
  >
  > re.sub(r‘要替换原字符’，’要替换新字符’，’原始字符串’) 
  >
  > re.sub(r'cast'，'heima'，'itcast.cn')
  
- 零宽断言

  - (?<=pattern) (?<!pattern) **STRING** (?=pattern) (?!pattern) ：各种断言出现的相对位置
  - 判断要匹配的内容中是否存在正则匹配的内容, 不会去获取匹配出的字符串
  - 例子: 
    ```
    abcd --> a(?=bc) --> 匹配出a
    bbc --> a(?=bc) --> 匹配失败
    abd  --> a(?=bc) --> 匹配失败
    ```

- (?=exp):断言自身出现的位置的后面能匹配表达式exp

- (?<=exp)断言自身出现的位置的后面能匹配表达式exp

---

### Python数据结构

##### 字典(有序)在内存中的存储结构

字典：

```text
d = {'timmy': 'red', 'barry': 'green', 'guido': 'blue'}
```

原始存储为(无序字典)：

```text
entries = [['--', '--', '--'],
           [-8522787127447073495, 'barry', 'green'],
           ['--', '--', '--'],
           ['--', '--', '--'],
           ['--', '--', '--'],
           [-9092791511155847987, 'timmy', 'red'],
           ['--', '--', '--'],
           [-6480567542315338377, 'guido', 'blue']]
```

新方法如下(python3.5以后)：

```text
indices =  [None, 1, None, None, None, 0, None, 2]
entries =  [[-9092791511155847987, 'timmy', 'red'],
            [-8522787127447073495, 'barry', 'green'],
            [-6480567542315338377, 'guido', 'blue']]
```



---



### 零零散散知识点

- 类型注释

  - `var:str`

  - 输出 `-> int`

- 反射: ?

- hasattr() getattr() setattr()的用法:

  - 为对象属性的存在判断、获取和添加修改

- Python对可变对象（字典或列表）传址，对不可变对象（数字、字符或元祖）传值

- metaclass，元类 ?

- is是身份运算符，判断两个对象的内存id是否相等

  ==是比较运算符，判断两个对象的值是否相等

- deepcopy深拷贝copy浅拷贝

- **dir()函数**

  > dir()函数不带参数时，返回当前范围内的变量、方法和定义的类型列表； 带参数时，返回参数的属性、方法列表。 如果参数包含方法__dir__()，该方法将被调用。如果参数不包含__dir__()，该方法将最大限度地收集参数信息。

- GIL(全局解释器锁)

  - 解决多线程之间数据完整性和状态同步
  - 

- 面对对象三大特性: 继承,多态,封装

  