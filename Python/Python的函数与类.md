# Python的函数与类

函数可以帮助我们做什么呢？在函数的基础上，类又可以实现哪些功能呢？下面让我们一起来认识一下Python中的函数与类：

## 函数

函数是用于完成具体任务的代码块，如果需要在程序中**多次执行同一任务**，只需调用执行该任务的函数即可。因此，**通过使用函数，可以简化程序操作**。

### 定义函数

首先，我们使用关键字`def`来告诉Python要定义一个函数；其次，向Python指出以字母数字或下划线组成的函数名，函数名后紧跟包含参数的括号；最后，定义以冒号结尾，其后面的所有缩进行构成了函数体。要调用函数时，可依次指定函数名以及括号内的参数。

在下面的例子中，创建了一个名为`user_id`的函数，调用时会输出相应的语句：

```python
def user_id(name):
    print(f"Hello! my name is {name}.")

user_id('Daisy')
```

```sh
#输出结果
Hello! my name is Daisy.
```

### 传递实参

先来了解形参和实参的概念。在上面函数 `user_id()` 的定义中，括号内的变量 `name` 是一个形参，而在代码 `user('Daisy')` 中，值 `'Daisy'` 是一个实参，**实参是调用函数时传递给函数的具体信息**。

在调用函数时，Python **必须将函数调用中的每个实参都关联到函数定义中的一个形参**。为此，最简单的关联方式是基于实参的顺序，即**位置实参**。此外，还可直接在实参中将名称和值关联起来，即**关键字实参**。

在下面的例子中，调用 `my_pet()` 函数时，我们向它传递了实参 `'dog'` 和 `'Mary'`，分别存储在形参 `pet_type` 和 `pet_name` 中，函数完成其任务后会输出一条名为 Mary 的小狗信息。

```python
def my_pet(pet_type, pet_name): 
    print(f"My {pet_type}'s name is {pet_name}.")

my_pet('dog', 'Mary')
```

```sh
#输出结果
My dog's name is Mary.
```

为了避免传递实参时位置对应错误，还可以直接在实参中指定名称和值，如下面的代码所示。当然，这两种方式传递实参后所输出的信息是一致的。

```python
def my_pet(pet_type, pet_name): 
    print(f"My {pet_type}'s name is {pet_name}.")

my_pet(pet_type='dog', pet_name='Mary')
```

```sh
#输出结果
My dog's name is Mary.
```

### 返回值

函数并非总是直接显示输出，它也可以处理一些数据并返回一个或一组值。在函数中，可**使用return 语句将值返回到调用函数的代码行**。下面的例子中创建了名为 `add` 的函数，调用后会返回数值相加的结果：

```python
def add(a, b):
    print(f"ADDING {a} + {b}")
    return a + b

age = add(10 + 8)
print(f"Age: {age}")
```

```sh
Age: 18
```

函数所返回的值并不仅限于简单的数值，还可以是字典或列表这种复杂的数据结构。

下面的函数接受省、市的组成部分，并返回一个表示城市隶属于省的字典：

```python
def in_country(province, city):
    country = {'Province': province, 'City': city }
    return country

north = in_country('Jilin', 'Changchun')
print(north)
```

```sh
#输出结果
{'Province' : 'Jilin' , 'City' : 'Changchun'}
```

将列表传递给函数后，函数就能直接访问其内容。假设有一个用户列表，我们要问候其中的每位用户。下面的示例将一个名字列表传递给一个名为`greet_users()` 的函数，调用该函数后，会输出对列表中每人的问候信息：

```python
def greet_users(names):
    for name in names:
        message = f"Hello, {name}!" 
        print(message)

user_name = ['Mary', 'John', 'Maria']
greet_users(user_name)
```

```sh
#输出结果
Hello, Mary!
Hello, John!
Hello, Maria!
```

## 类

Python是一种面向对象编程的语言，**使用类可以定义某类对象都有的通用行为**，从而加强程序的一致性。基于类创建对象时，每个对象都会自动具备通用行为，而且还可以根据需要赋予每个对象独特的个性。

### 创建和使用类

在Python中，**首字母大写的名称指的是类**，**根据类来创建对象被称为实例化**，**类中的函数称为方法**。其中方法`__init__()` 中的**第一个形参必须是self**，每个与类相关联的方法调用都自动传递实参self，它是一个指向实例本身的引用，让实例能够访问类中的属性和方法。

在根据类创建实例时，只需要给 self 之外的形参提供值，在访问实例的属性和方法时，一般使用句点表示法。下面来看一个例子：

```python
class Animals(object):

    def __init__(self, name):
        self.name = name

    def sleep(self):
        print(f"{self.name} is now sleeping.")


my_dog = Animals('Mary')
print(f"My dog's name is {my_dog.name}.")
my_dog.sleep()
```

```sh
#输出结果
My dog's name is Mary.
Mary is now sleeping.
```

在这个例子中，定义了名为 Animals 的类，创建实例时 Python 将调用 Animals 类的方法`__init__()`。`self.name = name` 获取存储在形参name 中的值，并将其存储到变量 name 中，然后该变量被关联到当前创建的实例。遇到代码 `my_dog.sleep()` 时，Python 在类 Animals中查找方法 `sleep()` 并运行其代码。

### 继承

编写类时，并非总是要从空白开始。如果要编写的类是另一现成类的特殊版本，可使用继承。

**一个类继承另一个类时，它将自动获得另一个类的所有属性和方法**，原有的类称为父类，而新类称为子类。**创建子类时，父类必须包含在当前文件中，且位于子类前面**。

当在父类定义了一个方法但没有在子类中定义时会发生隐式继承，即子类会自动调用父类中的该方法。

比如在下面的例子中，父类Parent有名为 implicit的方法，而子类 Child却没有，这时子类若要访问 implicit，Python会自动去父类中查找，执行 implicit方法下的代码`print("PARENT implicit()")`。

```python
class Parent(object):

    def implicit(self):
        print("PARENT implicit()")


class Child(Parent):
    pass


dad = Parent()
son = Child()

dad.implicit()
son.implicit()
```

```sh
#输出结果
PARENT implicit()
PARENT implicit()
```

对于父类的方法，只要它不符合子类模拟的实物的行为，都可以对其进行重写，让子类的方法实现与父类不同的新功能，这时只需要在子类中定义一个同名方法。

假设 Parent类有一个名为 `override()` 的方法，它对 Child来说毫无意义，这时需要进行在 Child类下重写。重写之后，如果再对 Child类调用方法 `override()`，Python将忽略Parent 类中的方法`override()`，转而运行 Child中 `override()`下的代码：

```python
class Parent(object):

    def override(self):
        print("PARENT override()")


class Child(Parent):

    def override(self):
        print("CHILD override()")


dad = Parent()
son = Child()

dad.override()
son.override()
```

```sh
#输出结果
PARENT override()
CHILD override()
```

如果想在父类中定义的内容运行之前或运行之后修改行为，需要先覆盖函数，再使用 Python内置函数 `super` 来调用父类里的版本，形式为 super(子类名, self).方法名。 在下面的代码中，第8行调用了 `super(Child, self).altered()`，使 Python访问 Parent 类中的 `altered()`，打印出信息 `PARENT altered()`。

```python
class Parent(object):

    def altered(self):
        print("PARENT altered()")


class Child(Parent):

    def altered(self):
        print("CHILD, BEFORE PARENT altered()")
        super(Child, self).altered()
        print("CHILD, AFTER PARENT altered()")


dad = Parent()
son = Child()
dad.altered()
son.altered()
```

```sh
#输出结果
PARENT altered()
CHILD, BEFORE PARENT altered()
PARENT altered()
CHILD, AFTER PARENT altered()
```

以上是关于函数和类的基本认识。

## 模块

模块是包含 Python 定义和语句的文件。其文件名是模块名加后缀名 `.py` 。在模块内部，通过全局变量 `__name__` 可以获取模块名（即字符串）。例如，用文本编辑器在当前目录下创建 `fibo.py` 文件，输入以下内容：

```python
# Fibonacci numbers module

def fib(n):    # write Fibonacci series up to n
    a, b = 0, 1
    while a < n:
        print(a, end=' ')
        a, b = b, a+b
    print()

def fib2(n):   # return Fibonacci series up to n
    result = []
    a, b = 0, 1
    while a < n:
        result.append(a)
        a, b = b, a+b
    return result
```

现在，进入 Python 解释器，用以下命令导入该模块：

```python
import fibo
fibo.fib(1000)
fibo.__name__
```

模块包含可执行语句及函数定义。这些语句用于初始化模块，且仅在 import 语句 *第一次* 遇到模块名时执行。

```python
from fibo import fib, fib2
fib(500)
```

或者

```python
from fibo import *
fib(500)
```

> 这种方式会导入所有不以下划线（`_`）开头的名称。大多数情况下，不要用这个功能，这种方式向解释器导入了一批未知的名称，可能会覆盖已经定义的名称。
>
> 注意，一般情况下，不建议从模块或包内导入 `*`， 因为，这项操作经常让代码变得难以理解。不过，为了在交互式编译器中少打几个字，这么用也没问题。

模块名后使用 `as` 时，直接把 `as` 后的名称与导入模块绑定。

```python
import fibo as fib
fib.fib(500)
```

与 `import fibo` 一样，这种方式也可以有效地导入模块，唯一的区别是，导入的名称是 `fib`。

[`from`](https://docs.python.org/zh-cn/3/reference/simple_stmts.html#from) 中也可以使用这种方式，效果类似：

```python
from fibo import fib as fibonacci
fibonacci(500)
```

## 实战

demo.py

```python
# coding:utf-8
import os
import re
import subprocess


class OsPlus:

    def __init__(self, path_ffmpeg: str, path_7z: str):
        """初始化OsPlus

        Args:
            path_ffmpeg (str): ffmpeg的路径
            path_7z (str): 7z的路径
        """
        self.path_ffmpeg = path_ffmpeg
        self.path_7z = path_7z

    def get_all_files(self, path: str, ext: str = '') -> list:
        """获取指定路径下指定扩展名的全部文件

        Args:
            path (str): 指定路径
            ext (str, optional): 指定扩展名，默认为''，代表不限制.

        Returns:
            list: 获取的全部文件列表
        """
        allfile = []
        for dirpath, dirnames, filenames in os.walk(path):
            for name in filenames:
                if ext == '' or name.endswith(ext):
                    allfile.append(os.path.join(dirpath, name))
        return allfile

    def get_file_hash(self, file: str) -> str:
        """获取文件的MD5值

        Args:
            file (str): 文件路径

        Returns:
            str: 文件的MD5值
        """
        ret = subprocess.run(f'certutil -hashfile "{file}" MD5',
                             shell=True,
                             stdout=subprocess.PIPE,
                             stderr=subprocess.PIPE)
        hashs = ret.stdout.decode('gbk').split('\r\n')
        return hashs[1]

    def get_zip_files(self, file: str) -> list:
        """获取指定的压缩文件内的文件列表

        Args:
            file (str): 压缩文件路径

        Returns:
            list: 压缩文件内的文件列表
        """
        ret = subprocess.run(f'"{self.path_7z}" l "{file}" -ba -slt',
                             shell=True,
                             stdout=subprocess.PIPE,
                             stderr=subprocess.PIPE)
        result = re.findall(r"(?im)Path = ([\S| ]+)", ret.stdout.decode('gbk'))
        return result

    def find_duplicate_file(self, path: str, ext: str = '') -> list:
        """查找指定路径指定类型文件的重复文件

        Args:
            path (str): 指定路径
            ext (str, optional): 检索的文件扩展名。默认为''，代表全部文件.

        Returns:
            list: 检索到重复的文件路径列表
        """
        files = {}
        uni_files = []
        duplicate_files = []
        allfile = self.get_all_files(path, ext)
        for file in allfile:
            file_hash = self.get_file_hash(file)
            # 用个字典存一下file和hash的关系，当然用二维list存也没问题
            files[file] = file_hash
            # uni_files里面没有，代表还没重复，添加到uni_files中
            if uni_files.count(file_hash) == 0:
                uni_files.append(file_hash)
            # uni_files里面有（重复文件），duplicate_file里面没有，添加到duplicate_file保存
            elif duplicate_files.count(file_hash) == 0:
                duplicate_files.append(file_hash)

        ret = []
        for hash in duplicate_files:
            for kfile, vfile in files.items():
                if hash == vfile:
                    ret.append(kfile)
        return ret

    def do_ffmpeg(self, path: str):
        """将指定路径中查找到的视频文件进行截图

        Args:
            path (str): 文件路径
        """
        allfile = self.get_all_files(path, '.mp4')
        for file in allfile:
            subprocess.run(
                f'"{self.path_ffmpeg}" -i "{file}" -y -ss 10 -f image2 -frames:v 1 "{file}.png"'
            )

```

另外的文件中调用

```python
from demo import OsPlus

os_plus = OsPlus(r'C:\Tools\ffmpeg\ffmpeg.exe',
                 r'c:\Program Files\7-Zip\7z.exe')

dir3D = r'C:\Users\lgc653\Documents\3D Objects'
# 查找所有重复的glb
print(os_plus.find_duplicate_file(dir3D, '.glb'))
# 查找所有zip的被压缩的文件列表
zips = os_plus.get_all_files(dir3D, '.zip')
for file in zips:
    print(file)
    print(os_plus.get_zip_files(file))
# 查找mp4并截图
os_plus.do_ffmpeg(dir3D)
```

## Python练习：封装FFmpeg工具类

**目标：**

* 练习Python面向对象编程，包括类定义、属性、方法等。
* 学习使用`subprocess`模块调用外部程序。
* 封装`ffmpeg`命令行工具，简化视频处理操作。

**任务：**

创建一个名为`FFmpegUtil`的类，封装以下`ffmpeg`功能：

1. **获取视频信息:** 
    * 方法名：`get_video_info(video_path)`
    * 参数：`video_path` (str) - 视频文件路径
    * 返回值：字典类型，包含以下信息：
        * `duration` (float): 视频时长，单位秒
        * `width` (int): 视频宽度，单位像素
        * `height` (int): 视频高度，单位像素
        * `format` (str): 视频格式，例如 "mov", "mp4" 等
2. **视频截图:**
    * 方法名：`capture_screenshot(video_path, output_path, time)`
    * 参数：
        * `video_path` (str) - 视频文件路径
        * `output_path` (str) - 截图输出路径
        * `time` (float) - 截图时间点，单位秒
    * 返回值：无
3. **视频转码:**
    * 方法名：`convert_video(input_path, output_path, output_format)`
    * 参数：
        * `input_path` (str) - 输入视频文件路径
        * `output_path` (str) - 输出视频文件路径
        * `output_format` (str) - 输出视频格式，例如 "mp4", "avi" 等
    * 返回值：无

**要求：**

* 使用`subprocess.run()`函数执行`ffmpeg`命令。
* 使用正则表达式从`ffmpeg`输出中提取所需信息。
* 处理`ffmpeg`命令执行过程中的错误，并抛出异常。

**提示：**

* 可以使用`os.path.exists()`函数检查文件是否存在。
* 可以使用`re`模块进行正则表达式匹配。
* 可以参考`ffmpeg`官方文档了解命令行参数：https://ffmpeg.org/ffmpeg.html

**示例代码：**

```python
import subprocess
import re
import os

class FFmpegUtil:

    def __init__(self):
        # 检查ffmpeg是否安装
        if not self._check_ffmpeg():
            raise Exception("FFmpeg not found. Please install FFmpeg.")

    def _check_ffmpeg(self):
        # 检查ffmpeg是否安装的函数
        # ...

    def get_video_info(self, video_path):
        # 获取视频信息的函数
        # ...

    def capture_screenshot(self, video_path, output_path, time):
        # 视频截图的函数
        # ...

    def convert_video(self, input_path, output_path, output_format):
        # 视频转码的函数
        # ...

# 示例用法
if __name__ == "__main__":
    ffmpeg_util = FFmpegUtil()
    video_info = ffmpeg_util.get_video_info("my_video.mp4")
    print(video_info)
    ffmpeg_util.capture_screenshot("my_video.mp4", "screenshot.jpg", 5)
    ffmpeg_util.convert_video("my_video.mp4", "my_video.avi", "avi")
```

**进阶挑战：**

* 添加更多`ffmpeg`功能，例如视频剪辑、添加水印等。
* 支持异步执行`ffmpeg`命令，提高程序效率。
* 创建图形界面，方便用户使用。

这个练习可以帮助你更好地理解Python面向对象编程和`ffmpeg`工具的使用。完成这个练习后，你可以尝试使用`FFmpegUtil`类处理自己的视频文件。
