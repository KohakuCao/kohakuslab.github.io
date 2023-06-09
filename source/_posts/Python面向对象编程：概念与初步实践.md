---
title: Python面向对象编程：概念与初步实践
date: 2023-05-13 09:58:52
tags: [Python, 面向对象编程, 编程]
categories: Coding
swiper: true
img: https://i.imgloc.com/2023/05/14/VZOpkF.jpeg
excerpt: 本文是为了帮助完成北京航空航天大学大学计算机基础（理科类）课程大作业而编写的，旨在帮助非代码类专业的学生迅速掌握面向对象编程的基本概念与初步实践。
---

## 前言

本文是为了帮助完成北京航空航天大学大学计算机基础（理科类）课程大作业而编写的，旨在帮助非代码类专业的学生迅速掌握面向对象编程的基本概念与初步实践。在大作业这样的较大规模的项目开发中，面向对象编程因为其易于维护和扩展，逻辑清晰而具有很大优势。

本文会尽量以通俗易懂的方式讲解面向对象编程的基本概念，同时会给出一些简单的代码示例，帮助没有很丰富代码经验的读者理解面向对象编程的基本思想。

## 基本概念

首先要先了解两种基本的编程思想：面向过程编程和面向对象编程。

### 面向过程

面向过程编程（Procedural Oriented Programming, POP）是以过程为中心的，也就是说这种编程思想把解决问题的过程分解为一个个步骤，程序员根据这个过程编写每一个步骤的代码，然后再按照一定的顺序执行这些步骤，最终完成任务。所有步骤走完了，任务就完成了。

### 面向对象

面向对象编程（Object Oriented Programming, OOP）是以对象为中心的，这代表编写程序的时候首先要经历一个抽象的过程。我们首先要把具体的事务抽象成**对象（Object）**，考虑这一个对象有怎么样**属性（Property）**，能够执行怎样的**方法（Method）**。然后我们根据这些对象的属性和可以执行的方法来编写代码，让一个个对象做自己的事情，最终结合起来完成整个任务。其中依据**类（Class）**建立对象的过程称为**实例化（Instantiate）**，因而对象也被叫做类的一个实例。

## Why OOP

事实上，我们无法用优劣来区分POP和OOP，因为这两种编程思想都有各自的优势和劣势。POP的优势很简单，它的思维逻辑是直线的，同时代码编写起来也简单，占用的硬件资源也更少，因此在很多底层开发中例如单片机、嵌入式系统、类Unix系统中有广泛的应用。然而OOP在大型项目的的开发中优势是非常明显的，尽管它占用了更多硬件资源来实例化对象，但是它的代码逻辑更加清晰，易于维护和扩展，对程序员要更加友好，能够极大地提高开发效率。

面向对象变成的主要优势在于它的**可维护性（Maintainability）**。一个好的大型项目代码首先要求，我们能够通过改变一部分代码来增加、修改、删除一个功能，并且其它功能能够不受到任何（负面的）影响。下面来看一个简单的例子：

见泷原市生活着许多魔法少女，他们需要通过讨伐魔女净化自己的灵魂宝石来维持生存，现在我们用一段程序来表示鹿目圆（Madoka）和美树沙耶香（Sayaka）的这个过程。如果使用面向过程的写法，我们可能会这样写：

```python
#两人的灵魂宝石余量
madokaSoul=100
sayakaSoul=100

#两个人的战斗
def madokasBattle():
    #code1
    
def sayakasBattle():
    #code2

#两个人活动需要消耗灵魂宝石
madoakSoul-=10
sayakaSoul-=10

#两个人的战斗成果
madokaSoul+=madokasBattle()
sayakaSoul+=sayakasBattle()
```

这是最直接的写法，我们看到由于不存在抽象过程，每增加一个魔法少女就必须再写一遍可能很类似的代码，这样的代码不仅冗余，而且不易于维护。同时，由于面向过程的代码就是从上至下执行的，因此在修改的时候就会牵一发而动全身，修改某一功能可能就会破坏其他功能。如果我们用面向对象的思想来写，我们可以这样写：

```python
#抽象出一个魔法少女的类
class MahouShoujo:
    def __init__(self, soul):
        #初始化，定义灵魂宝石余量这个属性
        self.soul=soul
    def battle(self):
        #战斗方法
        #code
    def consume(self):
        #消耗灵魂宝石
        self.soul-=10
    def recover(self):
        #战斗成果
        self.soul+=self.battle()
    
#实例化两个魔法少女
madoka=MahouShoujo(100)
sayaka=MahouShoujo(100)
while(everyday):
    #两个人活动需要消耗灵魂宝石
    madoka.consume()
    sayaka.consume()
    #两个人的战斗成果
    madoka.recover()
    sayaka.recover()
```

面向对象的编程思想把魔法少女抽象成一个类，这是因为所以魔法少女都具有类似的属性和方法，因此我们不需要考虑这个魔法少女具体是谁。这样的好处首先在于提高代码复用水平，不需要对每一个魔法少女单独编写；此外，面向对象的写法允许通过修改类定义而修改所有魔法少女的行为，但是又不会影响到某一个特定的个体。

## 基本特性

面向对象有三个基本特性：封装、继承和多态。

### 封装

**封装（Encapsulation）**是一个类似“黑盒子”的机制，在面向对象编程中它要求把具体的事物的属性、方法封装为抽象的类和对象。在类外部调用的时候，我们并不关心它的内部是如何实现的，只需要关心它有怎样的功能，也就是我们要给一个方法怎样的输入，它又会给出怎样的输出。这样的好处首先在于，在开发大型项目的时候（尤其是合作开发），编写每一部分只需要专注于自身功能的实现即可；其次，封装也是一种安全机制，它可以防止类的使用者直接修改类内部的属性，从而导致不可预料的后果。

举个例子，Python中内置的数据类型如整数、字符串、列表的本质都是一个类，而我们在调用他们的方法例如
```python
a="Hello World"
a.upper()
```
的时候，我们并不关心upper方法是怎么实现的，只需要知道它的功能是把字符串中的小写字母转换成大写字母即可。

### 继承

**继承（Inheritance）**是令一个获得另一个类的属性和方法，从而不要将代码重写一遍即可获得先前写好的功能，同时对被继承的类进行功能的扩展。被继承的类被称为**父类（Parent Class）**或**基类（Base Class）**、继承其它类的类称为**子类（Child Class）**或**派生类（Derived Class）**。下面看一个简单的例子：

```python
class People:
    def __init__(self, age, gender):
        self.age=age
        self.gender=gender
    def sleep(self):
        print("正在睡觉")

class Shushan(People):
    def __init__(self, age, gender, lezi):
        super.__init__(age,gender)
        self.lezi=lezi
    def le(self):
        print("乐子，，，")
```

在上面的代码中，我们定义了一个People类，其中\_\_init()\_\_是它的构造方法，会在这个类被实例化的时候调用；下面是一个Shushan类，它继承了People类，同时重写了其父类People的构造方法。在子类中，可以通过super()来直接访问父类，上述的写法即是先调用父类的构造方法，再执行自己的构造方法中独有的内容。子类的实例可以直接调用父类的方法，例如下面的写法是合法的：

```python
a=Shushan(20,1,114514) #实例化Shushan类
a.sleep() #调用父类的方法
a.le() #调用子类方法
```

但是父类的实例不能调用子类方法，例如下面的写法是错误的：

```python
kohaku=People(20,xyn)
kohaku.le() #错误！
```

需要注意的是，Python是一个支持多重继承的语言，下列写法可以继承多个父类：

```python
class ChildClass(Parent1, Parent2, Parent3):
    #code
```

多重继承尤其是涉及多层多重继承的时候极易引发一些不可预料的问题，例如如果两个父类具有同名方法，那么子类该继承哪一个方法呢？事实上Python有自己的继承顺序原则能够保证程序不报错，但是运行结果一般不是我们所期待的。

### 多态

**多态（Polymorphism）**是指同一个方法在不同情形下有不同的表现形式，下面看一个例子：

```python
class C1:
    def p(self):
        print("欧内的手，好汉")
class C2:
    def p(self):
        print("阿米诺斯，一个里拉米")

def do(obj):
    obj.p()
    
a=C1()
b=C2()

do(a)
do(b)
```

函数do()执行了传入的obj的p()方法，而此时对于传入的不同的对象，他们的p()方法的含义也不同。需要注意的是，Python没有原生提供**接口（Interface）**，因此通常不会在Python编程中单独提到多态的问题。通常我们使用继承实现类似功能。

## 拓展思考

1. 面向对象编程的五大基本原则：SPR, OCP, LSP, DIP, ISP分别是什么意思，我们如何在编程中实践它们？
2. 在Python的类中，实例方法、类方法、静态方法的定义与调用有什么区别，它们分别适用于什么情形？
3. Python的类中除了\_\_init()\_\_外还有很多特殊方法，它们分别有什么作用？
   - \_\_new()\_\_
   - \_\_slot()\_\_
   - \_\_getitem()\_\_
   - \_\_iter\_\_
   - 其它……？