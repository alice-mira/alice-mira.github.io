---
title: Python学习基础语法
tags: [后端,python]
date: 2025-10-09 08:08:08
---

## 前言——为什么要学习Python

### 原因就一句话：因为AI是主流，要用到Python！

## 注意事项

### 我的第一编程语言是Java，所以学习节奏会很快，不适合小白！

## 一、print函数

### 1\. 语法格式

📌 简单使用

> print(输出内容)

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/073d27fdf5254a4aa4290d65562d3d32.png)

📌 完整使用

> print(self, \*args, sep=’ ‘, end=’\\n’, file=None)

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/0ef2a0a5d3d843da8c7b9d2b0eb39c35.png)

* args：输出的内容；
* sep：间隔符，默认空格
* end：结束符，默认换行
* file：指定输出目标，默认为`sys.stdout`，也可以是一个文件

### 2\. 基础用法详解

#### 🔵 基础打印用法

```python
# 1. 打印单个对象
print("Hello World")                    # 输出: Hello World
print(123)                             # 输出: 123
print([1, 2, 3])                       # 输出: [1, 2, 3]

# 2. 打印多个对象（默认空格分隔）
print("Hello", "World", "!")           # 输出: Hello World !
print(1, 2, 3, 4, 5)                   # 输出: 1 2 3 4 5

# 3. 打印空行
print()                                # 输出空行
print("")                              # 输出空行

```

#### 🔵 分隔符控制（sep参数）

```python
# 4. 无分隔符
print('a', 'b', 'c', sep='')           # 输出: abc

# 5. 自定义分隔符
print('2023', '11', '04', sep='/')     # 输出: 2023/11/04
print('a', 'b', 'c', sep=' → ')        # 输出: a → b → c
print('1', '2', '3', sep=', ')         # 输出: 1, 2, 3

# 6. 特殊字符分隔符
print('line1', 'line2', sep='\n')      # 输出两行内容
print('name', 'value', sep='\t')       # 制表符分隔

```

#### 🔵 行尾控制（end参数）

```python
# 7. 不换行输出
print("Loading", end='')
print("...Done")                       # 输出: Loading...Done

# 8. 自定义行尾
print("Hello", end=' ')               
print("World")                         # 输出: Hello World

print("Question", end='? ')
print("Answer")                        # 输出: Question? Answer

# 9. 多行合并输出
for i in range(3):
    print(f"Item {i}", end=' | ')      # 输出: Item 0 | Item 1 | Item 2 | 
print()  # 最后换行

```

#### 🔵 输出重定向（file参数）

```python
# 10. 输出到文件
import os

print("当前工作目录:", os.getcwd())
# 将内容写入文件
with open('output.txt', 'w') as f:
    print("这是写入文件的内容，默认输出到工作目录", file=f)

with open('D:/log/output.txt', 'w') as file:
    print("这是写入文件的内容，指定输出到D盘某个位置", file=file)

# 11. 输出到标准错误
import sys
print("错误信息", file=sys.stderr)

# 12. 输出到内存缓冲区
from io import StringIO
buffer = StringIO()
print("内存输出", file=buffer)

# 13. 同时输出到多个目标
with open('log.txt', 'w') as f:
    print("日志信息", file=f)           # 写入文件
    print("日志信息")                   # 同时输出到控制台

```

#### 🔵 缓冲控制（flush参数）

```python
# 14. 实时输出（立即刷新）
import time
print("进度:", end='', flush=True)
for i in range(5):
    print('.', end='', flush=True)     # 每个点立即显示
    time.sleep(0.5)

# 15. 缓冲输出（默认）
print("内容", flush=False)             # 可能延迟显示

```

#### 🔵 格式化输出组合

```python
# 16. f-string 格式化
name, age = "Alice", 25
print(f"{name} is {age} years old")    # 输出: Alice is 25 years old

# 17. .format() 方法
print("{} is {} years old".format(name, age))

# 18. % 格式化
print("%s is %d years old" % (name, age))

# 19. 数字格式化
pi = 3.14159
print(f"π ≈ {pi:.2f}")                 # 输出: π ≈ 3.14

```

> 注意：这里的最后一个数字格式化稍微有点难懂，语法不像Java那么严格，扩展如下：

* `f`: 这是最关键的一个符号。它放在字符串的引号之前，标志着这是一个`f-字符串`（formatted string literal，格式化字符串字面量）。它允许我们在字符串中`直接嵌入变量和表达式`，并用花括号 {} 括起来。
* `"..."`: 双引号定义了字符串本身的开始和结束。
* `.2f:` 这是格式说明符，它精确控制了变量pi的显示方式。  
   * `.`: 小数点，表示后面要定义的是小数部分的精度。  
   * `2`: 一个整数，指定要保留的小数位数。这里表示保留2位小数。  
   * `f`: 表示“定点数”（fixed-point）格式。它告诉Python将数字格式化为一个浮点数，并遵循指定的小数位数。它会自动进行四舍五入。
* **不同的格式说明符**：格式说明符 .2f 只是众多选择中的一个。你可以根据需要改变：  
   * **保留3位小数**：{pi:.3f} -> 输出 3.142  
   * **百分比格式**：{0.75:.1%} -> 输出 75.0% （将小数转换为百分比）  
   * **设置总宽度和对齐**：{pi:10.2f} -> 输出 ’ 3.14’ （总宽度为10个字符，默认右对齐）

#### 🔵 高级用法组合

```python
# 20. 所有参数组合使用
with open('result.txt', 'w') as f:
    print(
        "数据1", "数据2", "数据3",      # 多个对象
        sep=" | ",                     # 自定义分隔符  
        end=" → 结束\n",               # 自定义行尾
        file=f,                        # 输出到文件
        flush=True                     # 立即刷新
    )

# 21. 调试输出模板
from datetime import datetime
def debug_print(*args):
    timestamp = datetime.now().strftime("%H:%M:%S")
    print(f"[DEBUG {timestamp}]", *args, flush=True)

debug_print("变量值:", 42)             # 输出: [DEBUG 14:30:25] 变量值: 42

```

#### 🔵 特殊场景用法

```python
# 22. 打印特殊字符
print("换行:\n第二行")                  # 换行符
print("制表符:\t对齐")                  # 制表符
print("反斜杠: \\")                    # 转义字符
print(r"原始字符串: C:\Users")          # 原始字符串

# 23. 打印对象信息
data = {"name": "John", "age": 30}
print("字典内容:", data)                # 输出完整字典
print("类型:", type(data))             # 输出类型信息

# 24. 条件打印
verbose = True
if verbose:
    print("详细模式信息")               # 条件性输出

```

### 3\. print()与内置函数的组合用法

#### 🔵 print() 与字符处理函数

```python
# 25. print(ord()) - 字符转ASCII码
print(ord('A'))        # 输出: 65
print(ord('a'))        # 输出: 97  
print(ord('中'))       # 输出: 20013 (中文字符的Unicode)

# 26. print(chr()) - ASCII/Unicode转字符
print(chr(65))         # 输出: A
print(chr(97))         # 输出: a
print(chr(20013))      # 输出: 中

# 27. 字符转换组合使用
char = 'B'
print(f"字符 '{char}' 的ASCII码是: {ord(char)}")  # 字符 'B' 的ASCII码是: 66

```

#### 🔵 print() 与数学函数

```python
# 28. 数学计算输出
import math
print(abs(-10))                # 输出: 10 (绝对值)
print(pow(2, 3))              # 输出: 8 (2的3次方)
print(round(3.14159, 2))      # 输出: 3.14 (四舍五入)
print(math.sqrt(16))          # 输出: 4.0 (平方根)

# 29. 数学函数组合
print(f"π ≈ {math.pi:.4f}")   # 输出: π ≈ 3.1416
print(f"sin(30°) = {math.sin(math.radians(30)):.2f}")  # 输出: sin(30°) = 0.50

```

#### 🔵 print() 与类型转换函数

```python
# 30. 类型转换输出
print(int("123"))             # 输出: 123
print(float("3.14"))          # 输出: 3.14
print(str(456))               # 输出: 456
print(bool(0))                # 输出: False

# 31. 进制转换
print(hex(255))               # 输出: 0xff (十六进制)
print(oct(64))                # 输出: 0o100 (八进制)  
print(bin(10))                # 输出: 0b1010 (二进制)

```

#### 🔵 print() 与容器函数

```python
# 32. 列表相关
numbers = [1, 2, 3, 4, 5]
print(len(numbers))           # 输出: 5 (长度)
print(max(numbers))           # 输出: 5 (最大值)
print(min(numbers))           # 输出: 1 (最小值)
print(sum(numbers))           # 输出: 15 (求和)

# 33. 排序和反转
print(sorted([3, 1, 4, 2]))   # 输出: [1, 2, 3, 4]
print(list(reversed([1, 2, 3])))  # 输出: [3, 2, 1]

```

#### 🔵 print() 与字符串处理函数

```python
# 34. 字符串操作
text = "Hello World"
print(text.upper())           # 输出: HELLO WORLD
print(text.lower())           # 输出: hello world
print(text.find("World"))     # 输出: 6 (查找位置)
print(text.replace("World", "Python"))  # 输出: Hello Python

# 35. 字符串格式化
name = "Alice"
print("Hello, {}!".format(name))        # 输出: Hello, Alice!
print("Name: {name}, Age: {age}".format(name="Bob", age=25))

```

#### 🔵 print() 与输入函数组合

```python
# 36. 输入输出组合
name = input("请输入您的姓名: ")
print(f"欢迎您, {name}!")

age = int(input("请输入年龄: "))
print(f"明年您将 {age + 1} 岁")

```

#### 🔵 print() 与文件操作函数

```python
# 37. 文件读取后输出
with open('example.txt', 'r') as f:
    content = f.read()
    print(f"文件内容:\n{content}")

# 38. 逐行读取输出
with open('example.txt', 'r') as f:
    print("文件行数:", len(f.readlines()))

```

#### 🔵 print() 与时间日期函数

```python
# 39. 时间日期输出
from datetime import datetime, date, time
print(datetime.now())                    # 当前完整时间
print(date.today())                      # 当前日期
print(time(14, 30, 45))                  # 指定时间

# 40. 时间格式化
now = datetime.now()
print(now.strftime("%Y-%m-%d %H:%M:%S"))  # 输出: 2023-11-04 14:30:25

```

> 扩展：这里的 from datetime import datetime, date, time 怎么理解

* `from`: 这是一个Python关键字，用于声明一个从…导入 语句。它指定了我们要从哪个模块中获取资源。
* `datetime`: 这是紧跟在 from 后面的模块名。Python有一个标准库模块就叫 datetime，它专门用于处理日期和时间。注意：这个 datetime 是模块名。  
 \-` import`: 这是另一个关键字，与 from 配合使用，意思是“导入以下具体内容”。  
   * `date`： 这是 datetime 模块中的一个类，用于表示一个日期（年、月、日），不包含时间。  
   * `time`： 这也是一个类，用于表示一个时间（时、分、秒、微秒），不包含日期。  
   * `datetime`： 这同样是一个类，但它表示一个完整的日期时间（年、月、日、时、分、秒、微秒）。

重要区别： 这里的 datetime（类）与 from datetime（模块）同名。导入后，在代码中直接写 datetime 指的是这个类，而不是模块。

> 怎么选择合适的导入方式？

| 导入方式     | 代码示例                              | 适用场景                                            | 推荐度   |
| -------- | --------------------------------- | ----------------------------------------------- | ----- |
| **联合导入** | from module import ClassA, ClassB | 只使用模块中的少数几个类，且确信无命名冲突。                          | ★★★★☆ |
| **模块别名** | import module as alias            | 频繁使用模块中的多个功能，希望代码简洁清晰。**处理 datetime 模块时的最佳实践。** | ★★★★★ |
| **整体导入** | import module                     | 偶尔使用模块功能，或为避免任何可能的命名冲突。                         | ★★★☆☆ |
| **全部导入** | from module import \*             | 应避免使用。仅在快速交互式测试中可以考虑。                           | ★☆☆☆☆ |

#### 🔵 print() 与高级函数式编程

```python
# 41. map() 函数输出
numbers = [1, 2, 3, 4]
print(list(map(lambda x: x * 2, numbers)))  # 输出: [2, 4, 6, 8]

# 42. filter() 函数输出
print(list(filter(lambda x: x % 2 == 0, numbers)))  # 输出: [2, 4]

# 43. zip() 函数输出
names = ["Alice", "Bob"]
ages = [25, 30]
print(dict(zip(names, ages)))            # 输出: {'Alice': 25, 'Bob': 30}

```

> 注意：这里的高级函数如果会JavaScript的就很熟悉，map中两个参数分别为一个箭头函数和一个执行的对象，如果对Java研究深的伙伴也能发现第一个参数就是一个Lambda表达式。

#### 🔵 print() 与错误处理函数

```python
# 44. 类型检查输出
value = "123"
print(f"类型: {type(value)}")            # 输出: <class 'str'>
print(f"是否是数字: {value.isdigit()}")   # 输出: True

# 45. 异常信息输出
try:
    result = 10 / 0
except Exception as e:
    print(f"错误类型: {type(e).__name__}")  # 输出: ZeroDivisionError
    print(f"错误信息: {e}")                 # 输出: division by zero

```

### 3\. 需要注意的情况

#### ❌ 不允许使用加号拼接数字和字符串

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/761784112a5d4d5181fa1dc07c741683.png)

## 二、input函数

### 1\. 基本用法

#### 🔵 基础输入操作

```python
# 1. 最简单的输入
name = input()                    # 等待用户输入，无提示
print("您输入的是:", name)

# 2. 带提示的输入
name = input("请输入您的姓名: ")   # 显示提示信息
print(f"欢迎, {name}!")

# 3. 多步骤输入
age = input("请输入年龄: ")
city = input("请输入城市: ")
print(f"年龄: {age}, 城市: {city}")

```

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/94838d7dc7be4ecca23fd690341180f5.png)

#### 🔵 输入数据类型处理

```python
# 4. 数字输入（需要类型转换）
# ❌ 错误做法
age = input("请输入年龄: ")
# result = age + 10  # ❌ TypeError: 字符串和数字不能相加

# ✅ 正确做法
age = int(input("请输入年龄: "))    # 转换为整数
result = age + 10                   # ✅ 正常工作
print(f"10年后您将 {result} 岁")

# 5. 浮点数输入
price = float(input("请输入价格: "))
print(f"价格: ￥{price:.2f}")

# 6. 布尔值输入
is_active = input("是否激活 (y/n): ").lower() == 'y'
print(f"激活状态: {is_active}")

```

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/449a98faa89747ffa7155298c212437b.png)

### 2\. 输入验证与错误处理

#### 🔴 输入验证的重要性

```python
# 7. 基本的输入验证
def get_valid_integer(prompt, min_val=0, max_val=100):
    """获取有效的整数输入"""
    while True:
        try:
            value = int(input(prompt))
            if min_val <= value <= max_val:
                return value
            else:
                print(f"请输入 {min_val} 到 {max_val} 之间的数字")
        except ValueError:
            print("请输入有效的数字!")

# 使用示例
age = get_valid_integer("请输入年龄(0-120): ", 0, 120)
print(f"验证通过的年龄: {age}")

```

> 稍微解释一下：这是一个比较简单的输入验证，使用while循环进行不断验证，加上简单的校验，return语句跳出循环，只是这是Python的写法。

#### 🔴 复杂输入验证系统

```python
# 8. 完整的输入验证框架
class InputValidator:
    @staticmethod
    def get_integer(prompt, min_val=None, max_val=None):
        while True:
            try:
                value = int(input(prompt))
                if min_val is not None and value < min_val:
                    print(f"数值不能小于 {min_val}")
                    continue
                if max_val is not None and value > max_val:
                    print(f"数值不能大于 {max_val}")
                    continue
                return value
            except ValueError:
                print("请输入有效的整数!")

    @staticmethod
    def get_float(prompt, min_val=None, max_val=None):
        while True:
            try:
                value = float(input(prompt))
                if min_val is not None and value < min_val:
                    print(f"数值不能小于 {min_val}")
                    continue
                if max_val is not None and value > max_val:
                    print(f"数值不能大于 {max_val}")
                    continue
                return value
            except ValueError:
                print("请输入有效的数字!")

    @staticmethod
    def get_choice(prompt, valid_choices):
        while True:
            choice = input(prompt).strip().lower()
            if choice in valid_choices:
                return choice
            print(f"请输入有效的选择: {', '.join(valid_choices)}")


# 使用验证框架
validator = InputValidator()
age = validator.get_integer("年龄: ", 0, 150)
score = validator.get_float("分数: ", 0, 100)
choice = validator.get_choice("继续吗? (y/n): ", ['y', 'n', 'yes', 'no'])

```

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/314d906fbb0f4684b99ae90862601150.png)

> 解释：这段代码定义了一个验证的类，类中有三个方法，分别是整数的验证输入、浮点数的验证输入、是否继续的命令验证输入，调用的时候类似Java的new 对象，然后对象.方法执行。

### 3\. 高级输入技巧

#### 🔵 多值输入处理

```python
# 9. 一次性输入多个值
data = input("请输入姓名和年龄(用空格分隔): ").split()
if len(data) == 2:
    name, age = data[0], int(data[1])
    print(f"姓名: {name}, 年龄: {age}")

# 10. CSV格式输入
csv_input = input("输入数据(格式: 姓名,年龄,城市): ")
name, age, city = [x.strip() for x in csv_input.split(',')]
print(f"姓名: {name}, 年龄: {age}, 城市: {city}")

# 11. 带默认值的输入
def input_with_default(prompt, default=""):
    result = input(f"{prompt} [{default}]: ").strip()
    return result if result else default

name = input_with_default("请输入姓名", "匿名")
print(f"姓名: {name}")

```

> 这段代码中有一个难点不是很好理解，x.strip() for x in csv\_input.split(‘,’)，解释一下

* 首先它的专业名词叫做：“列表推导式”
* 这一段需要拆分为两部分来看：  
   * 第一部分是`for x in csv_input.split(',')`，这就比较熟悉了，就是一个加强for循环。  
   * 第二部分是`x.strip()`，对每个元素 x 调用 .strip() 方法。该方法会移除字符串首尾的所有空白字符（包括空格、制表符、换行符等）。
* 替代视角

```python
# 分步完成第2行的操作
data_list = csv_input.split(',')       # 第一步：分割字符串
cleaned_list = []                      # 第二步：创建一个新列表用于存放清理后的数据
for item in data_list:
    cleaned_item = item.strip()        # 对每个元素调用 strip()
    cleaned_list.append(cleaned_item)  # 将清理后的元素加入新列表

# 第三步：解包赋值
name, age, city = cleaned_list

```

#### 🔵 密码输入和隐藏

```python
# 12. 密码输入（使用getpass模块）
from getpass import getpass

password = getpass("请输入密码: ")  # 输入时不显示内容
print("密码长度:", len(password))

# 13. 简单的密码确认
def get_confirmed_password():
    while True:
        pwd1 = getpass("设置密码: ")
        pwd2 = getpass("确认密码: ")
        if pwd1 == pwd2:
            if len(pwd1) >= 6:
                return pwd1
            else:
                print("密码长度至少6位")
        else:
            print("两次输入的密码不一致")

# password = get_confirmed_password()

```

> 注意：这段代码最后一行注释掉了，因为这在pycharm环境无法运行，getpass模块是在终端中使用的，这里只是示例。

### 扩展

1. 始终验证输入：不要信任用户输入
2. 处理异常：使用try-except处理转换错误
3. 提供明确提示：告诉用户期望的输入格式
4. 设置超时机制：在需要时添加超时处理
5. 避免代码注入：绝对不要直接执行用户输入

## 三、注释

### 1\. 单行注释

> 单行注释：以井号 # 开头，直到行尾。

```python
# 单行注释
name = "Python"
age = 18
description = "Python单行注释"

```

### 2\. 内联注释

> 内联注释：与代码写在同一行，放在代码之后，同样以 # 开头。

```python
# 单行注释
name = "Python"
age = 18
description = "Python单行注释"  
print("内联注释")   # 这是内联注释

```

### 3\. 多行注释

> 多行注释（块注释）：使用三个连续的单引号 ‘’’ 或双引号 “”" 将注释内容包裹起来。这实际上是利用`未赋值的字符串字面量`。

```python
'''
多行注释，Python中没有明确规定，这是一个普遍约定

推理：当一段字符串字面量没有被赋值给任何变量时，Python解释器会计算它，
      但随后会立即丢弃它，因此不会对程序产生任何影响。
      这被开发者社区广泛采纳为写多行注释的事实标准。
'''


```

### 4\. 特殊注释（Shebang 和 编码声明）

在Unix/Linux/Mac系统下的脚本文件开头，你可能会看到：

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

```

* `#! ...` (Shebang)：这其实不是Python注释，而是给操作系统看的，指定用哪个解释器来执行这个脚本。
* `# -*- coding: ... -*-`：在Python 3中，默认源文件编码是UTF-8，所以通常不需要这行。但在Python 2或使用特殊编码的文件中，它用于声明文件的字符编码，确保解释器能正确读取。

## 四、缩进

💡 注意，在`Python中没有大括号的概念`，都是`基于缩进`进行的代码处理，所以不能随便的加空格！！

### 1\. 缩进规则

* **一致性**：同一代码块内的语句必须使用完全相同数量的缩进。
* **增加缩进**：表示一个新的、更深层级的代码块开始（如 after if, for, while, def, class 等语句的冒号 : 之后）。
* **减少缩进**：表示当前代码块的结束，返回到上一层级的代码块。

### 2\. 示例

正确示例：if 语句

```python
# 正确：缩进清晰地定义了哪些语句属于if分支
if True:
    print("Hello,")   # 属于if块
    print("World!")   # 属于if块
print("This is outside the if block.") # 不属于if块

# 输出：
# Hello,
# World!
# This is outside the if block.

```

错误示例：IndentationError

```python
# 错误：同一代码块内缩进不一致
if True:
    print("Hello,")   # 4个空格
    print("World!")   # 2个空格（会导致运行时错误）

# 运行时会报错：IndentationError: unindent does not match any outer indentation level

```

### 3\. 为什么Python这么在意缩进

💡 Python 对缩进的严格规定源于其核心设计哲学，这直接体现在《Python 之禅》的原则中：**“可读性很重要”** 和 **“明了胜于晦涩”**。将缩进从代码风格提升为语法要求，是这一哲学最彻底的实践。

#### 核心理由

##### 1\. 强制可读性，消除歧义

* **在其他语言（如 C、Java）中：**  
 代码的逻辑结构由大括号 `{}` 定义，而缩进仅是为了美观。这导致一个关键问题：代码的**视觉结构**（对人眼）和**逻辑结构**（对编译器）可能完全脱节。糟糕的缩进会严重误导阅读者，但程序仍能正常运行，埋下理解隐患。但是从另一方面来说，这对编程也有一定的好处，它的可兼容性更强，只不过对于初学者不太友好，如果查看一个不规范的程序猿写的代码会很痛苦。
* **在 Python 中：**  
 视觉结构和逻辑结构被强制绑定。**一段看起来层次分明的 Python 代码，其逻辑结构也必然是清晰的。** 这彻底消除了“代码看起来是这样，但实际运行是那样”的歧义，确保代码对所有阅读者都只有一种唯一、正确的解释。

##### 2\. 减少冗余符号，让代码更简洁

* 大括号 `{}` 和分号 `;` 等符号对于编译器是必要的，但对于人类读者而言是冗余的视觉噪音。
* Python 创新地使用缩进这一种机制，同时解决了“代码块划分”和“代码美观”两个问题。它移除了不必要的符号，让代码更紧凑、更接近纯文本的叙述，从而提升了代码的优雅性和简洁性。

##### 3\. 统一团队编码风格

* 在其他语言中，开发团队常需要为“大括号是否换行”、“缩进用制表符还是空格”、“用几个空格”等问题争论不休，消耗大量精力在风格约定上。
* Python 通过语法直接规定了缩进的重要性，并由官方风格指南 **PEP 8** 明确推荐使用 **4 个空格** 作为标准缩进。这极大地统一了全球 Python 社区的代码风格，使得任何`Python 程序员都能几乎无门槛地阅读和理解他人编写的代码`，极大地提升了协作效率。

## 五、保留字和标识符

💡 这是一个在大多数高级编程语言中都有的一个概念，总的来说就一句话：`标识符可以随便定义，但不能和保留字相同`。

* **保留字**：也被称为关键字，是Python语言本身预先定义好的、具有特殊含义和功能的单词。你不能用它们来作为变量名、函数名或任何其他标识符。
* **标识符**：是由程序员自己定义的名称，用于给变量、函数、类、模块等代码元素命名。
* **关系**：标识符是你可以自由选择的名称，但绝对不能与保留字列表中的名字冲突。

### Python中的保留字

```python
import keyword
print(keyword.kwlist)
print("当前版本关键字共有：", len(keyword.kwlist))  # 当前版本关键字共有： 35

```

> \[  
> ‘False’, ‘None’, ‘True’, ‘and’, ‘as’, ‘assert’, ‘async’, ‘await’, ‘break’, ‘class’, ‘continue’,  
> ‘def’, ‘del’, ‘elif’, ‘else’, ‘except’, ‘finally’, ‘for’, ‘from’, ‘global’, ‘if’, ‘import’, ‘in’, ‘is’,  
> ‘lambda’, ‘nonlocal’, ‘not’, ‘or’, ‘pass’, ‘raise’, ‘return’, ‘try’, ‘while’, ‘with’, ‘yield’  
> \]

### Java中的保留字

> abstract, assert, boolean, break, byte, case, catch, char, class, const, continue, default, do,  
> double, else, enum, extends, final, finally, float, for, goto, if, implements, import, instanceof,  
> int, interface, long, native, new, package, private, protected, public, return, short, static,  
> strictfp, super, switch, synchronized, this, throw, throws, transient, try, void, volatile, while

### 两者的关键字对比

| 类别             | Python 独有关键字                               | Java 独有关键字                                                                                                  | 共有关键字                                 |
| -------------- | ------------------------------------------ | ----------------------------------------------------------------------------------------------------------- | ------------------------------------- |
| **逻辑控制**       | elif, not, or, and                         | switch, case, default, do                                                                                   | if, else, for, while, break, continue |
| **异常处理**       | raise, as (在except中)                       | throws, throw                                                                                               | try, except/catch, finally            |
| **OOP (面向对象)** | \-                                         | new, interface, extends, implements, super, this, public, private, protected, abstract, static, final, void | class, return                         |
| **类型与变量**      | None, True, False, is, global, nonlocal    | 所有基本类型：int, double, boolean…, char, byte, float, long, short, void, enum, volatile, transient, instanceof   | assert                                |
| **函数/方法**      | def, lambda, yield, pass, global, nonlocal | synchronized, native, strictfp                                                                              | \-                                    |
| **模块/包**       | from, import, with, as (在import中)          | package, import                                                                                             | \-                                    |
| **其他**         | del, async, await                          | const, goto                                                                                                 | \-                                    |

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/82586afdc8b1485a91139464a81b0974.png)  
 这里简单的列举了一下两者的区别，说真的，个人还是更喜欢Java，因为它严谨，Python更像是一个继承了很多内部工具的高级编程语言，某方面来说门槛更低，但不可控性又高。

## 六、Python中的变量和常量

### 1\. 结论

💡 Python中没有直接的语法表明变量和常量，不像Java中的`final`关键字可以定义为常量且无法修改，它的底层更像是JavaScript，是一个`动态的类型`，不过在ES6出现后，JavaScript也有了常量的关键字`const`。

### 2\. 变量——动态类型的标签

#### 1\. 变量的创建与赋值

```python
# 变量赋值
name = "Alice"     # 变量name现在指向一个字符串"Alice"
age = 30           # 变量age现在指向一个整数30
score = 95.5       # 变量score现在指向一个浮点数95.5
is_student = True  # 变量is_student现在指向一个布尔值True

```

* Python中没有对变量用保留字修饰，也就是无论你怎么定义和使用，其实都是一个内存地址的引用，底层会基于处理机制不断的进行变化，不需要我们关系堆内存和栈内存等概念。

#### 2\. 变量的动态性

```python
x = 100      # x是整数
print(x)     # 输出: 100

x = "Hello"  # 现在x是字符串
print(x)     # 输出: Hello

x = [1, 2, 3] # 现在x是列表
print(x)     # 输出: [1, 2, 3]

```

* Python中变量可以随时变化类型，这是对`动态性`最核心的诠释。

#### 3\. 多个标签指向同一个对象（重要概念）

```python
a = [1, 2, 3] # a指向一个列表[1, 2, 3]
b = a         # b也指向同一个列表！不是创建副本。
print(a is b) # 输出: True, 证明a和b是同一个对象

b.append(4)   # 通过b修改列表
print(a)      # 输出: [1, 2, 3, 4], a指向的列表也被修改了！

```

* 这是一个容易理解错的概念，因为上面说了是一个内存地址的引用，所以这里a和b都是一个对象，一改两个变量都会进行变化。
* 在Java中我们可以通过new关键字或者一些框架的copy方法来解决这个问题，其实在Python中也有类似的解决方案，而且都是官方提供的方法，从可靠性来说要好一点，就拿上面的例子说明：  
   * 使用切片操作`[:]`(最Pythonic的列表浅拷贝方法)  
   * 使用 [`list() `](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.list.md)构造函数  
   * 使用 copy 模块的 `copy() 函数`（浅拷贝）  
   * 使用 copy 模块的 `deepcopy() `函数（深拷贝）

```python
a = [1, 2, 3]

# 方法1：切片 [:]
b = a[:]       # 创建a的一个浅拷贝副本
# 方法2：list()构造函数
# b = list(a)   # 效果同上
# 方法3：copy.copy()
# import copy
# b = copy.copy(a) # 效果同上

print(a is b)  # 输出: False, 证明a和b现在是两个不同的对象

b.append(4)    # 修改b不会影响a
print(a)       # 输出: [1, 2, 3] (保持不变)
print(b)       # 输出: [1, 2, 3, 4]

```

* **浅拷贝和深拷贝的区别**：这里还是要说明一下，我们在正常使用copy的时候要根据情况进行区分，如果数组中是对象，那必须使用深拷贝，因为我们大多数情况是会改变数组中的对象，如果只是一些基本类型，则可以使用浅拷贝。

### 2\. 常量

#### 1\. 常量的使用

由于Python没有内置常量，社区通过`命名约定来模拟常量`。

* 通常，在模块的顶层（文件开头）定义“常量”。

```python
# constants.py 文件内容
PI = 3.14159
MAX_CONNECTIONS = 100
DATABASE_URL = "postgresql://localhost/mydb"
COMPANY_NAME = "My Awesome Corp"

```

* 或者定义一个常量文件，之后通过导入进行使用，按照约定这是无法更改的。

```python
import constants

radius = 5
area = constants.PI * radius ** 2
print(f"面积是: {area}")

# 程序员约定俗成：不应该这样做！
# constants.PI = 3.14 # 这从技术上可行，但极其糟糕，会破坏程序逻辑。

```

### 3\. 替代视角——常量的保护策略

#### 1\. 强制执行方案

* “常量”的强制执行方案：虽然不常用，但如果你真的需要强制不可变性，可以通过创建类并使用属性（property）来实现。这利用了面向对象的特性来模拟常量行为。

```python
class Constants:
    @property
    def PI(self):
        return 3.14159

const = Constants()
print(const.PI) # 输出: 3.14159
const.PI = 3.14 # 尝试修改会报错: AttributeError: can't set attribute

```

#### 2\. （枚举）模块

```python
from enum import Enum

class Color(Enum):
    RED = 1
    GREEN = 2
    BLUE = 3

print(Color.RED)        # 输出: Color.RED
print(Color.RED.value)  # 输出: 1

# Color.RED = 4 # 这行会报错，枚举成员是不可变的。

```

### 4\. 变量和常量的命名区别

#### 1\. 必须要遵守的四个规范

* 首字符：字母或下划线
* 其余字符：字母、数字、下划线。
* 区分大小写。
* 不能是保留字。

#### 2\. 程序猿约定的规范（蛇形命名）

* **变量**：小写字母和数字的组合，不同单词之间使用下划线`_`连接。

```python
# 好的变量命名 - 清晰地描述了所包含的数据
first_name = "Alice"
user_id = 12345
is_logged_in = True
shopping_cart_total = 99.99
preferred_language_list = ["Python", "English"]

# 在程序运行中，这些变量的值预期会改变
user_id = user_id + 1 # ID增加
is_logged_in = False # 登录状态改变
shopping_cart_total += 10.50 # 购物车总价更新

```

* **常量**：大写字母和数字的组合，不同单词之间使用下划线`_`连接。

```python
# 在程序开头或单独的config.py文件中定义“常量”
# 这些值在程序逻辑中应被视为不可变的

# 数学常数
PI = 3.141592653589793
SPEED_OF_LIGHT = 299792458  # m/s

# 应用程序配置
MAX_FILE_SIZE = 10485760    # 10MB
DATABASE_CONNECTION_STRING = "postgresql://user:pass@localhost/db"
SUPPORTED_LANGUAGES = ("en", "zh", "es") # 使用元组更强调不可变性

# 业务逻辑常量
STATUS_DRAFT = "draft"
STATUS_PUBLISHED = "published"
DEFAULT_PAGE_SIZE = 20

# 在程序逻辑中使用
radius = 5
circumference = 2 * PI * radius # 使用常量，清晰且不易出错

# 程序员约定：不应该这样做！尽管语法上允许。
# PI = 3.14 # 这行代码不会报错，但破坏了约定，是糟糕的做法。

```

## 七、数值类型

### 1\. 核心的三种内置类型

* **整数** (int)：表示正整数、负整数和零。在Python 3中，int是任意精度的，意味着它的大小只受内存限制。
* **浮点数** (float)：表示实数，即带小数点的数。它遵循IEEE 754双精度标准，有精度限制，可能导致舍入误差。
* **复数** (complex)：表示形式为 a + bj 的数，其中 a 和 b 是浮点数，j 是虚数单位。

#### 1.1 整数

* 任意精度

```python
# 小整数
a = 10
# 大整数（在其他语言中可能溢出）
big_num = 123456789012345678901234567890
print(big_num) # 正常输出
print(type(big_num)) # <class 'int'>

```

* 进制表示

```python
bin_num = 0b1010  # 二进制，等于十进制的10
oct_num = 0o12    # 八进制，等于十进制的10
hex_num = 0xA     # 十六进制，等于十进制的10

```

#### 1.2 浮点数

* **精度限制与舍入误差**：由于使用固定数量的比特位存储，浮点数无法精确表示所有十进制小数。这是最重要的概念。

```python
# 经典的浮点数精度问题
result = 0.1 + 0.2
print(result) # 输出：0.30000000000000004，而不是0.3
print(0.1 + 0.2 == 0.3) # 输出：False！

```

* **科学计数法**：支持使用 e 或 E 表示。

```python
avogadro = 6.022e23  # 阿伏伽德罗常数
tiny_num = 1.6e-35   # 普朗克长度（近似）

```

#### 1.3 复数

```python
c = 3 + 4j        # 注意是 j，不是数学中的 i
print(c.real)     # 输出实部：3.0
print(c.imag)     # 输出虚部：4.0
print(abs(c))     # 输出模：5.0 (勾股定理)

```

### 2\. 专业的数值类型

#### 2.1 decimal类型（相当于Java中的BigDecimal类）

```python
from decimal import Decimal
# 使用字符串初始化以避免初始的浮点误差
exact_result = Decimal('0.1') + Decimal('0.2')
print(exact_result) # 输出：0.3
print(exact_result == Decimal('0.3')) # 输出：True

```

#### 2.2 fractions类型

```python
from fractions import Fraction
f = Fraction(1, 3) # 表示三分之一
print(f) # 输出：1/3
print(float(f)) # 输出：0.3333333333333333 (近似值)
result_frac = Fraction(1, 3) + Fraction(1, 6)
print(result_frac) # 精确输出：1/2

```

### 3\. 不同数值类型之间的对比

| 特性         | 整数 (int)   | 浮点数 (float)     | 复数 (complex) | Decimal        | Fraction       |
| ---------- | ---------- | --------------- | ------------ | -------------- | -------------- |
| **主要用途**   | 计数、索引、离散数学 | 科学计算、测量、连续值     | 电气工程、数学物理    | 金融、货币计算        | 有理数运算、精确比例     |
| **精度**     | 任意精度（精确）   | 约15-17位有效数字（近似） | 实部和虚部为浮点精度   | 用户自定义精度（精确）    | 精确（分子分母为整数）    |
| **内存占用**   | 随数字增大而增加   | 固定（通常64位）       | 固定（两个浮点数）    | 大于基本类型         | 大于基本类型         |
| **速度**     | 快（对于小整数）   | 非常快（硬件优化）       | 快            | 较慢             | 较慢             |
| **是否精确**   | 是          | 否（有舍入误差）        | 实部虚部不精确      | 是              | 是              |
| **关键字/构造** | 123        | 123.45, 1.23e2  | 3+4j         | Decimal('0.1') | Fraction(1, 3) |

## 八、字符串类型

### 1\. 字符串的不同表现形式

* **单引号**: ‘hello’
* **双引号**: “hello”
* **三引号**（块字符串）: ‘’‘hello’‘’ 或 “”“hello”“”

这里我们着重注意三引号的作用：`保留字符串中的所有缩进等格式`。

```python
multi_line_text = """这是一个多行字符串。
这是第二行。
    这是第三行，前面有缩进。
"""
print(multi_line_text)

```

输出如下：

```python
这是一个多行字符串。
这是第二行。
    这是第三行，前面有缩进。

```

### 2\. 字符的不可变性

> 字符串是不可变的。这意味着一旦创建，就不能修改其中的某个字符。

💡 注意，这里说的不可变性是指一个字符串在底层中是不能修改的，在Java中有一个常量池，其中使用了享元模式对字符串进行了管理，加大了系统的运行速度，这和Python中底层处理机制是一样的。

```python
my_string = "hello"
# my_string[0] = 'H' # 这行会报错：TypeError: 'str' object does not support item assignment

# 正确的“修改”方式是创建一个新的字符串
new_string = 'H' + my_string[1:] # 拼接操作
print(new_string) # 输出: Hello
print(my_string)  # 输出: hello (原字符串未被改变)

```

### 3\. 字符串的序列操作

```python
text = "Python"

# 索引 (从0开始)
print(text[0])   # 输出: P (第一个字符)
print(text[-1])  # 输出: n (最后一个字符，负索引从右向左)

# 切片 [start:end:step] (包含start，不包含end)
print(text[0:2])  # 输出: Py (获取索引0到1的字符)
print(text[2:])   # 输出: thon (从索引2到末尾)
print(text[:4])   # 输出: Pyth (从开头到索引3)
print(text[::2])  # 输出: Pto (从头到尾，步长为2)
print(text[::-1]) # 输出: nohtyP (反转字符串，一个非常巧妙的技巧！)

```

| 操作类型                       | 示例                                                                          | 说明        | 与数值类型的对比          |
| -------------------------- | --------------------------------------------------------------------------- | --------- | ----------------- |
| **拼接 (+)**                 | "Hello" + " " + "World"                                                     | 连接字符串。    | 数值 + 是数学加法。       |
| **重复 (\*)**                | "Ha" \* 3 \-> "HaHaHa"                                                      | 重复字符串。    | 数值 \* 是数学乘法。      |
| **成员检查 (in)**              | "Py" in "Python" \-> True                                                   | 检查子串是否存在。 | 用于检查元素是否在列表/集合中。  |
| **常用方法**                   |                                                                             |           |                   |
| .upper() / .lower()        | "Hello".upper() \-> "HELLO"                                                 | 大小写转换。    | 数值类型没有此类方法。       |
| .strip()                   | " hello ".strip() \-> "hello"                                               | 去除首尾空白字符。 | 用于数据清洗。           |
| .split() / .join()         | "a,b,c".split(",") \-> \['a','b','c'\]",".join(\['a','b','c'\]) \-> "a,b,c" | 分割与合并。    | 极其重要，用于字符串与列表的转换。 |
| .find() / .index()         | "apple".find("p") \-> 1                                                     | 查找子串位置。   |                   |
| \`.format() / f-string\*\* | f"{name} is {age} years old."                                               | 现代字符串格式化。 | 数值会被自动转换为字符串。     |

### 4\. 现代常用的字符串表现形式

```python
name = "Alice"
age = 30
score = 95.5

# 1. 基本用法（推荐！）
message = f"{name} is {age} years old and scored {score} points."
print(message) # Alice is 30 years old and scored 95.5 points.

# 2. 在表达式内进行计算和调用函数
message = f"Next year, {name} will be {age + 1} years old."
print(message) # Next year, Alice will be 31 years old.

# 3. 格式化数字（与数值类型交互的重点）
pi = 3.1415926535
# 保留两位小数
print(f"Pi is approximately {pi:.2f}") # Pi is approximately 3.14
# 格式化为百分比
print(f"Your score is {score/100:.1%}") # Your score is 95.5%
# 设置宽度和对齐
print(f"|{name:>10}|") # |     Alice| (右对齐，宽度10)

```

💡 注意这里的表现形式很像JavaScript中ES6的一种写法（const a = “a + ${b}”），这确实是一个非常方便的写法，简化了我们的编程，但可读性稍差。

## 九、布尔类型

### 1\. 最基础的了解

* True：表示逻辑“真”。
* False：表示逻辑“假”。
* bool 类型是整数类型 (int) 的子类。这意味着在数值上下文中，**True 等价于 1，False 等价于 0**。

### 2\. bool（）函数的应用

```python
# 显式转换
print(bool(1))     # True
print(bool(0))     # False
print(bool("Hello")) # True
print(bool(""))    # False
print(bool([1, 2])) # True
print(bool([]))    # False

```

### 3\. 布尔运算符

#### 1\. 基础运算符

* **and**：逻辑与。只有左右两边都为 True，结果才为 True。
* **or**：逻辑或。只要左右两边有一个为 True，结果就为 True。
* **not**：逻辑非。取反。

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/8b765553c47c4957ae3cbd6b3c20fcfa.png)

#### 2\. 短路计算

> Python的布尔运算符是“短路”的。这意味着表达式从左向右求值，一旦结果明确，就会立即停止。

```python
def is_ready():
    print("Function was called!")
    return True

# 因为 False and ... 的结果一定是 False，所以 is_ready() 不会被调用
result1 = False and is_ready() # 输出：无 （函数未被调用）

# 因为 True or ... 的结果一定是 True，所以 is_ready() 也不会被调用
result2 = True or is_ready()   # 输出：无 （函数未被调用）

# 只有在必要时才会计算右边的表达式
result3 = True and is_ready() # 输出：Function was called!
result4 = False or is_ready() # 输出：Function was called!

```

#### 3\. 布尔类型是整数的子类

```python
# 验证 bool 是 int 的子类
print(issubclass(bool, int)) # 输出：True

# 在算术运算中，True 和 False 被当作 1 和 0
print(True + True)   # 输出：2 (1 + 1)
print(False * 10)    # 输出：0 (0 * 10)
print(sum([True, False, True])) # 输出：2 (统计列表中 True 的个数，非常实用！)

# 甚至可以这样（但不推荐，影响可读性）
my_list = ['a', 'b', 'c']
print(my_list[True])  # 输出：'b' (等价于 my_list[1])

```

## 十、类型转换函数

### 1\. 隐式转换

💡 隐式转换指的是在程序运行过程中自动发生的类型转换，和Java中一样，整数和浮点数相加最后输出肯定是浮点数，但其实隐式转换的概念和Java中的自动装箱和自动拆箱理解起来方便一些，总的就是两个字`自动`。

```python
# 示例1：整数与浮点数相加
result = 5 + 3.14
# 1. Python发现整数(5)和浮点数(3.14)相加
# 2. 根据数值类型层次，将整数转换为浮点数：float(5) → 5.0
# 3. 执行操作：5.0 + 3.14 = 8.14
print(result)  # 输出：8.14
print(type(result))  # 输出：<class 'float'>

# 示例2：布尔值与整数运算
result = True + 10
# 1. Python发现布尔值(True)和整数(10)相加
# 2. 将布尔值转换为整数：int(True) → 1
# 3. 执行操作：1 + 10 = 11
print(result)  # 输出：11

# 示例3：不同数值类型的比较
result = 10 == 10.0
# 1. Python比较整数(10)和浮点数(10.0)
# 2. 将整数转换为浮点数：float(10) → 10.0
# 3. 执行比较：10.0 == 10.0 → True
print(result)  # 输出：True

```

> 需要注意的是，无论是在哪个高级语言中，都不提倡进行这种隐式转换，因为极有可能出现类型转换错误，不可控性比较高。

### 2\. 显式转换

💡 这就是通过一些函数和方法对变量进行直接和明显的类型转换，具体可分为以下几种：  
 💡 具体的就不解释过多了，根据函数名我们大部分都可以理解

| 函数       | 描述              | 输入示例             | 输出示例                    |
| -------- | --------------- | ---------------- | ----------------------- |
| [`int(x)`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.int.md)   | 将x转换为整数         | int("123")       | 123                     |
| [`float(x)`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.float.md) | 将x转换为浮点数        | float("3.14")    | 3.14                    |
| [`str(x)`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.str.md)   | 将x转换为字符串        | str(123)         | "123"                   |
| [`bool(x)`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.bool.md)  | 将x转换为布尔值        | bool(0)          | False                   |
| [`list(x)`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.list.md)  | 将x转换为列表         | list("hello")    | \['h','e','l','l','o'\] |
| [`tuple(x)`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.tuple.md) | 将x转换为元组         | tuple(\[1,2,3\]) | (1,2,3)                 |
| [`set(x)`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.set.md)   | 将x转换为集合         | set(\[1,2,2,3\]) | {1,2,3}                 |
| [`ord(x)`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.ord.md)   | 获取字符的Unicode码点  | ord('A')         | 65                      |
| [`hex(x)`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.hex.md)   | 将整数转换为十六进制字符串   | hex(255)         | '0xff'                  |
| [`oct(x)`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.oct.md)   | 将整数转换为八进制字符串    | oct(64)          | '0o100'                 |
| [`bin(x)`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.bin.md)   | 将整数转换为二进制字符串    | bin(42)          | '0b101010'              |
| [`chr(x)`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.chr.md)   | 将Unicode码点转换为字符 | chr(65)          | 'A'                     |

```python
# 基础类型转换示例
print("=== 基础类型转换 ===")
print(f"int('123'): {int('123')}")
print(f"float('3.14'): {float('3.14')}")
print(f"str(456): '{str(456)}'")
print(f"bool(0): {bool(0)}, bool(1): {bool(1)}")

print("\n=== 容器类型转换 ===")
print(f"list('hello'): {list('hello')}")
print(f"tuple([1,2,3]): {tuple([1,2,3])}")
print(f"set([1,2,2,3]): {set([1,2,2,3])}")

print("\n=== 数值表示转换 ===")
print(f"hex(255): {hex(255)}")
print(f"oct(64): {oct(64)}")
print(f"bin(42): {bin(42)}")

print("\n=== 字符编码转换 ===")
print(f"ord('A'): {ord('A')}")
print(f"chr(65): '{chr(65)}'")

print("\n=== 实际应用场景 ===")
# 数据清洗
user_input = " 123 "
clean_number = int(user_input.strip())
print(f"清洗后的数字: {clean_number}")

# 字符串处理
numbers = [1, 2, 3]
result = ", ".join(str(x) for x in numbers)
print(f"列表转字符串: {result}")

# 快速去重
data = [1, 2, 2, 3, 3, 3]
unique_data = list(set(data))
print(f"去重后的数据: {unique_data}")

```

## 十一、eval函数

💡 这也是显式转换函数的一种，但为什么要单独来讲是因为它的独特性。

> 定义：[`eval()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.eval.md) 是一个内置函数，用于`执行一个字符串表达式`，并返回表达式的值。它能够将`字符串当作有效的Python表达式来求值`。

### 1\. 基本语法

```python
eval(expression, globals=None, locals=None)

```

* **expression**：字符串，包含要计算的Python表达式
* **globals**：可选，字典，指定全局命名空间
* **locals**：可选，映射对象，指定局部命名空间

### 2\. 基本使用

```python
# 简单的数学表达式
result = eval("2 + 3 * 4")
print(result)  # 输出: 14

# 使用变量（在当前作用域中查找）
x = 10
y = 20
result = eval("x + y")
print(result)  # 输出: 30

# 函数调用
result = eval("len([1, 2, 3, 4])")
print(result)  # 输出: 4

# 布尔表达式
result = eval("10 > 5 and 'a' in 'apple'")
print(result)  # 输出: True

```

### 3\. 与 exec() 的区别

| 特性   | eval()            | exec()                           |
| ---- | ----------------- | -------------------------------- |
| 返回值  | 返回表达式的计算结果        | 总是返回 None                        |
| 输入类型 | 单个表达式（字符串）        | 代码块、语句组（字符串）                     |
| 语法要求 | 必须是有效的Python表达式   | 必须是有效的Python语句                   |
| 适用场景 | 计算数学表达式、简单逻辑判断    | 执行复杂的代码块、动态定义函数/类                |
| 安全性  | 高风险（执行任意代码）       | 高风险（执行任意代码）                      |
| 性能   | 相对较快（解析表达式）       | 相对较慢（编译和执行代码块）                   |
| 示例   | [`eval("1 + 1")`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.eval.md) → 2 | [`exec("x = 1 + 1")`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.exec.md) → `None`（但创建变量x） |

**代码示例：**

```python
# eval() - 用于表达式，有返回值
expression_result = eval("2 + 3")
print(expression_result)  # 输出: 5

# exec() - 用于语句，无返回值
exec("x = 2 + 3")
print(x)  # 输出: 5

# eval() 不能执行语句
# eval("x = 2 + 3")  # 这会报错：SyntaxError

```

### 4\. 命名空间控制（globals 和 locals 参数）

💡 这是 [`eval()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.eval.md) 的安全特性，可以**限制可访问的变量和函数**。

> 注意：为什么要存在这两个参数，从上面的描述中我们可以看到，它可以执行用户输入的字符串信息，而且权限相当大，如果任由其执行那结果就非常不可控了，所以自带了两个安全控制的参数，比如下面的代码：

```python
# 危险！用户可以执行任意代码
user_input = "__import__('os').system('rm -rf /')"  # 删除系统文件！
# eval(user_input)  # 千万不要执行这个！

# 其他危险操作：
# - 读取敏感文件：eval("open('/etc/passwd').read()")
# - 安装恶意软件
# - 消耗所有内存：eval("[] * 10**9")
# - 无限循环消耗CPU

```

**参数使用示例**：

```python
# 限制全局命名空间
x = 10
safe_globals = {'x': 5, 'y': 3}  # 只允许访问这些变量

# 使用受限的命名空间
result = eval("x + y", safe_globals)
print(result)  # 输出: 8

# 尝试访问外部变量会失败
# result = eval("x + y", {})  # 这会报错：NameError，因为x和y未定义

# 完全禁用内置函数
restricted_globals = {"__builtins__": {}}  # 空字典，禁用所有内置函数
# eval("print('hello')", restricted_globals)  # 报错：NameError，print未定义

```

### 5\. 更加安全的方案

#### 1\. 使用literal\_eval()

ast.literal\_eval() 只能评估字面量表达式，不能执行函数或方法

```python
from ast import literal_eval

# 安全地评估基本数据结构
safe_result = literal_eval("[1, 2, 3]")
print(safe_result)  # 输出: [1, 2, 3]

safe_result = literal_eval("{'key': 'value'}")
print(safe_result)  # 输出: {'key': 'value'}

# 尝试执行函数会失败
# literal_eval("__import__('os').system('ls')")  # 报错：ValueError

```

#### 2\. 使用解析器或专用库

```python
# 使用 numexpr 用于数值表达式（更安全、更快）
# pip install numexpr
import numexpr as ne

result = ne.evaluate("2 * x + y", local_dict={'x': 5, 'y': 3})
print(result)  # 输出: 13

```

## 十二、算术运算符

| 运算符  | 名称   | 描述                | 示例       | 结果   | 支持的数据类型             |
| ---- | ---- | ----------------- | -------- | ---- | ------------------- |
| +    | 加法   | 两个数相加             | 5 + 3    | 8    | 数字、字符串、列表、元组        |
| \-   | 减法   | 两个数相减             | 10 - 4   | 6    | 数字                  |
| \*   | 乘法   | 两个数相乘             | 6 \* 7   | 42   | 数字、字符串、列表、元组        |
| /    | 除法   | 两个数相除，返回浮点数       | 15 / 4   | 3.75 | 数字                  |
| //   | 整除   | 两个数相除，向下取整        | 15 // 4  | 3    | 数字                  |
| %    | 取模   | 返回除法的余数           | 15 % 4   | 3    | 数字                  |
| \*\* | 幂运算  | 返回x的y次幂           | 2 \*\* 3 | 8    | 数字                  |
| @    | 矩阵乘法 | 矩阵相乘（Python 3.5+） | A @ B    | 矩阵乘积 | 支持\_\_matmul\_\_的对象 |

```python
# 基本算术运算
a, b = 10, 3

print(f"{a} + {b} = {a + b}")   # 输出: 10 + 3 = 13
print(f"{a} - {b} = {a - b}")   # 输出: 10 - 3 = 7
print(f"{a} * {b} = {a * b}")   # 输出: 10 * 3 = 30
print(f"{a} / {b} = {a / b}")   # 输出: 10 / 3 = 3.3333333333333335
print(f"{a} // {b} = {a // b}") # 输出: 10 // 3 = 3 (整除，向下取整)
print(f"{a} % {b} = {a % b}")   # 输出: 10 % 3 = 1 (取余数)
print(f"{a} ** {b} = {a ** b}") # 输出: 10 ** 3 = 1000 (幂运算)

```

### 1\. 算术优先级

| 优先级 | 运算符          | 描述        | 结合性  |
| --- | ------------ | --------- | ---- |
| 1   | \*\*         | 幂运算       | 从右到左 |
| 2   | +x, \-x, \~x | 一元正负、按位取反 | 从右到左 |
| 3   | \*, /, //, % | 乘、除、整除、取模 | 从左到右 |
| 4   | +, \-        | 加、减       | 从左到右 |

## 十三、赋值运算符

| 运算符   | 名称     | 描述            | 等价形式         | 示例        | 运算后值         |
| ----- | ------ | ------------- | ------------ | --------- | ------------ |
| \=    | 基本赋值   | 将右侧值赋给左侧变量    | x = value    | x = 5     | x = 5        |
| +=    | 加法赋值   | 将左右两边相加后赋给左边  | x = x + y    | x += 3    | x = x + 3    |
| \-=   | 减法赋值   | 将左右两边相减后赋给左边  | x = x - y    | x -= 2    | x = x - 2    |
| \*=   | 乘法赋值   | 将左右两边相乘后赋给左边  | x = x \* y   | x \*= 4   | x = x \* 4   |
| /=    | 除法赋值   | 将左右两边相除后赋给左边  | x = x / y    | x /= 2    | x = x / 2    |
| //=   | 整除赋值   | 将左右两边整除后赋给左边  | x = x // y   | x //= 3   | x = x // 3   |
| %=    | 取模赋值   | 将左右两边取模后赋给左边  | x = x % y    | x %= 5    | x = x % 5    |
| \*\*= | 幂赋值    | 将左右两边幂运算后赋给左边 | x = x \*\* y | x \*\*= 2 | x = x \*\* 2 |
| &=    | 按位与赋值  | 按位与运算后赋值      | x = x & y    | x &= 3    | x = x & 3    |
| \|=   | 按位或赋值  | 按位或运算后赋值      | x = x \| y   | x \|= 1   | x = x \| 1   |
| ^=    | 按位异或赋值 | 按位异或运算后赋值     | x = x ^ y    | x ^= 2    | x = x ^ 2    |
| <<=   | 左移赋值   | 左移位运算后赋值      | x = x << y   | x <<= 1   | x = x << 1   |
| \>>=  | 右移赋值   | 右移位运算后赋值      | x = x >> y   | x >>= 1   | x = x >> 1   |

> 重点看一下最后几个位运算符即可！

## 十四、比较运算符

| 运算符    | 名称    | 描述              | 示例         | 结果      |
| ------ | ----- | --------------- | ---------- | ------- |
| \==    | 等于    | 检查两个值是否相等       | 5 == 5     | True    |
| !=     | 不等于   | 检查两个值是否不相等      | 5 != 3     | True    |
| \>     | 大于    | 检查左值是否大于右值      | 5 > 3      | True    |
| <      | 小于    | 检查左值是否小于右值      | 5 < 3      | False   |
| \>=    | 大于等于  | 检查左值是否大于或等于右值   | 5 >= 5     | True    |
| <=     | 小于等于  | 检查左值是否小于或等于右值   | 5 <= 3     | False   |
| is     | 身份相等  | 检查两个对象是否是同一个对象  | x is y     | 取决于对象ID |
| is not | 身份不相等 | 检查两个对象是否不是同一个对象 | x is not y | 取决于对象ID |

### 1\. 字符串比较

```python
# 字符串按字典序比较
print("apple" == "apple")    # 输出: True
print("apple" == "Apple")    # 输出: False（区分大小写）
print("apple" != "orange")   # 输出: True
print("apple" > "banana")    # 输出: False（'a'在'b'之前）
print("apple" < "banana")    # 输出: True

# 实际应用：姓名排序
names = ["Alice", "Bob", "Charlie", "David"]
sorted_names = sorted(names)
print(sorted_names)  # 输出: ['Alice', 'Bob', 'Charlie', 'David']

```

### 2\. is 与 == 的重要区别

```python
# 对于小整数和短字符串，Python会缓存（驻留）
a = 256
b = 256
print(a == b)  # 输出: True（值相等）
print(a is b)  # 输出: True（是同一个对象，因为小整数缓存）

a = 257
b = 257
print(a == b)  # 输出: True（值相等）
print(a is b)  # 输出: False（不是同一个对象）

# 列表总是不同的对象
list1 = [1, 2, 3]
list2 = [1, 2, 3]
print(list1 == list2)  # 输出: True（内容相同）
print(list1 is list2)  # 输出: False（不同对象）

```

### 3\. is 的典型用法

```python
# 检查是否为None（总是用is，不要用==）
value = None
if value is None:
    print("值为空")  # 输出: 值为空

if value is not None:
    print("值不为空")

# 检查布尔值
flag = True
if flag is True:    # 等同于 if flag:
    print("标志为真")

if flag is False:   # 等同于 if not flag:
    print("标志为假")

```

## 十五、逻辑运算符

| 运算符 | 名称  | 描述                 | 真值表                                                                                     | 示例                  | 结果    |
| --- | --- | ------------------ | --------------------------------------------------------------------------------------- | ------------------- | ----- |
| and | 逻辑与 | 两个条件都为True时返回True  | True and True → TrueTrue and False → FalseFalse and True → FalseFalse and False → False | (5 > 3) and (2 < 4) | True  |
| or  | 逻辑或 | 至少一个条件为True时返回True | True or True → TrueTrue or False → TrueFalse or True → TrueFalse or False → False       | (5 > 3) or (2 > 4)  | True  |
| not | 逻辑非 | 反转条件的逻辑值           | not True → Falsenot False → True                                                        | not (5 > 3)         | False |

## 总结

💡 这一章讲解了基本的Python知识点，虽然大部分和Java是重合的，但是有一些语法和写法还是需要我们好好了解一下。

💡 OK，下一章我们继续程序的描述方式，也就是一些基本的判断和for循环等操作。

---

本文是转载文章，[点击查看原文](https://blog.csdn.net/weixin_48588897/article/details/152092464)。