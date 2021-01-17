# Python从入门到入门



[toc]



## 教程简介

Python Numpy 教程（使用 Jupyter 和 Colab）

教程原文来自：https://cs231n.github.io/python-numpy-tutorial/ 最初由[Justin Johnson](http://cs.stanford.edu/people/jcjohns/)贡献。

在本课程中，我们将使用Python编程语言进行所有作业。Python本身就是一种出色的通用编程语言，但是在一些流行的库（numpy，scipy，matplotlib）的帮助下，Python 成为了科学计算的强大环境。

我们希望你们中的许多人将对 Python 和 numpy 有所了解；对于其余的人，本节将作为速成课程，介绍Python编程语言及其在科学计算中的用法。



----

教程正式开始

## 基础篇

### Python

Python 是一种高级的，~~动态类型化的多范例~~编程语言。Python代码通常被称为几乎类似于伪代码，因为它使您可以在很少的代码行中表达非常强大的思想，同时又易于阅读。例如，这是经典的快速排序算法在Python中的实现：

```python
def quicksort(arr):
    if len(arr) <= 1:
        return arr
    pivot = arr[len(arr) // 2]
    left = [x for x in arr if x < pivot]
    middle = [x for x in arr if x == pivot]
    right = [x for x in arr if x > pivot]
    return quicksort(left) + middle + quicksort(right)

print(quicksort([3,6,8,10,1,2,1]))
# Prints "[1, 1, 2, 3, 6, 8, 10]"
```

### Python版本

Python 已经正式下架了`python2`。 对于此类，所有代码都将使用Python 3.7。在继续本教程之前，请确保您已完成**环境搭建**并正确安装了`python3`虚拟环境。

### 基本数据类型

像大多数语言一样，Python 具有许多基本类型，包括整数，浮点数（1.0），布尔值（true and false）和字符串（balabala）。这些数据类型以其他编程语言所熟悉的方式运行。

#### 数字

```python
x = 3
print(type(x)) # Prints "<class 'int'>"   		#打印x的类型（int）
print(x)       # Prints "3"					   #打印x的值（3）
print(x + 1)   # Addition; prints "4"		    #打印（x+1）
print(x - 1)   # Subtraction; prints "2"
print(x * 2)   # Multiplication; prints "6"
print(x ** 2)  # Exponentiation; prints "9"
x += 1										 #x=x+1的省略写法
print(x)  # Prints "4"
x *= 2										 #x=x*2的省略写法
print(x)  # Prints "8"
y = 2.5
print(type(y)) # Prints "<class 'float'>"
print(y, y + 1, y * 2, y ** 2) # Prints "2.5 3.5 5.0 6.25"
```

请注意，与许多语言不同，Python没有一元的增量（`x++`）或减量（`x--`）运算符。~~（不同于C语言哦）~~

Python还具有用于复数的内置类型。您可以[Python 官方文档](https://docs.python.org/3.5/library/stdtypes.html#numeric-types-int-float-complex)找到所有详细信息 。

#### 布尔

Python 布尔类型的逻辑实现通过英语字符单词`True`和`False`而非符号（`&&`，`||`等）

```python
t = True
f = False
print(type(t)) # Prints "<class 'bool'>"		#打印t的类型
print(t and f) # Logical AND; prints "False"	#逻辑与（且）（真且假这里为假）
print(t or f)  # Logical OR; prints "True"		#逻辑或（真或假这里为或）
print(not t)   # Logical NOT; prints "False"	#逻辑否（True的否定是False）
print(t != f)  # Logical XOR; prints "True"		#判断（True！=False是真命题）
```

#### 字符串

```python
hello = 'hello'    # String literals can use single quotes
world = "world"    # or double quotes; it does not matter.
#字符串可以使用单引号或者双引号括起来

print(hello)       # Prints "hello"
#把变量hello所代表的字符串(hello)打印出来

print(len(hello))  # String length; prints "5"
#打印字符串hello的长度

hw = hello + ' ' + world  # String concatenation
print(hw)  # prints "hello world"
#hw这个字符串是由hello和空格(' ')和world组合起来的

hw12 = '%s %s %d' % (hello, world, 12)  # sprintf style string formatting
print(hw12)  # prints "hello world 12"
#%s %d是占位符，s是string代表字符串，d代表整数，与后面的变量依次关联。

```

字符串对象有很多有用的方法（函数），例如：

```python
s = "hello"
print(s.capitalize())  # Capitalize a string; prints "Hello"
#字符串第一个字母小写变大写

print(s.title())
#字符串中所有单词的首字母小写变大写

print(s.upper())       # Convert a string to uppercase; prints "HELLO"
#小写字母变成大写字母

print(s.rjust(7))      # Right-justify a string, padding with spaces; prints "  hello"
#字符串右对齐，用空格填充。

print(s.center(7))     # Center a string, padding with spaces; prints " hello "
#字符串居中，用空格填充。

print(s.replace('l', '(ell)'))  # Replace all instances of one substring with another;prints "he(ell)(ell)o"
#字符替换函数 字符串中的字符l被(ell)替换

print('  world '.strip())  # Strip leading and trailing whitespace; prints "world"
#去除开头和结尾的空格
```

### 容器

Python内置多种容器类型：列表、字典、集合、元组。

#### 列表

Python列表类似于其它语言中的数组，但是列表可以调整大小，里面的成员也可以是不同的类型。

```python
xs = [3, 1, 2]    # Create a list
#创建列表

print(xs, xs[2])  # Prints "[3, 1, 2] 2"
#打印列表中的第三个成员(xs[0] xs[1] xs[2]中的xs[2])

print(xs[-1])     # Negative indices count from the end of the list; prints "2"
#第-1号元素表示列表的最后一个元素

xs[2] = 'foo'     # Lists can contain elements of different types
#同一列表的不同元素可以是不同类型 例如当前的xs列表中前两元素xs[0] xs[1]为int型 xs[2]为字符串

print(xs)         # Prints "[3, 1, 'foo']"
#可以打印整个列表

xs.append('bar')  # Add a new element to the end of the list
#append函数可以在列表末尾加入新成员

print(xs)         # Prints "[3, 1, 'foo', 'bar']"

x = xs.pop()      # Remove and return the last element of the list
#pop函数会删除列表的最后一个元素并且把这个元素返回(这里我们用变量x接收这个最后一个元素'bar')

print(x, xs)      # Prints "bar [3, 1, 'foo']"
#(这里进行了测试打印)
```

了解更多细节： [官方文档](https://docs.python.org/3.5/tutorial/datastructures.html#more-on-lists).

##### 切片

除了一次访问一个列表元素外，Python还提供了简洁的语法来访问子列表。这称为切片：

```python
nums = list(range(5))     # range is a built-in function that creates a list of integers
#这里创建了一个大小是5的列表(默认元素0 1 2 3 4)
print(nums)               # Prints "[0, 1, 2, 3, 4]"

print(nums[2:4])          # Get a slice from index 2 to 4 (exclusive); prints "[2, 3]"
#这里获得了一个从第2号元素(包含)到第四号元素(不包含)的切片 类似于数学中的[2,4)

print(nums[2:])           # Get a slice from index 2 to the end; prints "[2, 3, 4]"
#这里获得了一个从第2号元素(包含)到最后一个元素的列表切片

print(nums[:2])           # Get a slice from the start to index 2 (exclusive); prints "[0, 1]"
#这里获得了一个从开始到第2号元素(不包含)的切片。

print(nums[:])            # Get a slice of the whole list; prints "[0, 1, 2, 3, 4]"
#获得了一个包含整个列表的切片(copy行为)

print(nums[:-1])          # Slice indices can be negative; prints "[0, 1, 2, 3]"
#切片索引可以为负

nums[2:4] = [8, 9]        # Assign a new sublist to a slice
#将新的子列表分配给切片

print(nums)               # Prints "[0, 1, 8, 9, 4]"
```

我们将在numpy数组的学习中再次看到切片（~~heihei~~）

##### 循环

循环：您可以像这样循环遍历列表的元素：

```python
animals = ['cat', 'dog', 'monkey']
for animal in animals:
    print(animal)
# Prints "cat", "dog", "monkey", each on its own line.
#这里我们使用for关键字循环遍历列表 animals，我们记列表 animals 中的每个成员为animal，通过语句 ‘for animal in animals’ 访问其中的每个 animal,在每次循环时打印这个animal.
```

如果您要访问循环体内每个元素的索引，可以使用内置的`enumrate`方法：

```python
animals = ['cat', 'dog', 'monkey']
for idx, animal in enumerate(animals):
    print('#%d: %s' % (idx, animal))
# Prints "#0: cat", "#1: dog", "#2: monkey", each on its own line
#这里的idx其实是每个animal的索引 0对应cat、1对应dog、2对应monkey.我们使用语句‘for idx, animal in enumerate(animals):’访问其中的索引和成员(键值对)并且在每次循环时一并打印出来。
```

##### 灵活运用

在编程时，我们经常希望将一种数据类型转换为另一种数据类型。作为一个简单的示例，请考虑以下计算平方数的代码：

```python
nums = [0, 1, 2, 3, 4]
squares = []
for x in nums:
    squares.append(x ** 2)
print(squares)   # Prints [0, 1, 4, 9, 16]
#设计思路：获取 nums 列表中的元素并且将其平方后添加到列表 squares 中
```

减少代码量的优化：

```python
nums = [0, 1, 2, 3, 4]
squares = [x ** 2 for x in nums]
print(squares)   # Prints [0, 1, 4, 9, 16]
```

列表推导也可以包含条件：

```python
nums = [0, 1, 2, 3, 4]
even_squares = [x ** 2 for x in nums if x % 2 == 0]
print(even_squares)  # Prints "[0, 4, 16]"
#这里我们只获取偶数的平方
```

#### 字典

字典存储（键，值）对，类似于Java中的Map或Javascript中的对象。您可以像这样使用它：

```python
d = {'cat': 'cute', 'dog': 'furry'}  # Create a new dictionary with some data
#建立了一个字典d 这里可以看出字典是由键值对组成的 cat(键)对应cute(值)

print(d['cat'])       # Get an entry from a dictionary; prints "cute"
#通过键打印值

print('cat' in d)     # Check if a dictionary has a given key; prints "True"
#检查字典d中是否包含某个键cat，这里打印出True

d['fish'] = 'wet'     # Set an entry in a dictionary
#在d中加入条目fish-wet

print(d['fish'])      # Prints "wet"

print(d['monkey'])  # KeyError: 'monkey' not a key of d
#访问不存在的键会报错的（~~呜呜呜~~）

print(d.get('monkey', 'N/A'))  # Get an element with a default; prints "N/A"
#获取具有默认值的元素

print(d.get('fish', 'N/A'))    # Get an element with a default; prints "wet"
#获取具有默认值的元素

del d['fish']         # Remove an element from a dictionary
#del 关键字会根据键参数(fish)在字典中删除该条目

print(d.get('fish', 'N/A')) # "fish" is no longer a key; prints "N/A"
```

更多信息：[官方文档](https://docs.python.org/3.5/library/stdtypes.html#dict).

##### 循环

迭代字典中的键很容易：

```python
d = {'person': 2, 'cat': 4, 'spider': 8}
for animal in d:
    legs = d[animal]
    print('A %s has %d legs' % (animal, legs))
# Prints "A person has 2 legs", "A cat has 4 legs", "A spider has 8 legs"
#animal 是字典d中的键，我们通过角标(d[])将其值得到并且赋值给变量legs最终打印出键和值。
```

如果要访问键及其对应的值，请使用`items`方法：

```python
d = {'person': 2, 'cat': 4, 'spider': 8}
for animal, legs in d.items():
    print('A %s has %d legs' % (animal, legs))
# Prints "A person has 2 legs", "A cat has 4 legs", "A spider has 8 legs"
#item方法有两个键和值两个返回值 我们这里使用animal和legs两个变量接收
```

##### 灵活运用

这与列表运用类似，可让您轻松构造字典。例如：

```python
nums = [0, 1, 2, 3, 4]
even_num_to_square = {x: x ** 2 for x in nums if x % 2 == 0}
print(even_num_to_square)  # Prints "{0: 0, 2: 4, 4: 16}"
```

#### 集合

集合是不同元素的无序集合。作为一个简单的示例，请考虑以下内容：

```python
animals = {'cat', 'dog'}
print('cat' in animals)   # Check if an element is in a set; prints "True"
#检查集合animals中是否有成员cat，这里返回True

print('fish' in animals)  # prints "False"
#检查集合animals中是否有成员fish，这里返回False

animals.add('fish')       # Add an element to a set
#添加成员fish进入集合animals

print('fish' in animals)  # Prints "True"
#检查集合animals中是否有成员fish，这里返回True

print(len(animals))       # Number of elements in a set; prints "3"
#通过len关键字打印集合animals中的成员个数

animals.add('cat')        # Adding an element that is already in the set does nothing
#向集合中增加一个已经存在的成员则什么也不会发生

print(len(animals))       # Prints "3"
#果然什么也没有用发生

animals.remove('cat')     # Remove an element from a set
#remove方法可以删除集合中的成员

print(len(animals))       # Prints "2"
#果然删除了
```

了解更多：[官方文档](https://docs.python.org/3.5/library/stdtypes.html#set).

##### 循环

在集合上进行迭代与在列表上进行迭代具有相同的语法。但是，由于集合是无序的，因此无法假设访问集合元素的顺序：

```python
animals = {'cat', 'dog', 'fish'}
for idx, animal in enumerate(animals):
    print('#%d: %s' % (idx, animal))
# Prints "#0: fish", "#1: dog", "#2: cat"
```

##### 灵活使用

```python
from math import sqrt
#这里从math中导入了sqrt方法
nums = {int(sqrt(x)) for x in range(30)}
print(nums)  # Prints "{0, 1, 2, 3, 4, 5}"
#这里我们使用sqrt方法求平方根，把所有结果转化成整数加入到集合nums中，最终进行了打印。
```

#### 元组

元组是（不可变的）有序值列表。元组在很多方面都类似于列表。最重要的区别之一是元组可以用作字典中的键和集合的元素，而列表则不能。示例：

```python
d = {(x, x + 1): x for x in range(10)}  # Create a dictionary with tuple keys
#这里我们使用元组作为键生成了一个字典

t = (5, 6)        # Create a tuple
#生成元组我们使用小括号，并且用 , 分割元素

print(type(t))    # Prints "<class 'tuple'>"

print(d[t])       # Prints "5"
#相当于d[(5,6)],键(5,6)对应的值是5

print(d[(1, 2)])  # Prints "1"
#同上
```

更多信息：[官方文档](https://docs.python.org/3.5/tutorial/datastructures.html#tuples-and-sequences)

### 函数

我们使用关键字`def`声明创建一个函数，例如：

```python
def sign(x):
    if x > 0:
        return 'positive'
    elif x < 0:
        return 'negative'
    else:
        return 'zero'

for x in [-1, 0, 1]:
    print(sign(x))
# Prints "negative", "zero", "positive"
#我们创建了一个函数 sign,这个函数传入一个参数x，根据x正负性传出positive\negative\zero的结果
```

我们经常会定义函数以接受可选的关键字参数，例如：

```python
def hello(name, loud=False):
    if loud:
        print('HELLO, %s!' % name.upper())
    else:
        print('Hello, %s' % name)

hello('Bob') # Prints "Hello, Bob"
hello('Fred', loud=True)  # Prints "HELLO, FRED!"
#这里的参数loud就是一个可选参数(默认是布尔类型的false),当第二次调用hello函数时我们传入了loud参数为True所以产生了不同的效果
```

更多信息：[官方文档](https://docs.python.org/3.5/tutorial/controlflow.html#defining-functions)

### 类

这部分参考廖雪峰教程，[原文](https://www.liaoxuefeng.com/wiki/1016959663602400/1017496031185408)

面向对象最重要的概念就是类（Class）和实例（Instance），必须牢记类是抽象的模板，比如Greeter类，而实例是根据类创建出来的一个个具体的“对象”，每个对象都拥有相同的方法，但各自的数据可能不同。

在Python中定义类的语法很简单，例如：

```python
class Greeter(object):

    #构造函数
    def __init__(self, name):
        self.name = name  #创建一个实例变量

    #实例方法
    def greet(self, loud=False):
        if loud:
            print('HELLO, %s!' % self.name.upper())
        else:
            print('Hello, %s' % self.name)

g = Greeter('Fred')  # 构造一个Greeter类的实例
g.greet()            # 调用实例g的greet方法; prints "Hello, Fred"
g.greet(loud=True)   # 调用实例g的greet方法(可选参数为True类型); prints "HELLO, FRED!"
```

#### 定义

在Python中，定义类是通过`class`关键字：

```python
class Student(object):
    pass
```

`class`后面紧接着是类名，即`Student`，类名通常是大写开头的单词，紧接着是`(object)`，表示该类是从哪个类继承下来的，继承的概念我们后面再讲，通常，如果没有合适的继承类，就使用`object`类，这是所有类最终都会继承的类。

#### 创建实例

定义好了`Student`类，就可以根据`Student`类创建出`Student`的实例，创建实例是通过类名+()实现的：

```python
	bart = Student()
    
	bart
<__main__.Student object at 0x10a67a590>
	Student
<class '__main__.Student'>
```

可以看到，变量`bart`指向的就是一个`Student`的实例，后面的`0x10a67a590`是内存地址，每个object的地址都不一样，而`Student`本身则是一个类。

可以自由地给一个实例变量绑定属性，比如，给实例`bart`绑定一个`name`属性：

```python
	bart.name = 'Bart Simpson'
	bart.name
'Bart Simpson'
```

由于类可以起到模板的作用，因此，可以在创建实例的时候，把一些我们认为必须绑定的属性强制填写进去。通过定义一个特殊的`__init__`方法，在创建实例的时候，就把`name`，`score`等属性绑上去：

```python
class Student(object):

    def __init__(self, name, score):
        self.name = name
        self.score = score
```

 **注意：特殊方法“__init__”前后分别有两个下划线！！！**

注意到`__init__`方法的第一个参数永远是`self`，表示创建的实例本身，因此，在`__init__`方法内部，就可以把各种属性绑定到`self`，因为`self`就指向创建的实例本身。

有了`__init__`方法，在创建实例的时候，就不能传入空的参数了，必须传入与`__init__`方法匹配的参数，但`self`不需要传，Python解释器自己会把实例变量传进去：

```python
	bart = Student('Bart Simpson', 59)
    
	bart.name
'Bart Simpson'
	bart.score
59
```

和普通的函数相比，在类中定义的函数只有一点不同，就是第一个参数永远是实例变量`self`，并且，调用时，不用传递该参数。除此之外，类的方法和普通函数没有什么区别，所以，你仍然可以用默认参数、可变参数、关键字参数和命名关键字参数。

#### 数据封装

面向对象编程的一个重要特点就是数据封装。在上面的`Student`类中，每个实例就拥有各自的`name`和`score`这些数据。我们可以通过函数来访问这些数据，比如打印一个学生的成绩：

```python
	def print_score(std):
	    print('%s: %s' % (std.name, std.score))

	print_score(bart)
    
# result：Bart Simpson: 59
```

但是，既然`Student`实例本身就拥有这些数据，要访问这些数据，就没有必要从外面的函数去访问，可以直接在`Student`类的内部定义访问数据的函数，这样，就把“数据”给封装起来了。这些封装数据的函数是和`Student`类本身是关联起来的，我们称之为类的方法：

```python
class Student(object):

    def __init__(self, name, score):
        self.name = name
        self.score = score

    def print_score(self):
        print('%s: %s' % (self.name, self.score))
```

要定义一个方法，除了第一个参数是`self`外，其他和普通函数一样。要调用一个方法，只需要在实例变量上直接调用，除了`self`不用传递，其他参数正常传入：

```python
bart.print_score()
#result:Bart Simpson: 59
```

这样一来，我们从外部看`Student`类，就只需要知道，创建实例需要给出`name`和`score`，而如何打印，都是在`Student`类的内部定义的，这些数据和逻辑被“封装”起来了，调用很容易，但却不用知道内部实现的细节。

封装的另一个好处是可以给`Student`类增加新的方法，比如`get_grade`：

```python
class Student(object):
    ...

    def get_grade(self):
        if self.score >= 90:
            return 'A'
        elif self.score >= 60:
            return 'B'
        else:
            return 'C'
```

同样的，`get_grade`方法可以直接在实例变量上调用，不需要知道内部实现细节：

类的构造：

```python
class Student(object):
    def __init__(self, name, score):
        self.name = name
        self.score = score

    def get_grade(self):
        if self.score >= 90:
            return 'A'
        elif self.score >= 60:
            return 'B'
        else:
            return 'C'
```

测试：

```python
lisa = Student('Lisa', 99)
bart = Student('Bart', 59)
print(lisa.name, lisa.get_grade())
print(bart.name, bart.get_grade())
```

结果：

```
Lisa A 
Bart C 
```

##### 小结

类是创建实例的模板，而实例则是一个一个具体的对象，各个实例拥有的数据都互相独立，互不影响；

方法就是与实例绑定的函数，和普通函数不同，方法可以直接访问实例的数据；

通过在实例上调用方法，我们就直接操作了对象内部的数据，但无需知道方法内部的实现细节。

和静态语言不同，Python允许对实例变量绑定任何数据，也就是说，对于两个实例变量，虽然它们都是同一个类的不同实例，但拥有的变量名称都可能不同：

#### 访问限制

在Class内部，可以有属性和方法，而外部代码可以通过直接调用实例变量的方法来操作数据，这样，就隐藏了内部的复杂逻辑。

但是，从前面Student类的定义来看，外部代码还是可以自由地修改一个实例的`name`、`score`属性：

```python
>>> bart = Student('Bart Simpson', 59)
>>> bart.score
59
>>> bart.score = 99
>>> bart.score
99
```

如果要让内部属性不被外部访问，可以把属性的名称前加上两个下划线`__`，在Python中，实例的变量名如果以`__`开头，就变成了一个私有变量（private），只有内部可以访问，外部不能访问，所以，我们把Student类改一改：

```python
class Student(object):

    def __init__(self, name, score):
        self.__name = name
        self.__score = score

    def print_score(self):
        print('%s: %s' % (self.__name, self.__score))
```

改完后，对于外部代码来说，没什么变动，但是已经无法从外部访问`实例变量.__name`和`实例变量.__score`了：

```python
>>> bart = Student('Bart Simpson', 59)
>>> bart.__name
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: 'Student' object has no attribute '__name'
```

这样就确保了外部代码不能随意修改对象内部的状态，这样通过访问限制的保护，代码更加健壮。

但是如果外部代码要获取name和score怎么办？可以给Student类增加`get_name`和`get_score`这样的方法：

```python
class Student(object):
    ...

    def get_name(self):
        return self.__name

    def get_score(self):
        return self.__score
```

如果又要允许外部代码修改score怎么办？可以再给Student类增加`set_score`方法：

```python
class Student(object):
    ...

    def set_score(self, score):
        self.__score = score
```

##### 参数检查

你也许会问，原先那种直接通过`bart.score = 99`也可以修改啊，为什么要定义一个方法大费周折？因为在方法中，可以对参数做检查，避免传入无效的参数：

```python
class Student(object):
    ...

    def set_score(self, score):
        if 0 <= score <= 100:
            self.__score = score
        else:
            raise ValueError('bad score')
```

需要注意的是，在Python中，变量名类似`__xxx__`的，也就是以双下划线开头，并且以双下划线结尾的，是特殊变量，特殊变量是可以直接访问的，不是private变量，所以，不能用`__name__`、`__score__`这样的变量名。

有些时候，你会看到以一个下划线开头的实例变量名，比如`_name`，这样的实例变量外部是可以访问的，但是，按照约定俗成的规定，当你看到这样的变量时，意思就是，“虽然我可以被访问，但是，请把我视为私有变量，不要随意访问”。

#### 继承与多态

#### 继承和多态

在程序设计中，当我们定义一个class的时候，可以从某个现有的class继承，新的class称为子类（Subclass），而被继承的class称为基类、父类或超类（Base class、Super class）。

比如，我们已经编写了一个名为`Animal`的class，有一个`run()`方法可以直接打印：

```python
class Animal(object):
    def run(self):
        print('Animal is running...')
```

当我们需要编写`Dog`和`Cat`类时，就可以直接从`Animal`类继承：

```python
class Dog(Animal):
    pass

class Cat(Animal):
    pass
```

对于`Dog`来说，`Animal`就是它的父类，对于`Animal`来说，`Dog`就是它的子类。`Cat`和`Dog`类似。

继承有什么好处？最大的好处是子类获得了父类的全部功能。由于`Animial`实现了`run()`方法，因此，`Dog`和`Cat`作为它的子类，什么事也没干，就自动拥有了`run()`方法：

```python
dog = Dog()
dog.run()

cat = Cat()
cat.run()
```

运行结果：

```python
Animal is running...
Animal is running...
```

当然，也可以对子类增加一些方法，比如Dog类：

```python
class Dog(Animal):

    def run(self):
        print('Dog is running...')

    def eat(self):
        print('Eating meat...')
```

继承的第二个好处需要我们对代码做一点改进。你看到了，无论是`Dog`还是`Cat`，它们`run()`的时候，显示的都是`Animal is running...`，符合逻辑的做法是分别显示`Dog is running...`和`Cat is running...`，因此，对`Dog`和`Cat`类改进如下：

```python
class Dog(Animal):

    def run(self):
        print('Dog is running...')

class Cat(Animal):

    def run(self):
        print('Cat is running...')
```

再次运行，结果如下：

```
Dog is running...
Cat is running...
```

当子类和父类都存在相同的`run()`方法时，我们说，子类的`run()`覆盖了父类的`run()`，在代码运行的时候，总是会调用子类的`run()`。这样，我们就获得了继承的另一个好处：**多态**。

要理解什么是多态，我们首先要对数据类型再作一点说明。当我们定义一个class的时候，我们实际上就定义了一种数据类型。我们定义的数据类型和Python自带的数据类型，比如str、list、dict没什么两样：

```python
a = list() # a是list类型
b = Animal() # b是Animal类型
c = Dog() # c是Dog类型
```

当我们创建了一个`Dog`的实例`c`时，我们认为`c`的数据类型是`Dog`没错，但`c`同时也是`Animal`也没错，`Dog`本来就是`Animal`的一种！

所以，在继承关系中，如果一个实例的数据类型是某个子类，那它的数据类型也可以被看做是父类。但是，反过来就不行：`Dog`可以看成`Animal`，但`Animal`不可以看成`Dog`。

要理解多态的好处，我们还需要再编写一个函数，这个函数接受一个`Animal`类型的变量：

```python
def run_twice(animal):
    animal.run()
    animal.run()
```

当我们传入`Animal`的实例时，`run_twice()`就打印出：

```python
>>> run_twice(Animal())
Animal is running...
Animal is running...
```

当我们传入`Dog`的实例时，`run_twice()`就打印出：

```python
>>> run_twice(Dog())
Dog is running...
Dog is running...
```

当我们传入`Cat`的实例时，`run_twice()`就打印出：

```python
>>> run_twice(Cat())
Cat is running...
Cat is running...
```

看上去没啥意思，但是仔细想想，现在，如果我们再定义一个`Tortoise`类型，也从`Animal`派生：

```python
class Tortoise(Animal):
    def run(self):
        print('Tortoise is running slowly...')
```

当我们调用`run_twice()`时，传入`Tortoise`的实例：

```python
>>> run_twice(Tortoise())
Tortoise is running slowly...
Tortoise is running slowly...
```

你会发现，新增一个`Animal`的子类，不必对`run_twice()`做任何修改，实际上，任何依赖`Animal`作为参数的函数或者方法都可以不加修改地正常运行，原因就在于多态。

多态的好处就是，当我们需要传入`Dog`、`Cat`、`Tortoise`……时，我们只需要接收`Animal`类型就可以了，因为`Dog`、`Cat`、`Tortoise`……都是`Animal`类型，然后，按照`Animal`类型进行操作即可。由于`Animal`类型有`run()`方法，因此，传入的任意类型，只要是`Animal`类或者子类，就会自动调用实际类型的`run()`方法，这就是多态的意思：

对于一个变量，我们只需要知道它是`Animal`类型，无需确切地知道它的子类型，就可以放心地调用`run()`方法，而具体调用的`run()`方法是作用在`Animal`、`Dog`、`Cat`还是`Tortoise`对象上，由运行时该对象的确切类型决定，这就是多态真正的威力：调用方只管调用，不管细节，而当我们新增一种`Animal`的子类时，只要确保`run()`方法编写正确，不用管原来的代码是如何调用的。这就是著名的“开闭”原则：

对扩展开放：允许新增`Animal`子类；

对修改封闭：不需要修改依赖`Animal`类型的`run_twice()`等函数。

继承还可以一级一级地继承下来，就好比从爷爷到爸爸、再到儿子这样的关系。而任何类，最终都可以追溯到根类object，这些继承关系看上去就像一颗倒着的树。比如如下的继承树：

```ascii
                ┌───────────────┐
                │    object     │
                └───────────────┘
                        │
           ┌────────────┴────────────┐
           │                         │
           ▼                         ▼
    ┌─────────────┐           ┌─────────────┐
    │   Animal    │           │    Plant    │
    └─────────────┘           └─────────────┘
           │                         │
     ┌─────┴──────┐            ┌─────┴──────┐
     │            │            │            │
     ▼            ▼            ▼            ▼
┌─────────┐  ┌─────────┐  ┌─────────┐  ┌─────────┐
│   Dog   │  │   Cat   │  │  Tree   │  │ Flower  │
└─────────┘  └─────────┘  └─────────┘  └─────────┘
```

##### 静态语言 vs 动态语言

对于静态语言（例如Java）来说，如果需要传入`Animal`类型，则传入的对象必须是`Animal`类型或者它的子类，否则，将无法调用`run()`方法。

对于Python这样的动态语言来说，则不一定需要传入`Animal`类型。我们只需要保证传入的对象有一个`run()`方法就可以了：

```python
class Timer(object):
    def run(self):
        print('Start...')
```

这就是动态语言的“鸭子类型”，它并不要求严格的继承体系，一个对象只要“看起来像鸭子，走起路来像鸭子”，那它就可以被看做是鸭子。

Python的“file-like object“就是一种鸭子类型。对真正的文件对象，它有一个`read()`方法，返回其内容。但是，许多对象，只要有`read()`方法，都被视为“file-like object“。许多函数接收的参数就是“file-like object“，你不一定要传入真正的文件对象，完全可以传入任何实现了`read()`方法的对象。

##### 小结

继承可以把父类的所有功能都直接拿过来，这样就不必重零做起，子类只需要新增自己特有的方法，也可以把父类不适合的方法覆盖重写。

动态语言的鸭子类型特点决定了继承不像静态语言那样是必须的。

------

## 进阶篇（库）

### Numpy库

[Numpy](http://www.numpy.org/)是Python中科学计算的核心库。它提供了一个高性能的多维数组对象，以及用于处理这些数组的工具。如果您已经熟悉MATLAB，则可能会发现 本教程对于Numpy入门[有点作用](https://docs.scipy.org/doc/numpy/user/numpy-for-matlab-users.html)

#### 数组

numpy数组是所有相同类型的值的网格，并由非负整数的元组索引。维数是数组的*等级*。 数组的*形状*是一个整数元组，给出沿每个维度的数组大小

我们可以从嵌套的Python列表初始化numpy数组，并使用方括号访问元素：

```python
import numpy as np

a = np.array([1, 2, 3])   
#建立了一个1级数组

print(type(a))            
# Prints "<class 'numpy.ndarray'>"

print(a.shape)            
# Prints "(3,)"

print(a[0], a[1], a[2])   
# Prints "1 2 3"

a[0] = 5                  
#修改数组a的第一个元素为5
print(a)                  
# Prints "[5, 2, 3]"

b = np.array([[1,2,3],[4,5,6]])    
#建立一个2级数组
print(b.shape)                     
# Prints "(2, 3)"
print(b[0, 0], b[0, 1], b[1, 0])   
# Prints "1 2 4"
```

Numpy还提供了许多创建数组的功能：

```python
import numpy as np

a = np.zeros((2,2))   
#建立一个元素全是0的2*2的2级数组
print(a)              
# Prints "[[ 0.  0.]
#          [ 0.  0.]]"

b = np.ones((1,2))    
#建立一个元素全是1的1*2的2级数组
print(b)              
# Prints "[[ 1.  1.]]"

c = np.full((2,2), 7)  
#建立一个常量数组
print(c)               
# Prints "[[ 7.  7.]
#          [ 7.  7.]]"

d = np.eye(2)         
#建立一个2*2的单位矩阵
print(d)              
# Prints "[[ 1.  0.]
#          [ 0.  1.]]"
#有线性代数那味了

e = np.random.random((2,2)) 
#建立一个由随机值组成的数组
print(e)                     
# Might print "[[ 0.91940167  0.08143941]
#               [ 0.68744134  0.87236623]]"
```

您可以阅读有关数组创建的其他方法的信息 [官方文档](http://docs.scipy.org/doc/numpy/user/basics.creation.html#arrays-creation).

#### 数组索引

Numpy提供了几种索引数组的方法。

##### 切片

与Python列表类似，可以对numpy数组进行切片。由于数组可能是多维的，因此必须为数组的每个维度指定一个切片：

```python
import numpy as np

# Create the following rank 2 array with shape (3, 4)
# [[ 1  2  3  4]
#  [ 5  6  7  8]
#  [ 9 10 11 12]]
a = np.array([[1,2,3,4], [5,6,7,8], [9,10,11,12]])

#使用切片提取出由前2行组成的子数组和第1和第2列； b是以下形状数组（2，2）：
# [[2 3]
#  [6 7]]
b = a[:2, 1:3]

#数组的一部分是对相同数据的视图，因此可以对其进行修改，这将修改原始数组。
print(a[0, 1])   # Prints "2"
b[0, 0] = 77     # b[0,0]和a[0,1]完全等价
print(a[0, 1])   # Prints "77"
```

您也可以将整数索引与切片索引混合使用。但是，这样做将产生比原始数组低级的数组。请注意，这与MATLAB处理数组切片的方式完全不同：

```python
import numpy as np

# Create the following rank 2 array with shape (3, 4)
# [[ 1  2  3  4]
#  [ 5  6  7  8]
#  [ 9 10 11 12]]
a = np.array([[1,2,3,4], [5,6,7,8], [9,10,11,12]])

#两种访问数组中间行数据的方法。 
#将整数索引与切片混合会产生一个较低等级的数组， 
#仅使用切片时会产生与数组相同等级的数组 
#原始数组：
row_r1 = a[1, :]    
# Rank 1 view of the second row of a
row_r2 = a[1:2, :]  
#Rank 2 view of the second row of a

print(row_r1, row_r1.shape)  
# Prints "[5 6 7 8] (4,)"
print(row_r2, row_r2.shape)  
# Prints "[[5 6 7 8]] (1, 4)"

# 当访问数组的列时，我们可以做出相同的区分：
col_r1 = a[:, 1]
col_r2 = a[:, 1:2]
print(col_r1, col_r1.shape)  
# Prints "[ 2  6 10] (3,)"
print(col_r2, col_r2.shape)  
# Prints "[[ 2]
#          [ 6]
#          [10]] (3, 1)"
```

##### 整数数组索引

使用切片索引到numpy数组时，生成的数组视图将始终是原始数组的子数组。相反，整数数组索引使您可以使用另一个数组中的数据构造任意数组。例子：

```python
import numpy as np

a = np.array([[1,2], [3, 4], [5, 6]])

# 整数数组索引的示例。
# 返回的数组将具有形状（3，）

print(a[[0, 1, 2], [0, 1, 0]])  
# Prints "[1 4 5]"

# 上面的整数数组索引示例等同于此
print(np.array([a[0, 0], a[1, 1], a[2, 0]])) 
# Prints "[1 4 5]"

# 使用整数数组索引时，可以重复使用源数组中的相同元素：
print(a[[0, 0], [1, 1]])  
# Prints "[2 2]"

#等效于前面的整数数组索引示例
print(np.array([a[0, 1], a[0, 1]]))  
# Prints "[2 2]"
```

整数数组索引的一个有用技巧是从矩阵的每一行中选择或更改一个元素：

```python
import numpy as np

a = np.array([[1,2,3], [4,5,6], [7,8,9], [10, 11, 12]])

print(a)  
# prints "array([[ 1,  2,  3],
#                [ 4,  5,  6],
#                [ 7,  8,  9],
#                [10, 11, 12]])"

# 创建索引数组
b = np.array([0, 2, 0, 1])

# 使用b中的索引从a的每一行中选择一个元素
print(a[np.arange(4), b])  
# Prints "[ 1  6  7 11]"

# 使用b中的索引来修改a的每一行中的一个元素
a[np.arange(4), b] += 10

print(a)  # prints "array([[11,  2,  3],
          #                [ 4,  5, 16],
          #                [17,  8,  9],
          #                [10, 21, 12]])
```

##### 布尔数组索引

布尔数组索引使您可以挑选出数组的任意元素。通常，这种类型的索引用于选择满足某些条件的数组元素。这是一个例子

```python
import numpy as np

a = np.array([[1,2], [3, 4], [5, 6]])

bool_idx = (a > 2)   
#查找数组a中大于2的元素
#这将返回相同的布尔值的numpy数组
#形状为a，其中每个位置替换为bool类型来说明是否>2

print(bool_idx)      
# Prints "[[False False]
#          [ True  True]
#          [ True  True]]"

# 我们使用布尔数组索引来构造由与bool_idx的True值相对应的元素组成的等级1数组
print(a[bool_idx])  
# Prints "[3 4 5 6]"

# 我们可以在一个简洁的语句中完成上述所有操作：
print(a[a > 2])     
# Prints "[3 4 5 6]"
```

了解更多：[官方文档](http://docs.scipy.org/doc/numpy/reference/arrays.indexing.html)

#### 数据类型

每个numpy数组都是相同类型的元素的网格。Numpy提供了大量可用于构造数组的数据类型。在创建数组时，Numpy会尝试猜测数据类型，但是构造数组的函数通常还包含一个可选参数，以明确指定该数据类型。这是一个例子：

```python
import numpy as np

x = np.array([1, 2])   
#让 numpy 来选择数据类型
print(x.dtype)         
# Prints "int64"

x = np.array([1.0, 2.0])   
#让 numpy 来选择数据类型
print(x.dtype)             
# Prints "float64"

x = np.array([1, 2], dtype=np.int64)   # 强制使用特定数据类型
print(x.dtype)                         # Prints "int64"
```

了解更多：[官方文档](http://docs.scipy.org/doc/numpy/reference/arrays.dtypes.html)

#### 数组的数学函数

基本的数学函数在数组上按元素进行运算，并且可用作运算符重载和numpy模块中的函数：

```python
import numpy as np

x = np.array([[1,2],[3,4]], dtype=np.float64)
y = np.array([[5,6],[7,8]], dtype=np.float64)

#按元素求和，这会产生数组
# [[ 6.0  8.0]
#  [10.0 12.0]]
print(x + y)
print(np.add(x, y))

#按元素求差，这会都产生数组
# [[-4.0 -4.0]
#  [-4.0 -4.0]]
print(x - y)
print(np.subtract(x, y))

#按元素求乘积，这会都产生数组
# [[ 5.0 12.0]
#  [21.0 32.0]]
print(x * y)
print(np.multiply(x, y))

#按元素求商，这会都产生数组
# [[ 0.2         0.33333333]
#  [ 0.42857143  0.5       ]]
print(x / y)
print(np.divide(x, y))

#按元素求平方根，这会都产生数组
# [[ 1.          1.41421356]
#  [ 1.73205081  2.        ]]
print(np.sqrt(x))
```

请注意，与MATLAB不同，`*`是逐元素乘法，而不是矩阵乘法。取而代之的是，我们使用该`dot`函数来计算向量的内积，将向量乘以矩阵以及将矩阵相乘。`dot`可作为numpy模块中的函数和数组对象的实例方法使用：

```python
import numpy as np

x = np.array([[1,2],[3,4]])
y = np.array([[5,6],[7,8]])

v = np.array([9,10])
w = np.array([11, 12])

# 向量的内积运算; both produce 219
print(v.dot(w))
print(np.dot(v, w))

# 矩阵/矢量积; both produce the rank 1 array [29 67]
print(x.dot(v))
print(np.dot(x, v))

# 矩阵/矩阵乘积; both produce the rank 2 array
# [[19 22]
#  [43 50]]
print(x.dot(y))
print(np.dot(x, y))
```

Numpy提供了许多有用的函数来对数组执行计算。最有用的之一是`sum`：

```python
import numpy as np

x = np.array([[1,2],[3,4]])

print(np.sum(x))  
# 计算所有元素的和; prints "10"
print(np.sum(x, axis=0))  
# 计算列和; prints "[4 6]"
print(np.sum(x, axis=1)) 
# 计算行和; prints "[3 7]"
```

更多数学函数：[在文档中](http://docs.scipy.org/doc/numpy/reference/routines.math.html)

除了使用数组计算数学函数外，我们经常需要重整形或以其他方式处理数组中的数据。这种操作的最简单的例子是转置矩阵。要转置矩阵，只需使用`T`数组对象的属性：

```python
import numpy as np

x = np.array([[1,2], [3,4]])
print(x)    # Prints "[[1 2]
            #          [3 4]]"
print(x.T)  # Prints "[[1 3]
            #          [2 4]]"
```

更多对数组（矩阵）的操作：[官方文档](http://docs.scipy.org/doc/numpy/reference/routines.array-manipulation.html)

#### 广播

广播是一种强大的机制，允许numpy在执行算术运算时使用不同形状的数组。通常，我们有一个较小的数组和一个较大的数组，并且我们想多次使用较小的数组对较大的数组执行某些操作。

例如，假设我们要向矩阵的每一行添加一个常数向量。我们可以这样做：

```python
import numpy as np

# 我们要将向量v加在矩阵x上，并且存入矩阵y
x = np.array([[1,2,3], [4,5,6], [7,8,9], [10, 11, 12]])
v = np.array([1, 0, 1])
y = np.empty_like(x)   
# 创建一个和x一样形状的矩阵y

# 通过迭代将向量v添加到矩阵x的每一行
for i in range(4):
    y[i, :] = x[i, :] + v

# Now y is the following
# [[ 2  2  4]
#  [ 5  5  7]
#  [ 8  8 10]
#  [11 11 13]]
print(y)
```

这有效，但是，当矩阵`x`很大时，在Python中计算显式循环可能会很慢。请注意，将向量添加`v`到矩阵的每一行 `x`等效于`vv`通过`v`垂直堆叠多个副本，然后对`x`和进行元素求和来形成矩阵`vv`。我们可以像这样实现这种方法：

```python
import numpy as np

# 我们把向量v加到矩阵x的每一行上，把结果存入矩阵y
x = np.array([[1,2,3], [4,5,6], [7,8,9], [10, 11, 12]])
v = np.array([1, 0, 1])
vv = np.tile(v, (4, 1))   
# vv是向量v叠放四行的矩阵
print(vv)                 
# Prints "[[1 0 1]
#          [1 0 1]
#          [1 0 1]
#          [1 0 1]]"
y = x + vv  
print(y)  # Prints "[[ 2  2  4
          #          [ 5  5  7]
          #          [ 8  8 10]
          #          [11 11 13]]"
```

Numpy广播使我们无需实际创建v的多个副本即可执行此计算。请考虑以下版本，使用广播：

```python
import numpy as np

# 我们把向量v加到矩阵x的每一行上，把结果存入矩阵y
x = np.array([[1,2,3], [4,5,6], [7,8,9], [10, 11, 12]])
v = np.array([1, 0, 1])
y = x + v  
# 通过广播把向量v加到x的每一行上
print(y)  # Prints "[[ 2  2  4]
          #          [ 5  5  7]
          #          [ 8  8 10]
          #          [11 11 13]]"
```

##### 规则

 	1. 如果数组的秩不同，则将低秩数组的形状加1s，直到两个形状的长度相同。
 	2. 如果两个数组的尺寸相同，或者其中一个数组的尺寸为1，则称这两个数组在尺寸上兼容。
 	3. 如果阵列在所有维度上都兼容，则可以一起广播。
 	4. 广播时，每个数组的行为就好像它们中形状较大的一个一样。
 	5. 在一个数组的大小为1而另一个数组的大小大于1的任何维度中，第一个数组的行为就像是沿着该维度复制的一样。

更多介绍：[文档](http://docs.scipy.org/doc/numpy/user/basics.broadcasting.html) [解释](http://scipy.github.io/old-wiki/pages/EricsBroadcastingDoc).

支持广播的功能称为通用功能。您可以在[文档](http://docs.scipy.org/doc/numpy/reference/ufuncs.html#available-ufuncs)中找到所有通用功能的列表。

#### Numpy 官方文档

 [官方文档](http://docs.scipy.org/doc/numpy/reference/)

### SciPy

Numpy提供了高性能的多维数组和基本工具，可以使用这些数组进行计算和操作。 [SciPy](http://docs.scipy.org/doc/scipy/reference/) 以此为基础，并提供了可在numpy数组上运行的大量功能，可用于不同类型的科学和工程应用程序。

熟悉SciPy的最佳方法是 [浏览文档](http://docs.scipy.org/doc/scipy/reference/index.html)。我们将重点介绍SciPy的某些部分，这些部分可能对本课程有用。

#### 影像操作

SciPy提供了一些处理图像的基本功能。例如，它具有将磁盘中的图像读取到numpy数组，将numpy数组作为图像写入磁盘以及调整图像大小的功能。这是一个简单的示例，展示了这些功能：

```python
from scipy.misc import imread, imsave, imresize

# 将一个JPEG图像读入numpy数组
img = imread('assets/cat.jpg')
print(img.dtype, img.shape)  
# Prints "uint8 (400, 248, 3)"

#我们可以通过使用不同的标量常数缩放每个颜色通道来为图像着色。图像的形状为（400，248，3）;我们将其乘以形状（3，）的数组[1，0.95，0.9]； numpy广播意味着保持红色通道不变，并将绿色和蓝色通道分别乘以0.95和0.9。
img_tinted = img * [1, 0.95, 0.9]

# 将着色图像的大小调整为300 x 300像素。
img_tinted = imresize(img_tinted, (300, 300))

# 将着色的图像写回到磁盘
imsave('assets/cat_tinted.jpg', img_tinted)
```

效果：![原始图](.\cat.jpg)![修改后](./cat_tinted.jpg)

#### MATLAB文件

功能`scipy.io.loadmat`和`scipy.io.savemat`允许您读取和写入MATLAB文件。您可以[在文档中](http://docs.scipy.org/doc/scipy/reference/io.html)阅读有关它们 [的信息](http://docs.scipy.org/doc/scipy/reference/io.html)。

#### 点之间的距离

SciPy定义了一些有用的函数来计算点集之间的距离。

该函数`scipy.spatial.distance.pdist`计算给定集中所有对点之间的距离：

```python
import numpy as np
from scipy.spatial.distance import pdist, squareform

# 创建以下数组，其中每一行都是2D空间中的一个点：
# [[0 1]
#  [1 0]
#  [2 0]]
x = np.array([[0, 1], [1, 0], [2, 0]])
print(x)

# 计算x的所有行之间的欧几里得距离。
# d [i，j]是x [i，：]和x [j，：]之间的欧几里得距离，
# d是以下数组：
# [[ 0.          1.41421356  2.23606798]
#  [ 1.41421356  0.          1.        ]
#  [ 2.23606798  1.          0.        ]]
d = squareform(pdist(x, 'euclidean'))
print(d)
```

您可以[在文档中](http://docs.scipy.org/doc/scipy/reference/generated/scipy.spatial.distance.pdist.html)阅读有关此功能的所有详细信息 。

类似的函数（`scipy.spatial.distance.cdist`）计算所有两组点之间的距离，您可以[在文档中](http://docs.scipy.org/doc/scipy/reference/generated/scipy.spatial.distance.cdist.html)阅读有关内容。

### Matplotlib

[Matplotlib](http://matplotlib.org/)是一个绘图库。在本教程中，将简要介绍该`matplotlib.pyplot`模块，该模块提供了类似于MATLAB的绘图系统。

#### 绘图

matplotlib中最重要的功能是`plot`，它允许您绘制2D数据。这是一个简单的示例：

```python
import numpy as np
import matplotlib.pyplot as plt

# 计算正弦曲线上点的x和y坐标
x = np.arange(0, 3 * np.pi, 0.1)
y = np.sin(x)

# 使用matplotlib绘制点
plt.plot(x, y)
plt.show()  
# 您必须调用plt.show（）才能显示图形。
```

效果：![](./sine.png)

只需一点额外的工作，我们就可以轻松地一次绘制多条线，并添加标题，图例和轴标签：

```python
import numpy as np
import matplotlib.pyplot as plt

# 计算正弦和余弦曲线上的点的x和y坐标
x = np.arange(0, 3 * np.pi, 0.1)
y_sin = np.sin(x)
y_cos = np.cos(x)

# 使用matplotlib绘制点
plt.plot(x, y_sin)
plt.plot(x, y_cos)
plt.xlabel('x axis label')
plt.ylabel('y axis label')
plt.title('Sine and Cosine')
plt.legend(['Sine', 'Cosine'])
plt.show()
```

效果：![](.\sine_cosine.png)

您可以[在文档中](http://matplotlib.org/api/pyplot_api.html#matplotlib.pyplot.plot)阅读有关该`plot`功能的 更多信息。

#### 子图

您可以使用`subplot`函数在同一图中绘制不同的事物。这是一个例子：

```python
import numpy as np
import matplotlib.pyplot as plt

# 计算正弦和余弦曲线上的点的x和y坐标
x = np.arange(0, 3 * np.pi, 0.1)
y_sin = np.sin(x)
y_cos = np.cos(x)

# 设置高度为2且宽度为1的子图网格
# 设置第一个这样的子图为active。
plt.subplot(2, 1, 1)

# 制作第一个情景
plt.plot(x, y_sin)
plt.title('Sine')

# 将第二个子图设置为活动状态，并绘制第二个图。
plt.subplot(2, 1, 2)
plt.plot(x, y_cos)
plt.title('Cosine')

# Show the figure.
plt.show()
```

![](.\sine_cosine_subplot.png)

您可以[在文档中](http://matplotlib.org/api/pyplot_api.html#matplotlib.pyplot.subplot)阅读有关该`subplot`功能的 更多信息。

#### 图片

您可以使用该`imshow`功能显示图像。这是一个例子

```python
import numpy as np
from scipy.misc import imread, imresize
import matplotlib.pyplot as plt

img = imread('assets/cat.jpg')
img_tinted = img * [1, 0.95, 0.9]

# 显示原始图片
plt.subplot(1, 2, 1)
plt.imshow(img)

# 显示有色图像
plt.subplot(1, 2, 2)

# imshow的一个小问题是，如果显示的不是uint8数据，可能会产生奇怪的结果。要解决此问题，我们在显示图像之前将图像显式转换为uint8。
plt.imshow(np.uint8(img_tinted))
plt.show()
```

效果：![](.\cat_tinted_imshow.png)

## 恭喜

恭喜您完成了本教程，Python这门语言您已经从入门到入门啦。希望您继续学习再接再厉呀。