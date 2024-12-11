# Python的数据类型

## 基础数据类型

Python 中的基础数据类型可以分为以下几类：

### 数字类型

   *  **整数 (int)**： 用于表示整数，例如：10, -5, 0
   *  **浮点数 (float)**： 用于表示带小数的数字，例如：3.14, -2.5, 1.0
   *  **复数 (complex)**： 用于表示复数，例如：2 + 3j, -1j 

### 布尔类型 (bool)

   *  用于表示真或假，只有两个值：True 和 False

### 字符串类型 (str)

   *  用于表示文本数据，例如："Hello", 'Python', """多行字符串"""

### NoneType

   *  用于表示空值，只有一个值：None 

### 注意

Python 基础类型虽然概念简单，但在实际使用中，也有一些需要注意的地方：

**1.  整数 (int)**

   * Python 3 中，整数的长度没有限制，可以表示任意大小的整数，只受限于内存大小。
   * Python 2 中，整数分为 int 和 long 类型，long 类型可以表示任意大小的整数。

**2.  浮点数 (float)**

   * 浮点数的精度有限，不能精确表示所有小数。
   * 进行浮点数运算时，可能会出现精度丢失的情况，需要注意结果的精度。
   * 可以使用 Decimal 类型进行高精度计算。

**3.  布尔类型 (bool)**

   * 布尔类型是整数类型的子类，True 等价于 1，False 等价于 0。
   * 在条件判断中，任何非零值都会被视为 True，只有 0 和 None 被视为 False。

**4.  字符串类型 (str)**

   * Python 中的字符串是不可变的，不能直接修改字符串中的字符。
   * 可以使用字符串切片、拼接、格式化等操作创建新的字符串。
   * Python 3 中，字符串默认使用 Unicode 编码，可以表示任何字符。

**5.  NoneType**

   * NoneType 类型只有一个值 None，表示空值。
   * None 常用于表示变量没有赋值，或者函数没有返回值等情况。

## 序列类型

Python 中的序列类型是一种数据结构，用于存储一系列有序的元素。常见的序列类型有：

### 列表 (list)

   * **定义:** 使用方括号 `[]` 定义，元素之间用逗号 `,` 分隔。
   * **特点:** 有序、可变（mutable），可以包含不同类型的元素。
   * **操作:** 支持索引访问、切片、拼接、重复、成员运算、迭代等操作。
   * **使用场景:**
      * 存储需要动态修改的数据集合，例如学生名单、商品列表等。
      * 表示矩阵或多维数组。
      * 作为函数的参数或返回值，传递多个数据。

   **示例:**

```python
   # 存储学生名单
   students = ["Alice", "Bob", "Charlie"]

   # 表示矩阵
   matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]

   # 函数返回多个值
   def get_user_info():
       name = "Alice"
       age = 25
       city = "New York"
       return [name, age, city]

   user_info = get_user_info()
   print(user_info)  # 输出：["Alice", 25, "New York"]
```

### 元组 (tuple)

   * **定义:** 使用圆括号 `()` 定义，元素之间用逗号 `,` 分隔。
   * **特点:** 有序、不可变（immutable），可以包含不同类型的元素。
   * **操作:** 支持索引访问、切片、拼接、重复、成员运算、迭代等操作，但不支持修改元素。
   * **使用场景:**
      * 存储不需要修改的数据集合，例如数据库记录、配置文件选项等。
      * 函数返回多个值，确保返回值不被修改。
      * 作为字典的键，因为元组是不可变的。

   **示例:**

```python
   # 存储数据库记录
   user = ("Alice", 25, "New York")

   # 函数返回多个值
   def get_coordinates():
       x = 10
       y = 20
       return x, y  # 返回一个元组

   coordinates = get_coordinates()
   print(coordinates)  # 输出：(10, 20)

   # 作为字典的键
   my_dict = {("Alice", 25): "New York", ("Bob", 30): "London"}
```

### 范围 (range)

   * **定义:** 使用 `range(start, stop, step)` 函数创建。
   * **特点:** 表示一个整数序列，通常用于循环。
   * **参数:**
      * `start`: 起始值（包含），默认为 0。
      * `stop`: 结束值（不包含）。
      * `step`: 步长，默认为 1。
   * **使用场景:**
      * 循环执行固定次数的代码块。
      * 遍历特定范围内的整数。

   **示例:**

```python
   # 循环执行 5 次
   for i in range(5):
       print(i)  # 输出：0 1 2 3 4

   # 遍历 1 到 10 的偶数
   for i in range(2, 11, 2):
       print(i)  # 输出：2 4 6 8 10
```

### 总结

* 列表适用于需要修改元素的场景，例如存储动态数据。
* 元组适用于不需要修改元素的场景，例如函数返回多个值。
* 范围适用于需要迭代固定次数或遍历特定整数序列的场景。

## 集合类型

Python 中的集合类型也是一种数据结构，用于存储一系列无序的、唯一的元素。常见的集合类型有：

### 集合 (set)

   * **定义:** 使用大括号 `{}` 定义，元素之间用逗号 `,` 分隔。 
   * **特点:** 无序、可变（mutable），元素必须是不可变类型，且不允许重复。
   * **操作:** 支持成员运算、添加元素、删除元素、交集、并集、差集等操作。
   * **使用场景:**
      * 去除重复元素：例如，从列表中去除重复的用户名。
      * 判断元素是否存在：例如，检查用户是否在黑名单中。
      * 数学集合运算：例如，计算两个集合的交集、并集、差集等。

   **示例:**

   ```python
   # 去除重复元素
   usernames = ["Alice", "Bob", "Charlie", "Alice", "Bob"]
   unique_usernames = set(usernames)
   print(unique_usernames)  # 输出：{'Charlie', 'Bob', 'Alice'}

   # 判断元素是否存在
   banned_users = {"Bob", "Eve"}
   if "Alice" in banned_users:
       print("Alice is banned")
   else:
       print("Alice is not banned")

   # 数学集合运算
   set1 = {1, 2, 3}
   set2 = {2, 3, 4}
   intersection = set1 & set2  # 交集
   union = set1 | set2  # 并集
   difference = set1 - set2  # 差集
   print(intersection)  # 输出：{2, 3}
   print(union)  # 输出：{1, 2, 3, 4}
   print(difference)  # 输出：{1}
   ```

### 冻结集合 (frozenset)

   * **定义:** 使用 `frozenset()` 函数创建，传入一个可迭代对象作为参数。
   * **特点:** 无序、不可变（immutable），元素必须是不可变类型，且不允许重复。
   * **操作:** 支持成员运算、交集、并集、差集等操作，但不支持添加或删除元素。
   * **使用场景:**
      * 作为字典的键：因为冻结集合是不可变的。
      * 在需要保证集合内容不被修改的场景。

   **示例:**

   ```python
   # 作为字典的键
   my_dict = {frozenset({1, 2}): "value1", frozenset({3, 4}): "value2"}

   # 保证集合内容不被修改
   permissions = frozenset({"read", "write"})
   # permissions.add("execute")  # 这行代码会报错，因为冻结集合不可变
   ```

### 总结

* 集合适用于需要存储唯一元素、进行成员运算或集合运算的场景。
* 冻结集合适用于需要将集合作为字典键或保证集合内容不被修改的场景。

## 映射类型

Python 中的映射类型是一种数据结构，用于存储键值对的集合，其中每个键都映射到一个值。Python 中最常用的映射类型是字典 (dict)。

### 字典 (dict)

   * **定义:** 使用大括号 `{}` 定义，键值对之间用冒号 `:` 分隔，键值对之间用逗号 `,` 分隔。
   * **特点:** 无序、可变（mutable），键必须是不可变类型（例如字符串、数字、元组），值可以是任何类型，且键不允许重复。
   * **操作:** 支持通过键访问值、添加键值对、删除键值对、更新值、遍历键值对等操作。
   * **使用场景:**
      * 存储和访问关联数据：例如，将用户名映射到用户信息、将商品 ID 映射到商品详情等。
      * 表示计数器：例如，统计文本中每个单词出现的次数。
      * 作为函数参数或返回值，传递多个命名参数。

   **示例:**

   ```python
   # 存储用户信息
   user_info = {"name": "Alice", "age": 25, "city": "New York"}
   print(user_info["name"])  # 输出：Alice

   # 表示计数器
   word_counts = {}
   text = "apple banana apple cherry banana apple"
   for word in text.split():
       if word in word_counts:
           word_counts[word] += 1
       else:
           word_counts[word] = 1
   print(word_counts)  # 输出：{'apple': 3, 'banana': 2, 'cherry': 1}

   # 作为函数参数
   def greet_user(name, age, city):
       print(f"Hello, {name}! You are {age} years old and live in {city}.")

   user_data = {"name": "Bob", "age": 30, "city": "London"}
   greet_user(**user_data)  # 使用 ** 解包字典作为命名参数
   ```

### 总结

* 字典适用于需要存储键值对、通过键快速访问值、动态添加或删除键值对的场景。

## 数据类型转换

在 Python 中，我们经常需要对不同数据类型进行转换，以便进行各种操作。Python 提供了一些内置函数来实现数据类型转换。

### 常见数据类型转换函数

| 函数      | 描述                                                         |
| --------- | ------------------------------------------------------------ |
| `int()`   | 将一个数字或字符串转换为整数。                               |
| `float()` | 将一个数字或字符串转换为浮点数。                             |
| `str()`   | 将任何数据类型转换为字符串。                                 |
| `list()`  | 将一个序列（例如字符串、元组、范围）转换为列表。             |
| `tuple()` | 将一个序列（例如字符串、列表、范围）转换为元组。             |
| `set()`   | 将一个序列或迭代器转换为集合。                               |
| `dict()`  | 创建一个字典，可以从键值对序列或另一个字典创建。             |
| `bool()`  | 将一个值转换为布尔值，如果值为假则返回 False，否则返回 True。 |

### 使用示例

```python
# 字符串转换为数字
num_str = "123"
num_int = int(num_str)  # 转换为整数
num_float = float(num_str)  # 转换为浮点数

# 数字转换为字符串
num = 123
num_str = str(num)

# 列表转换为元组
my_list = [1, 2, 3]
my_tuple = tuple(my_list)

# 字符串转换为列表
my_str = "hello"
my_list = list(my_str)

# 创建字典
my_dict = dict(name="Alice", age=25)
```

### 注意事项

*  并非所有数据类型之间都可以进行转换，例如，无法将一个列表直接转换为字典。
*  在进行类型转换时，需要注意潜在的错误，例如，将一个包含非数字字符的字符串转换为数字会导致 `ValueError` 异常。
*  可以使用 `try...except` 语句来捕获类型转换过程中可能出现的异常。

## 数据类型的常见操作和方法

每种数据类型都有一系列内置的操作和方法，方便我们对数据进行处理和操作。以下是一些常见数据类型的操作和方法：

### 数字类型 (int, float, complex)

数字类型主要用于数学运算，支持以下常见操作：

* **算术运算符:**  `+`, `-`, `*`, `/`, `//` (地板除), `%` (取余), `**` (幂运算)
* **比较运算符:**  `==`, `!=`, `>`, `<`, `>=`, `<=`
* **赋值运算符:**  `=`, `+=`, `-=`, `*=`, `/=`, `//=`, `%=`, `**=`
* **内置函数:**  `abs()`, `round()`, `max()`, `min()`, `pow()`, `divmod()` 等

**示例:**

```python
x = 10
y = 3

print(x + y)  # 输出：13
print(x / y)  # 输出：3.3333333333333335
print(x // y)  # 输出：3
print(x % y)  # 输出：1
print(x ** y)  # 输出：1000
```

### 字符串 (str)

字符串类型用于存储和处理文本信息，支持以下常见操作：

* **拼接:**  `+`
* **重复:**  `*`
* **索引:**  `[index]`
* **切片:**  `[start:end:step]`
* **成员运算符:**  `in`, `not in`
* **常用方法:**  `len()`, `upper()`, `lower()`, `strip()`, `split()`, `join()`, `replace()`, `find()`, `count()` 等

**示例:**

```python
message = "Hello, world!"

print(message[0])  # 输出：H
print(message[7:12])  # 输出：world
print(len(message))  # 输出：13
print(message.upper())  # 输出：HELLO, WORLD!
print(message.split(", "))  # 输出：['Hello', 'world!']
```

### 列表 (list)

列表是可变的、有序的数据集合，支持以下常见操作：

* **拼接:**  `+`
* **重复:**  `*`
* **索引:**  `[index]`
* **切片:**  `[start:end:step]`
* **成员运算符:**  `in`, `not in`
* **常用方法:**  `len()`, `append()`, `insert()`, `remove()`, `pop()`, `index()`, `count()`, `sort()`, `reverse()` 等

**示例:**

```python
my_list = [1, 2, 3, 4, 5]

print(my_list[0])  # 输出：1
my_list.append(6)  # 添加元素
print(my_list)  # 输出：[1, 2, 3, 4, 5, 6]
my_list.remove(3)  # 删除元素
print(my_list)  # 输出：[1, 2, 4, 5, 6]
my_list.sort()  # 排序
print(my_list)  # 输出：[1, 2, 4, 5, 6]
```

### 元组 (tuple)

元组是不可变的、有序的数据集合，支持的操作与列表类似，但不支持修改元素的操作。

### 字典 (dict)

字典是存储键值对的数据结构，支持以下常见操作：

* **访问值:**  `dict[key]`
* **添加/修改键值对:**  `dict[key] = value`
* **删除键值对:**  `del dict[key]`
* **成员运算符:**  `in`, `not in` (判断键是否存在)
* **常用方法:**  `len()`, `keys()`, `values()`, `items()`, `get()`, `pop()`, `update()` 等

**示例:**

```python
my_dict = {"name": "Alice", "age": 25}

print(my_dict["name"])  # 输出：Alice
my_dict["city"] = "New York"  # 添加键值对
print(my_dict)  # 输出：{'name': 'Alice', 'age': 25, 'city': 'New York'}
del my_dict["age"]  # 删除键值对
print(my_dict)  # 输出：{'name': 'Alice', 'city': 'New York'}
```

### 集合 (set)

集合是存储无序、唯一元素的数据结构，支持以下常见操作：

* **成员运算符:**  `in`, `not in`
* **集合运算符:**  `|` (并集), `&` (交集), `-` (差集), `^` (对称差集)
* **常用方法:**  `len()`, `add()`, `remove()`, `discard()`, `union()`, `intersection()`, `difference()`, `issubset()`, `issuperset()` 等

**示例:**

```python
set1 = {1, 2, 3}
set2 = {2, 3, 4}

print(set1 | set2)  # 输出：{1, 2, 3, 4}
print(set1 & set2)  # 输出：{2, 3}
print(set1 - set2)  # 输出：{1}
```

## Python 数据类型判断

在 Python 中，我们可以使用以下两种方法来判断数据类型：

### 使用 `type()` 函数

   *  `type(object)` 函数返回一个对象的类型。
   *  返回结果是一个类型对象，例如 `<class 'int'>`、`<class 'str'>`、`<class 'list'>` 等。

   **示例：**

   ```python
   x = 10
   print(type(x))  # 输出：<class 'int'>

   y = "hello"
   print(type(y))  # 输出：<class 'str'>

   z = [1, 2, 3]
   print(type(z))  # 输出：<class 'list'>
   ```

### 使用 `isinstance()` 函数

   *  `isinstance(object, classinfo)` 函数用于判断一个对象是否属于指定的类型或其子类。
   *  `classinfo` 可以是一个类型对象或一个类型对象的元组。
   *  如果对象属于指定的类型或其子类，则返回 `True`，否则返回 `False`。

   **示例：**

   ```python
   x = 10
   print(isinstance(x, int))  # 输出：True
   print(isinstance(x, (int, float)))  # 输出：True

   y = "hello"
   print(isinstance(y, str))  # 输出：True
   print(isinstance(y, int))  # 输出：False

   z = [1, 2, 3]
   print(isinstance(z, list))  # 输出：True
   print(isinstance(z, (list, tuple)))  # 输出：True
   ```

### 选择哪种方法？

   *  `type()` 函数用于获取对象的实际类型，而 `isinstance()` 函数用于判断对象是否属于指定的类型或其子类。
   *  在大多数情况下，推荐使用 `isinstance()` 函数，因为它更灵活，可以判断子类关系。
   *  如果需要精确判断对象的类型，可以使用 `type()` 函数。

## 其他需要注意的点

除了上面提到的数据类型定义、转换和判断，还有一些额外的知识点可以帮助你更深入地理解和运用 Python 数据类型：

### 可变类型与不可变类型

* **不可变类型:**  数据在创建后就不能被修改，包括数字类型 (int, float, complex), 字符串 (str), 元组 (tuple), 布尔类型 (bool), frozenset。对不可变类型的操作会返回一个新的对象。
* **可变类型:**  数据在创建后可以被修改，包括列表 (list), 字典 (dict), set。对可变类型的操作会直接修改原对象。

**理解可变性和不可变性对于程序设计至关重要，尤其在函数参数传递、对象比较等方面需要格外注意。**

### 数据类型的应用场景

* **数字类型:**  进行数学运算、计数、索引等。
* **字符串类型:**  存储和处理文本信息，例如姓名、地址、文章内容等。
* **列表:**  存储可变的、有序的数据集合，例如学生名单、商品列表等。
* **元组:**  存储不可变的、有序的数据集合，例如函数返回多个值、数据库记录等。
* **字典:**  存储键值对，例如用户信息、配置选项等。
* **集合:**  存储无序的、唯一的元素，例如去重、成员判断等。

### 4.  NoneType 类型

* `None` 是 Python 中的一个特殊值，表示空值或缺失值。
* `None` 的数据类型是 `NoneType`。
*  `None` 常用于函数没有返回值、变量未赋值等情况。

## 案例：学生信息管理系统

假设我们要开发一个简单的学生信息管理系统，需要存储学生的姓名、年龄、成绩等信息。我们可以使用 Python 的字典来表示每个学生的信息，并将所有学生的字典存储在一个列表中。

```python
students = [
    {"name": "Alice", "age": 18, "scores": {"math": 90, "english": 85, "physics": 92}},
    {"name": "Bob", "age": 17, "scores": {"math": 78, "english": 80, "physics": 88}},
    {"name": "Charlie", "age": 18, "scores": {"math": 95, "english": 92, "physics": 96}},
]
```

### 练习

基于以上案例，尝试完成以下练习：

1. **添加学生信息:**  提示用户输入新学生的姓名、年龄和各科成绩，将信息存储到 `students` 列表中。

2. **查询学生信息:**  提示用户输入学生姓名，打印该学生的详细信息（包括姓名、年龄、各科成绩）。

3. **计算平均成绩:**  提示用户输入学生姓名，计算并打印该学生的平均成绩。

4. **查找最高分:**  找到所有学生中数学成绩最高的学生，打印其姓名和数学成绩。

5. **按年龄排序:**  将 `students` 列表按照学生年龄升序排序。

6. **统计年龄分布:**  统计不同年龄的学生人数，并将结果存储在一个字典中，例如：`{"17": 1, "18": 2}`。

### 练习代码示例 (1-4)

**1. 添加学生信息**

```python
new_student = {}
new_student["name"] = input("请输入学生姓名：")
new_student["age"] = int(input("请输入学生年龄："))
new_student["scores"] = {}
new_student["scores"]["math"] = int(input("请输入数学成绩："))
new_student["scores"]["english"] = int(input("请输入英语成绩："))
new_student["scores"]["physics"] = int(input("请输入物理成绩："))

students.append(new_student)
print("学生信息已添加！")
print(students)
```

**2. 查询学生信息**

```python
search_name = input("请输入要查询的学生姓名：")

for student in students:
    if student["name"] == search_name:
        print(student)
        break
else:
    print(f"未找到名为 {search_name} 的学生信息。")
```

**3. 计算平均成绩**

```python
search_name = input("请输入要计算平均成绩的学生姓名：")

for student in students:
    if student["name"] == search_name:
        total_score = sum(student["scores"].values())
        average_score = total_score / len(student["scores"])
        print(f"{search_name} 的平均成绩为：{average_score}")
        break
else:
    print(f"未找到名为 {search_name} 的学生信息。")
```

**4. 查找最高分**

```python
max_math_score = 0
max_math_student = None

for student in students:
    if student["scores"]["math"] > max_math_score:
        max_math_score = student["scores"]["math"]
        max_math_student = student["name"]

print(f"数学成绩最高的学生是：{max_math_student}，成绩为：{max_math_score}")
```

### 练习提示 (5-6)

**5. 按年龄排序**

*   提示：使用 `sorted()` 函数对 `students` 列表进行排序，可以使用 `lambda` 表达式指定排序关键字为学生的年龄。

**6. 统计年龄分布**

*   提示：创建一个空字典用于存储年龄分布，遍历 `students` 列表，对于每个学生的年龄，如果该年龄已经在字典中存在，则对应的值加 1，否则将该年龄作为键，值设为 1 添加到字典中。