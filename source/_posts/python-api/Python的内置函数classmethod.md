---
title: Python的内置函数anext
tags: [后端,python,API]
date: 2025-11-16 08:08:08
---

[Python 内建函数列表](https://xplanc.org/primers/document/zh/02.Python/99.API%20%E5%B8%AE%E5%8A%A9%E6%89%8B%E5%86%8C/00.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0.md) \> [Python 的内置函数 classmethod](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.classmethod.md)

Python 的内置函数 [`classmethod`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.classmethod.md) 是一个装饰器，用于将一个方法标记为类方法。类方法属于类本身，而不是类的实例，因此可以在不创建实例的情况下直接通过类名调用。

```python
def classmethod(fn):
    '''
    把一个方法封装成类方法

    :param fn: 要封装的方法
    :return: 封装后的方法
    '''

```

使用 [`@classmethod`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.classmethod.md) 装饰器来定义类方法：

```python
class MyClass:
    @classmethod
    def my_class_method(cls, arg1, arg2):
        # 方法实现
        pass

```

示例：

[运行结果](https://xplanc.org/shift/?lang=python&code=Y2xhc3MlMjBFbXBsb3llZSUzQSUwQSUyMCUyMCUyMCUyMHJhaXNlX2Ftb3VudCUyMCUzRCUyMDEuMDQlMjAlMjAlMjMlMjAlRTclQjElQkIlRTUlOEYlOTglRTklODclOEYlMEElMEElMjAlMjAlMjAlMjBkZWYlMjBfX2luaXRfXyhzZWxmJTJDJTIwbmFtZSUyQyUyMHNhbGFyeSklM0ElMEElMjAlMjAlMjAlMjAlMjAlMjAlMjAlMjBzZWxmLm5hbWUlMjAlM0QlMjBuYW1lJTBBJTIwJTIwJTIwJTIwJTIwJTIwJTIwJTIwc2VsZi5zYWxhcnklMjAlM0QlMjBzYWxhcnklMEElMEElMjAlMjAlMjAlMjAlNDBjbGFzc21ldGhvZCUwQSUyMCUyMCUyMCUyMGRlZiUyMHNldF9yYWlzZV9hbW91bnQoY2xzJTJDJTIwYW1vdW50KSUzQSUwQSUyMCUyMCUyMCUyMCUyMCUyMCUyMCUyMGNscy5yYWlzZV9hbW91bnQlMjAlM0QlMjBhbW91bnQlMjAlMjAlMjMlMjAlRTQlQkYlQUUlRTYlOTQlQjklRTclQjElQkIlRTUlOEYlOTglRTklODclOEYlMEElMEElMjMlMjAlRTQlQkQlQkYlRTclOTQlQTglMEFFbXBsb3llZS5zZXRfcmFpc2VfYW1vdW50KDEuMDUpJTIwJTIwJTIzJTIwJUU3JTlCJUI0JUU2JThFJUE1JUU5JTgwJTlBJUU4JUJGJTg3JUU3JUIxJUJCJUU4JUIwJTgzJUU3JTk0JUE4JTBBZW1wJTIwJTNEJTIwRW1wbG95ZWUoJTIySm9obiUyMiUyQyUyMDUwMDAwKSUwQWVtcC5zZXRfcmFpc2VfYW1vdW50KDEuMDYpJTIwJTIwJTIzJTIwJUU0JUI5JTlGJUU1JThGJUFGJUU0JUJCJUE1JUU5JTgwJTlBJUU4JUJGJTg3JUU1JUFFJTlFJUU0JUJFJThCJUU4JUIwJTgzJUU3JTk0JUE4JUVGJUJDJTg4JUU0JUJEJTg2JUU0JUJGJUFFJUU2JTk0JUI5JUU3JTlBJTg0JUU2JTk4JUFGJUU3JUIxJUJCJUU1JThGJTk4JUU5JTg3JThGJUVGJUJDJTg5JTBBcHJpbnQodmFycyhlbXApKQ%3D%3D)

```python
class Employee:
    raise_amount = 1.04  # 类变量

    def __init__(self, name, salary):
        self.name = name
        self.salary = salary

    @classmethod
    def set_raise_amount(cls, amount):
        cls.raise_amount = amount  # 修改类变量

# 使用
Employee.set_raise_amount(1.05)  # 直接通过类调用
emp = Employee("John", 50000)
emp.set_raise_amount(1.06)  # 也可以通过实例调用（但修改的是类变量）

```

类方法是面向对象编程中一种特殊的方法类型，它属于类本身而非类的实例对象。与普通实例方法不同，类方法在定义时需要使用@classmethod装饰器进行修饰，并且其第一个参数约定俗成命名为cls(指代类本身)，而不是实例方法的self参数。

类方法的主要特点包括：

1. 访问方式：可以直接通过类名调用(如ClassName.method\_name())，无需创建类的实例
2. 应用场景：适合处理与类相关但不依赖于特定实例的操作
3. 参数特点：自动接收类对象作为第一个参数
4. 权限范围：可以访问类属性，但不能直接访问实例属性

常见的使用场景包括：

1. 工厂模式：创建类的替代构造方法  
   * 当需要根据不同的输入参数创建不同类型的对象实例时，可以使用类方法作为工厂方法  
   * 例如：一个图形类可以有类方法 `create_circle()` 和 `create_square()` 来创建特定类型的图形对象  
   * 比直接使用构造函数更灵活，可以封装复杂的对象创建逻辑
2. 类状态的修改：修改所有实例共享的类变量  
   * 当需要修改或访问类的全局状态时，可以使用类方法  
   * 例如：一个计数器类可以用类方法 `increment_count()` 来修改所有实例共享的计数变量  
   * 适用于需要在整个类范围内维护和操作共享数据的情况
3. 工具方法：提供与类相关但不依赖实例的实用功能  
   * 当需要提供与类相关但不需要实例化的功能时，可以使用类方法  
   * 例如：数学计算类可以提供 `convert_units()` 这样的单位转换方法  
   * 日期处理类可以提供 `is_leap_year()` 这样的静态检查方法  
   * 这些方法逻辑上与类相关，但不依赖于具体的实例状态

其他应用场景还包括：

* 替代构造函数（如从不同数据格式创建对象）
* 实现单例模式
* 提供类级别的配置方法
* 执行类相关的预处理或后处理操作

示例：

```python
class Date:
    def __init__(self, year, month, day):
        self.year = year
        self.month = month
        self.day = day
    
    @classmethod
    def from_string(cls, date_string):
        year, month, day = map(int, date_string.split('-'))
        return cls(year, month, day)  # 相当于调用Date(year, month, day)

# 直接通过类调用而不需实例化
date = Date.from_string("2023-05-15")

```

与静态方法的区别：  
 虽然静态方法(@staticmethod)也可以通过类名直接调用，但它不会自动接收类或实例作为参数(self或cls)，更适合完全独立于类和实例的操作。与实例方法必须接收self参数和类方法必须接收cls参数不同，静态方法就像一个被封装在类里的普通函数，既可被类调用，也可被实例调用。

这种特性使静态方法特别适合以下场景：

1. 类中需要实现但不需要访问类或实例状态的辅助功能
2. 将相关功能组织在同一个命名空间下
3. 不需要继承重写的工具方法

[例如](https://xplanc.org/shift/index.html?lang=python&code=Y2xhc3MlMjBNYXRoVXRpbGl0eSUzQSUwQSUyMCUyMCUyMCUyMCU0MHN0YXRpY21ldGhvZCUwQSUyMCUyMCUyMCUyMGRlZiUyMGFkZChhJTJDJTIwYiklM0ElMEElMjAlMjAlMjAlMjAlMjAlMjAlMjAlMjByZXR1cm4lMjBhJTIwJTJCJTIwYiUwQSUyMCUyMCUyMCUyMCUwQSUyMCUyMCUyMCUyMCU0MHN0YXRpY21ldGhvZCUwQSUyMCUyMCUyMCUyMGRlZiUyMGZhY3RvcmlhbChuKSUzQSUwQSUyMCUyMCUyMCUyMCUyMCUyMCUyMCUyMHJldHVybiUyMDElMjBpZiUyMG4lMjAlM0QlM0QlMjAwJTIwZWxzZSUyMG4lMjAqJTIwTWF0aFV0aWxpdHkuZmFjdG9yaWFsKG4tMSklMEElMEElMjMlMjAlRTklODAlOUElRTglQkYlODclRTclQjElQkIlRTUlOTAlOEQlRTglQjAlODMlRTclOTQlQTglMEFwcmludChNYXRoVXRpbGl0eS5hZGQoMiUyQyUyMDMpKSUyMCUyMCUyMyUyMCVFOCVCRSU5MyVFNSU4NyVCQTUlMEFwcmludChNYXRoVXRpbGl0eS5mYWN0b3JpYWwoNSkpJTIwJTIwJTIzJTIwJUU4JUJFJTkzJUU1JTg3JUJBMTIwJTBBJTBBJTIzJTIwJUU5JTgwJTlBJUU4JUJGJTg3JUU1JUFFJTlFJUU0JUJFJThCJUU4JUIwJTgzJUU3JTk0JUE4JTBBY2FsYyUyMCUzRCUyME1hdGhVdGlsaXR5KCklMEFwcmludChjYWxjLmFkZCg1JTJDJTIwNykpJTIwJTIwJTIzJTIwJUU4JUJFJTkzJUU1JTg3JUJBMTI%3D)：

```python
class MathUtility:
    @staticmethod
    def add(a, b):
        return a + b
    
    @staticmethod
    def factorial(n):
        return 1 if n == 0 else n * MathUtility.factorial(n-1)

# 通过类名调用
print(MathUtility.add(2, 3))  # 输出5
print(MathUtility.factorial(5))  # 输出120

# 通过实例调用
calc = MathUtility()
print(calc.add(5, 7))  # 输出12

```

需要注意的是，静态方法虽然方便，但过度使用会影响代码的面向对象特性。静态方法本质上属于函数式编程范式，它们以独立的方式存在，无法访问类或实例的状态（self或cls）。这种特性使得静态方法更适合处理与类相关但不需要类状态的操作，比如数学计算、工具函数等。

以下是一些典型场景的对比：

1. 适合使用静态方法的例子：
* 计算两个日期之间的天数差
* 验证字符串格式是否符合规范
* 生成随机ID等工具函数
1. 应该使用实例方法的例子：
* 需要访问或修改实例属性的操作
* 涉及业务逻辑的状态变更
* 需要多态特性的方法

当方法确实需要访问类或实例状态时，仍应使用实例方法或类方法。比如：

* 需要访问实例属性的方法应定义为实例方法
* 需要访问类级别的配置或状态时应使用类方法
* 需要同时操作实例和类状态时要使用混合方法

过度使用静态方法会导致代码失去面向对象的优势，如继承、多态和封装等特性。合理的做法是根据实际业务需求，在保持代码面向对象特性的前提下适当使用静态方法。

---

> 《[Python 的内置函数 classmethod](https://xplanc.online/bed03a8f1236245a9475988117885ac4442729d2dae03ade08c11ff9f2513cac)》 是转载文章，[点击查看原文](https://blog.csdn.net/IMPYLH/article/details/148598156)。