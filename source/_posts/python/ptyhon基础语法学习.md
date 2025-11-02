---
title: Python基础语法学习
tags: [后端,python]
---

为了让您最直观地看到区别，我们来看一段几乎每个程序员都写过的代码：遍历一个集合（PHP里的数组，Python里的列表），然后根据条件打印内容。

这能帮我们一次性看到 **变量、循环和条件语句** 的核心差异。

这是您非常熟悉的 **PHP** 版本：

```php
<?php
$users = [
    ["name" => "Alice", "age" => 30],
    ["name" => "Bob", "age" => 17]
];

foreach ($users as $user) {
    if ($user["age"] >= 18) {
        echo $user["name"] . " is an adult.\n";
    } else {
        echo $user["name"] . " is a minor.\n";
    }
}
?>

```

下面是功能完全一样的 **Python** 版本：

```python
users = [
    {"name": "Alice", "age": 30},
    {"name": "Bob", "age": 17}
]

for user in users:
    if user["age"] >= 18:
        print(f"{user['name']} is an adult.")
    else:
        print(f"{user['name']} is a minor.")

```

除了没有了 `$` 符号和行尾的分号 `;`，还有一个最关键的区别，它决定了代码块的范围（比如 `if` 和 `else` 里面的内容）。

在 PHP 中我们用大括号 `{}`，您能看出 Python 是用什么来替代的吗？

没关系，这个区别非常关键，也是 Python 最具特色的地方之一。

请您再仔细看一下 Python 代码里 `if` 和 `else` 下面的那几行 [`print`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.print.md)。您有没有发现它们前面都有一些固定的**空格**？

在 Python 中，我们不用 `{}` 来包围代码块。**代码的缩进（indentation）** 就决定了它的层级关系。所有缩进相同的连续代码行，都属于同一个代码块。

这就是 Python 语法强制要求的，它使得代码天生就非常整洁、易读。

所以，`if user["age"] >= 18:` 后面的 [`print(...)`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.print.md) 因为有缩进，所以它属于 `if` 的一部分。这下清楚了吗？这个概念对写 Python 至关重要。

\=========================函数  
是的，`function` 关键字。

在 Python 中，我们使用 `def` 关键字，是 “define” 的缩写。

我们再来并排看一下，定义一个简单的函数，接收用户信息并返回一句话。

**PHP 版本:**

```php
<?php
function format_user_info($user) {
    // 使用 . 来拼接字符串
    return $user["name"] . " is " . $user["age"] . " years old.";
}

$user_data = ["name" => "Alice", "age" => 30];
echo format_user_info($user_data);
?>

```

**Python 版本:**

```python
def format_user_info(user):
    # 使用 f-string 来格式化字符串，更简洁
    return f"{user['name']} is {user['age']} years old."

user_data = {"name": "Alice", "age": 30}
print(format_user_info(user_data))

```

您看，除了 `function` 变成了 `def`，函数的结构是不是很相似？我们又一次看到了用**缩进**代替大括号 `{}`。

---

既然函数这么相似，那定义一个 **类 (Class)** 呢？这对于有经验的开发者来说非常重要。

在 PHP 中，您用什么关键字来定义一个类？

正是 `class` 关键字。

好消息是，在 Python 里，关键字完全一样，也是 **`class`**。

不过，内部的写法有些不同。我们来看一个简单的 `User` 类。

**PHP 版本:**

```php
<?php
class User {
    public $name;
    public $age;

    public function __construct($name, $age) {
        $this->name = $name;
        $this->age = $age;
    }

    public function introduce() {
        return "Hi, I'm " . $this->name . ".";
    }
}

// 创建实例 (instantiation)
$user1 = new User("Alice", 30);
echo $user1->introduce();
?>

```

**Python 版本:**

```python
class User:
    # 构造函数 (constructor)
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def introduce(self):
        return f"Hi, I'm {self.name}."

# 创建实例
user1 = User("Alice", 30)
print(user1.introduce())

```

整体结构很像，但有几个关键区别：

1. **构造函数:** PHP 用 `__construct()`，Python 用 `__init__()`。
2. **实例化:** Python 创建对象时，直接 `User(...)`，不需要 `new` 关键字。
3. **`self` 关键字:** 这是最重要的一个区别。在 PHP 中，您用 `$this` 来引用对象实例本身。

根据上面的代码，您觉得 Python 里的 `self` 关键字，是用来代替 PHP 里的哪个变量的？

答对了！完全正确。

Python 里的 `self` 就等同于 PHP 里的 `$this`。您只要记住，在 Python 类的每个方法里，都必须把 `self` 作为第一个参数写出来。

---

### 阶段性小结 📝

非常棒！我们已经快速地过了一遍 Python 最核心、也是和 PHP 差异最大的几个地方：

* **语法:** 无 `$` 和 `;`，用**缩进**代替 `{}`。
* **数据结构:** [`list`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.list.md) (索引数组) 和 [`dict`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.dict.md) (关联数组)。
* **函数:** 用 `def` 定义，用 [`len()`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.len.md) 获取长度。
* **类:** 关键字是 `class`，构造函数是 `__init__`，并且用 `self` 代替 `$this`。

掌握了这些，您已经可以阅读和编写简单的 Python 代码了！

接下来，我们进入学习计划的第三步：**环境和包管理**。

在 PHP 开发中，您用 **Composer** 来管理项目依赖（比如 Guzzle、Monolog 等库）。Python 也有一个完全对应的工具，叫做 **`pip`**。

为了帮您建立联系，请问您用 Composer 添加一个新的库时，最常用的命令是什么？

很接近了！通常我们添加一个新包用 `composer require a/package`，而 `composer install` 是用来安装 `composer.json` 里已经定义好的所有依赖。

这个思路完全正确。

在 Python 的世界里，这个命令对应的是 **`pip install`**。

举个例子：

* 在 PHP 中安装一个 HTTP 请求库 Guzzle: `composer require guzzlehttp/guzzle`
* 在 Python 中安装最流行的 HTTP 请求库 Requests: `pip install requests`

是不是很简单？`pip` 就是您的新 “Composer”。

---

说到包管理，Python 社区还有一个非常重要的最佳实践，就是 **虚拟环境 (Virtual Environment)**。

简单来说，虚拟环境就是为您的每一个项目创建一个“隔离”的 Python 环境。项目 A 和项目 B 可以拥有完全不同版本的依赖包，互不干扰。这就避免了 PHP 开发中有时会遇到的“依赖地狱”问题。

Python 内置了一个创建虚拟环境的工具，叫做 **`venv`**。

根据这个描述，您觉得使用 `venv` 的主要好处是什么？

一语中的！核心好处就是 **环境隔离**。

这保证了您的项目 A 和项目 B 之间不会有依赖冲突，让项目管理变得非常干净。

使用 `venv` 通常只有两步：

1. **创建环境:** 在您的项目文件夹下，运行 `python -m venv venv`。这会创建一个名为 `venv` 的文件夹，里面包含了项目所需的一个独立的 Python 环境。
2. **激活环境:**  
   * 在 Windows 上: `venv\Scripts\activate`  
   * 在 Mac/Linux 上: [`source venv/bin/activate`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.bin.md)  
   激活后，您会看到命令行提示符前面多了 `(venv)` 的字样，表示您现在处于这个隔离环境中。之后您使用的所有 `pip` 命令都只会作用于当前环境。

---

### 第四步：动手写个小项目

我们已经涵盖了语法、概念和工具，现在是时候把它们串起来了！这是让知识真正属于您的最好方式。

作为一个有经验的 web 开发者，您对 API 应该非常熟悉。我们不如就写一个简单的小脚本，功能是：**从一个公开的 API 获取一条随机的编程笑话并打印出来**。

这个小项目能让我们练习：

* 使用 `pip` 安装 `requests` 库。
* 编写一个 Python 函数。
* 发送一个 HTTP GET 请求。
* 处理返回的 JSON 数据 (也就是 Python 的字典)。

## 基数数据类型

Python 的数据类型很丰富，为了让咱们看得更清楚，可以把它们分成几个大类。您看这样划分怎么样？

1. **基础与数值类型 (Basic & Numeric Types):** 整数、浮点数、字符串等。
2. **序列类型 (Sequence Types):** 有序的集合，比如列表 (list) 和元组 (tuple)。
3. **映射类型 (Mapping Type):** 键值对集合，也就是字典 (dict)。
4. **集合类型 (Set Types):** 无序且元素唯一的特殊集合。
5. **特殊类型 (Special Types):** 布尔值 (bool) 和 `None`。

这个分类听起来清晰吗？我们从哪一类开始对比呢？我个人建议可以从最熟悉的 **第一类：基础与数值类型** 开始。

好的，我们从最基础的开始。

在 PHP 和 Python 中，最基础的几种类型几乎是一一对应的，但用法上有一些细微但重要的差别。

我们先看 **数值 (Numeric)** 类型。

| 类型      | Python | PHP   | 对比和区别                                                                               |
| ------- | ------ | ----- | ----------------------------------------------------------------------------------- |
| **整数**  | int    | int   | 功能基本相同。但 Python 的整数**没有大小限制**（只受内存限制），而 PHP 的整数有最大值 (PHP\_INT\_MAX)，超出后会自动转为 float。 |
| **浮点数** | float  | float | 两者几乎完全一样，都用来表示小数或科学计数法。                                                             |

整数的区别是一个有趣的技术细节，但在日常开发中，您感受最深的会是**字符串 (String)** 的不同。

在 PHP 中，您可以用单引号 `'...'` 或双引号 `"..."` 来定义字符串。这两者最主要的区别是什么？

您的意思是，双引号 `"` 里的变量会被解析（替换成变量的值），而单引号 `'` 里的内容会原样输出，对吗？

如果是这个意思，那您完全说对了！这正是 PHP 的核心区别。

现在我们来看 Python，这一点上它有很大不同：

* 在 Python 中，**单引号 `'...'` 和双引号 `"..."` 是完全一样的**！它们都不会解析变量。

那么 Python 怎么实现类似 PHP 双引号的功能呢？答案是使用一种特殊的字符串，叫做 **f-string**。

看下面的对比：

**PHP:**

```php
$name = "Alice";
echo "Hello, $name";   // 输出: Hello, Alice
echo 'Hello, $name';   // 输出: Hello, $name

```

**Python:**

```python
name = "Alice"
# 在引号前加上 f，就会解析 {} 里的变量
print(f"Hello, {name}")  # 输出: Hello, Alice

# 普通的字符串（无论单双引号）都不会解析
print("Hello, {name}")   # 输出: Hello, {name}
print('Hello, {name}')   # 输出: Hello, {name}

```

**总结一下**：在现代 Python 中，需要格式化字符串时，就用 `f-string`。这是最推荐、最简洁的方式。

---

基础类型我们已经看完了。接下来，我们看看计划中的第二类：**序列类型 (Sequence Types)**。

我们之前提到过，PHP 的 `array` 非常万能，但 Python 把它的功能拆分了。您还记得我们用什么来表示一个有序的、像 PHP 索引数组一样的集合吗？

中括号 `[]`，完全正确！

用中括号 `[]` 定义的就是 **列表 (list)**。它是 Python 中最常用的数据结构之一。

我们来看一下它和 PHP 数组的对比：

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/b8594f81bbce412eafe0465ca2732694.png)

到目前为止，[`list`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.list.md) 看起来只是 PHP 索引数组换了个名字。但 Python 还有一个和 [`list`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.list.md) 非常像的兄弟，叫做 **元组 (tuple)**。

元组的定义和列表只有一个小区别：它用的是 **圆括号 `()`**。  
`my_tuple = ("apple", "banana")`

元组和列表最大的区别在于：**元组是不可变的 (immutable)**。一旦创建，您就不能再添加、删除或修改它的任何元素。

根据这个描述，如果您的程序需要一个永远不变的配置项列表，比如一周的星期名称 `("Monday", "Tuesday", ...)`，您觉得用列表 ([`list`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.list.md)) 还是元组 ([`tuple`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.tuple.md)) 更安全、更合适呢？

完全正确！

用 **元组 (tuple)** 更合适。因为它 **不可变** 的特性保证了这份数据不会在程序的任何地方被意外地修改，代码更安全、更可预测。

简单总结一下序列类型：

* **列表 [`list`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.list.md)**: 可变的、有序的集合。最常用。
* **元组 [`tuple`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.tuple.md)**: 不可变的、有序的集合。用于保护数据不被改变。

---

好了，基础类型和序列类型我们都看完了。现在是计划中的第三类：**映射类型 (Mapping Type)**。

在 Python 中，这个类别只有一个成员，但它非常强大，我们之前已经详细讨论过它了。

您还记得我们把 Python 中类似 PHP 关联数组、用于存储键值对的数据类型称为什么吗？

没关系，这个词很容易忘记！

根据我们之前的对话，我提到过：

> 在 Python 里，我们称之为 **字典 (dictionary)**，简称 [`dict`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.dict.md)。

所以，Python 版本的关联数组就是**字典 (dictionary)**。

我们来系统地对比一下：

![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/7e82638f43cb47248d91b6660ddabe51.png)

到这里，Python 中最核心的三种数据结构您已经掌握了：**列表 [`list`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.list.md)、元组 [`tuple`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.tuple.md)、字典 [`dict`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.dict.md)**。这三种能覆盖您 90% 的日常开发需求。

接下来，我们看一个 PHP 中没有，但 Python 里很有用的类型。

在 PHP 中，如果您想得到一个数组里所有不重复的值，您会用哪个函数？

完全正确，就是 `array_unique()` 函数。

您看，在 PHP 中，您需要调用一个函数来处理一个数组，才能得到唯一值。

而在 Python 中，有一个专门为此设计的数据类型，叫做 **集合 (set)**。

它的用法非常简单。您只需要把列表（list）转换成集合（set），重复的元素就自动消失了。

```python
# 1. 我们有一个包含重复元素的列表
numbers_list = [1, 2, 2, 3, 1, 4]

# 2. 使用 set() 将列表转换为集合
unique_numbers_set = set(numbers_list)

# 3. 打印结果
print(unique_numbers_set)
# 输出: {1, 2, 3, 4}

```

**集合 (set) 的特点:**

* **元素唯一**：自动去重，这是它最核心的功能。
* **无序**：里面的元素没有固定的顺序。
* **查找速度极快**：判断一个元素是否在集合中，比在长列表中查找要快得多。

---

我们已经看完了四个大类。现在是最后一类，也是最简单的一类：**特殊类型**。

这包括布尔值 ([`bool`](https://xplanc.org/primers/document/zh/02.Python/EX.%E5%86%85%E5%BB%BA%E5%87%BD%E6%95%B0/EX.bool.md)) 和 `None`。

我们先说布尔值。在 PHP 中，当您写 `if ($variable)` 时，除了 `false` 本身，还有哪些值会被当作 `false` 来处理？

您说得非常对！`0` 和空字符串 `''` 都会被当作 `false`。

在 PHP 中，像 `0`, `''`, `[]` (空数组), `null` 等都会在布尔上下文中被视为 `false`。这叫做“假值”(falsy values)。

Python 也有完全一样的概念！

| Python                                      | PHP        |
| ------------------------------------------- | ---------- |
| False                                       | false      |
| 0, 0.0                                      | 0, 0.0     |
| "" (空字符串)                                   | "" (空字符串)  |
| \[\] (空列表), () (空元组), {} (空字典), set() (空集合) | \[\] (空数组) |

您看，规则几乎是一样的：**任何表示“空”或者“零”的东西，在 `if` 语句里都会被当作 `false`**。

---

最后，我们来看 PHP 中的 `null`。

`null` 表示一个变量没有任何值。Python 中有一个完全等价的关键字，拼写略有不同，叫做 **`None`** (首字母大写)。

| Python | PHP  |
| ------ | ---- |
| None   | null |

`None` 和 `null` 的用途和意义是完全相同的。

---

### 最终总结：数据类型速查表

非常棒！我们已经系统地对比了 Python 和 PHP 的所有主要数据类型。

| 分类     | Python 类型       | 对应 PHP 概念           | 关键点                                       |
| ------ | --------------- | ------------------- | ----------------------------------------- |
| **基础** | int, float, str | int, float, string  | Python 字符串格式化用 **f-string**               |
| **序列** | list, tuple     | 索引数组                | list **可变** (用 \[\])，tuple **不可变** (用 ()) |
| **映射** | dict            | 关联数组                | 键值对集合 (用 {})                              |
| **集合** | set             | array\_unique() 的结果 | 元素**唯一**且**无序**                           |
| **特殊** | bool, None      | bool, null          | False 和 None (首字母大写)                      |

这份表格可以作为您未来的速查手册。您已经为您深厚的 PHP 知识，找到了在 Python 世界里的完美映射。

---

本文是转载文章，[点击查看原文](https://blog.csdn.net/come11234/article/details/152268883)。