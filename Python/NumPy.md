# NumPy

## NumPy 简介和安装

### 什么是 NumPy？

NumPy（Numerical Python）是 Python 中用于科学计算的核心库。它提供了高性能的多维数组对象以及用于处理这些数组的工具。 NumPy 是 Python 数据科学领域众多其他库的基础，例如 Pandas、SciPy 和 Matplotlib，因此掌握 NumPy 是进行数据分析、机器学习等工作的基础。

### 为什么使用 NumPy？

- **高效的数组运算:** NumPy 的核心是 ndarray 对象，它允许对大量数据进行高效的存储和操作。与 Python 列表相比，NumPy 数组在处理数学运算时速度更快，内存效率更高。
- **丰富的数学函数:** NumPy 提供了大量的数学函数，包括线性代数运算、傅里叶变换、随机数生成等，方便进行各种科学计算。
- **广播机制:** NumPy 的广播机制允许对不同形状的数组进行运算，简化了代码并提高了效率。
- **开源和活跃的社区:** NumPy 是一个开源项目，拥有庞大而活跃的社区，可以方便地获取帮助和资源。

### 如何安装 NumPy？

最简单的安装 NumPy 的方法是使用 Python 包管理器 pip：

```bash
pip install numpy
```

如果您使用 Anaconda 或 Miniconda 发行版，NumPy 已经预先安装好了。

### 验证安装

安装完成后，您可以尝试导入 NumPy 库来验证安装是否成功：

```python
import numpy as np

print(np.__version__)
```

这将打印您安装的 NumPy 版本号。

## NumPy 数组和基本操作

### 什么是 NumPy 数组？

NumPy 数组是相同数据类型的值的集合，这些值在内存中按一定顺序排列。每个数组都有一个形状（shape），它是一个元组，描述了数组每个维度的大小。

### 创建 NumPy 数组

可以使用多种方法创建 NumPy 数组，以下是一些常见方法：

1. **从 Python 列表或元组创建：**

```python
import numpy as np

# 从列表创建数组
list1 = [1, 2, 3, 4, 5]
array1 = np.array(list1)

# 从元组创建数组
tuple1 = (6, 7, 8, 9, 10)
array2 = np.array(tuple1)

print(array1)  # 输出: [1 2 3 4 5]
print(array2)  # 输出: [ 6  7  8  9 10]
```

2. **使用 NumPy 函数创建：**

```python
# 创建全零数组
zeros_array = np.zeros(5)  # 创建一个包含5个零的一维数组

# 创建全一数组
ones_array = np.ones((2, 3))  # 创建一个2x3的全一数组

# 创建等差数列
arange_array = np.arange(1, 10, 2)  # 创建一个从1到10，步长为2的数组

# 创建随机数组
random_array = np.random.rand(3, 4)  # 创建一个3x4的随机数组
```

### 数组属性

- **ndim:** 返回数组的维度数量。
- **shape:** 返回数组的形状，即每个维度的大小。
- **size:** 返回数组中元素的总数。
- **dtype:** 返回数组中元素的数据类型。

```python
array = np.array([[1, 2, 3], [4, 5, 6]])

print(array.ndim)  # 输出: 2
print(array.shape)  # 输出: (2, 3)
print(array.size)  # 输出: 6
print(array.dtype)  # 输出: int64
```

### 基本操作

- **访问元素:** 可以使用索引和切片访问数组中的元素。
- **算术运算:** 可以对数组进行加减乘除等算术运算。
- **数组函数:** NumPy 提供了大量的数组函数，例如求和、平均值、最大值、最小值等。

```python
# 访问元素
print(array[0, 1])  # 输出: 2

# 切片
print(array[:, 1:])  # 输出: [[2 3] [5 6]]

# 算术运算
print(array + 10)  # 每个元素都加10

# 数组函数
print(np.sum(array))  # 求和
print(np.mean(array))  # 求平均值
```

##  数学函数和统计方法

NumPy 提供了大量的数学函数和统计方法，可以方便地对数组进行各种计算。

### 数学函数

NumPy 提供了几乎所有常用的数学函数，例如：

- **三角函数：** `np.sin()`, `np.cos()`, `np.tan()`, `np.arcsin()`, `np.arccos()`, `np.arctan()`
- **指数和对数函数：** `np.exp()`, `np.log()`, `np.log10()`, `np.sqrt()`
- **舍入函数：** `np.round()`, `np.floor()`, `np.ceil()`
- **绝对值函数：** `np.abs()`
- **幂函数：** `np.power()`

```python
import numpy as np

a = np.array([1, 2, 3])

print(np.sin(a))  # 计算每个元素的正弦值
print(np.exp(a))  # 计算每个元素的指数值
print(np.round(a / 2))  # 将每个元素除以2并四舍五入
```

### 统计方法

NumPy 也提供了丰富的统计方法，可以方便地计算数组的统计指标，例如：

- **求和：** `np.sum()`
- **平均值：** `np.mean()`
- **标准差：** `np.std()`
- **方差：** `np.var()`
- **最小值：** `np.min()`
- **最大值：** `np.max()`
- **中位数：** `np.median()`
- **百分位数：** `np.percentile()`

```python
data = np.array([1, 3, 2, 4, 5])

print(np.sum(data))  # 计算所有元素的和
print(np.mean(data))  # 计算平均值
print(np.std(data))  # 计算标准差
print(np.min(data))  # 找到最小值
print(np.max(data))  # 找到最大值
```

### 沿着轴计算

许多 NumPy 函数可以沿着指定的轴进行计算，例如计算每行或每列的统计指标。可以通过 `axis` 参数指定计算的轴。

```python
matrix = np.array([[1, 2, 3],
                   [4, 5, 6]])

print(np.sum(matrix, axis=0))  # 计算每列的和
print(np.mean(matrix, axis=1))  # 计算每行的平均值
```

### 逻辑运算

NumPy 也支持对数组进行逻辑运算，例如：

- **大于：** `>`
- **小于：** `<`
- **等于：** `==`
- **不等于：** `!=`

```python
a = np.array([1, 2, 3])
b = np.array([3, 2, 1])

print(a > b)  # 输出: [False False  True]
print(a == b)  # 输出: [False  True False]
```

这些逻辑运算可以用于筛选数组中的元素，例如找到所有大于某个值的元素。

### 实践案例：使用 NumPy 分析学生考试成绩

假设我们有一组学生的考试成绩数据，存储在一个 CSV 文件中。数据包括每个学生的姓名、数学成绩、语文成绩和英语成绩。我们希望使用 NumPy 对这些数据进行分析，例如计算每个学生的总分、平均分、每门课的最高分、最低分和平均分等。

**1. 数据准备**

首先，我们需要将数据从 CSV 文件中加载到 NumPy 数组中。假设 CSV 文件名为 "grades.csv"，内容如下：

```
姓名,数学,语文,英语
张三,80,75,90
李四,90,85,80
王五,70,90,85
赵六,85,80,95
```

可以使用 NumPy 的 `genfromtxt()` 函数加载数据：

```python
import numpy as np

data = np.genfromtxt("grades.csv", delimiter=",", skip_header=1, dtype=str)
```

这将创建一个包含所有数据的 NumPy 数组，其中第一行是表头，因此使用 `skip_header=1` 跳过。`dtype=str` 指定所有数据都读取为字符串类型。

**2. 数据处理**

接下来，我们需要将数据进行一些处理，例如将姓名和成绩分开，并将成绩转换为数值类型。

```python
names = data[:, 0]  # 获取所有学生的姓名
scores = data[:, 1:].astype(float)  # 获取所有学生的成绩，并转换为浮点数类型
```

**3. 数据分析**

现在我们可以使用 NumPy 的各种函数对成绩数据进行分析了。

- **计算每个学生的总分和平均分：**

```python
total_scores = np.sum(scores, axis=1)  # 计算每行的总分
average_scores = np.mean(scores, axis=1)  # 计算每行的平均分
```

- **找到每门课的最高分、最低分和平均分：**

```python
math_max = np.max(scores[:, 0])  # 数学最高分
chinese_min = np.min(scores[:, 1])  # 语文最低分
english_avg = np.mean(scores[:, 2])  # 英语平均分
```

- **找到数学成绩高于平均分的学生：**

```python
above_average_math = names[scores[:, 0] > np.mean(scores[:, 0])]
```

**4. 结果展示**

最后，我们可以将分析结果打印出来：

```python
print("学生姓名：", names)
print("总分：", total_scores)
print("平均分：", average_scores)
print("数学最高分：", math_max)
print("语文最低分：", chinese_min)
print("英语平均分：", english_avg)
print("数学成绩高于平均分的学生：", above_average_math)
```

这只是一个简单的例子，展示了如何使用 NumPy 分析数据。您可以根据自己的需要，使用 NumPy 提供的各种函数对数据进行更复杂的分析。

## 广播（Broadcasting）和索引总结

广播和索引是 NumPy 中非常重要的概念，它们使得数组操作更加灵活高效。掌握这些技巧可以帮助您更方便地处理和分析数据。

### 广播 (Broadcasting)

广播是 NumPy 中一个强大的机制，它允许对不同形状的数组进行运算。在一定条件下，NumPy 可以自动扩展较小的数组以匹配较大数组的形状，从而使它们能够进行元素级的运算。

**广播的规则：**

1. **比较两个数组的形状，从后往前逐个维度比较。**
2. **如果两个维度的大小相等，或者其中一个维度的大小为 1，则可以进行广播。**
3. **如果两个维度的大小不相等，且都不是 1，则无法进行广播，会引发错误。**

**示例：**

```python
import numpy as np

# 创建一个 2x3 的数组
a = np.array([[1, 2, 3],
              [4, 5, 6]])

# 创建一个长度为 3 的一维数组
b = np.array([10, 20, 30])

# 将 b 广播到 a 的每一行
c = a + b
print(c)
# 输出：
# [[11 22 33]
#  [14 25 36]]
```

在这个例子中，`b` 的形状是 `(3,)`，而 `a` 的形状是 `(2, 3)`。根据广播规则，`b` 会被扩展为 `(1, 3)`，然后再复制成 `(2, 3)`，从而与 `a` 的形状匹配。

### 索引

NumPy 提供了多种索引数组元素的方法：

**1. 整数索引：**

与 Python 列表类似，可以使用整数索引访问数组中的单个元素或切片。

```python
# 获取第一行第二列的元素
print(a[0, 1])  # 输出：2

# 获取第一列的所有元素
print(a[:, 0])  # 输出：[1 4]
```

**2. 布尔索引：**

可以使用布尔数组作为索引，选择满足特定条件的元素。

```python
# 找到所有大于 3 的元素
mask = a > 3
print(a[mask])  # 输出：[4 5 6]
```

**3. 花式索引：**

可以使用整数数组作为索引，选择特定位置的元素。

```python
# 选择第 0 行和第 1 行，第 2 列和第 0 列的元素
indices = np.array([[0, 1], [2, 0]])
print(a[indices])
# 输出：
# [[3 1]
#  [6 4]]
```

**广播和索引的结合使用**

广播和索引可以结合使用，实现更灵活的数据操作。例如，可以使用广播对数组进行条件赋值：

```python
# 将所有大于 3 的元素替换为 0
a[a > 3] = 0
print(a)
# 输出：
# [[1 2 3]
#  [0 0 0]]
```

### 案例：图像处理中的广播和索引

#### 场景

假设我们有一张灰度图像，用一个 NumPy 数组表示，其中每个元素代表像素的亮度值（0-255）。我们希望对图像进行以下操作：

1. **提高图像亮度：** 将所有像素值增加 50。
2. **创建圆形遮罩：**  将图像中心区域以外的像素值设置为 0，形成一个圆形区域。

#### 代码实现

```python
import numpy as np
import matplotlib.pyplot as plt

# 创建一个 8x8 的示例图像
image = np.random.randint(0, 255, size=(8, 8))

# 1. 提高图像亮度
# 使用广播机制，将一个标量值加到整个数组
image_brighter = image + 50

# 2. 创建圆形遮罩
# 创建坐标网格
x, y = np.meshgrid(np.arange(8), np.arange(8))
# 计算每个像素点到中心的距离
distance = np.sqrt((x - 3.5)**2 + (y - 3.5)**2)
# 创建圆形遮罩，距离中心 3 以内的像素值为 True
mask = distance <= 3

# 使用布尔索引将遮罩应用于图像
image_masked = image_brighter.copy()  # 复制一份图像，避免修改原图像
image_masked[~mask] = 0  # 将遮罩外的像素值设为 0

# 可视化结果
plt.figure(figsize=(10, 4))

plt.subplot(1, 3, 1)
plt.imshow(image, cmap='gray')
plt.title('原始图像')

plt.subplot(1, 3, 2)
plt.imshow(image_brighter, cmap='gray')
plt.title('亮度增强')

plt.subplot(1, 3, 3)
plt.imshow(image_masked, cmap='gray')
plt.title('圆形遮罩')

plt.show()
```

#### 解释

1. **提高亮度：**  我们直接将一个标量值 `50`  加到图像数组 `image` 上。由于 NumPy 的广播机制，这个标量值会被自动扩展为与 `image` 相同形状的数组，然后进行元素级的加法运算。

2. **创建圆形遮罩：** 
   - 首先，我们使用 `np.meshgrid()` 创建一个坐标网格，表示每个像素的坐标。
   - 然后，我们计算每个像素点到图像中心 (3.5, 3.5) 的距离。
   - 接着，我们创建一个布尔数组 `mask`，其中距离中心小于等于 3 的像素值为 `True`，其他为 `False`。
   - 最后，我们使用布尔索引 `image_masked[~mask] = 0` 将 `mask`  应用于图像。`~mask` 表示对 `mask` 取反，即选择 `mask` 中值为 `False` 的元素。

#### 总结

这个案例展示了如何使用 NumPy 的广播和索引功能进行简单的图像处理操作。广播机制可以方便地对整个数组进行运算，而索引功能可以灵活地选择和修改数组中的元素。 

## NumPy 高级应用

在之前的章节中，我们学习了 NumPy 的基础知识，包括数组创建、操作、数学函数、广播和索引等。本章将介绍一些 NumPy 的高级应用，包括线性代数运算、傅里叶变换、随机数生成和结构化数组等，进一步拓展 NumPy 在数据科学领域的应用能力。

### 线性代数运算

NumPy 提供了 `numpy.linalg` 模块，包含了大量的线性代数运算函数，可以方便地进行矩阵运算、求解线性方程组、计算特征值和特征向量等操作。

**1.1 矩阵运算**

* `np.dot(a, b)`: 计算矩阵 a 和 b 的点积，即矩阵乘法。
* `np.transpose(a)`: 返回矩阵 a 的转置。
* `np.linalg.inv(a)`: 计算矩阵 a 的逆矩阵。

**1.2 求解线性方程组**

`np.linalg.solve(a, b)` 函数可以求解线性方程组 ax = b，其中 a 是系数矩阵，b 是常数向量。

```python
import numpy as np

# 定义系数矩阵和常数向量
a = np.array([[1, 2], [3, 4]])
b = np.array([5, 6])

# 求解线性方程组
x = np.linalg.solve(a, b)

# 打印结果
print(x)  # 输出: [-4.  4.5]
```

**1.3 特征值和特征向量**

`np.linalg.eig(a)` 函数可以计算矩阵 a 的特征值和特征向量。

```python
import numpy as np

# 定义矩阵
a = np.array([[1, 2], [3, 4]])

# 计算特征值和特征向量
eigenvalues, eigenvectors = np.linalg.eig(a)

# 打印结果
print("特征值:", eigenvalues)
print("特征向量:", eigenvectors)
```

### 傅里叶变换

傅里叶变换是一种将信号从时域转换到频域的数学工具，在信号处理、图像处理等领域有着广泛的应用。NumPy 提供了 `numpy.fft` 模块，可以进行快速傅里叶变换 (FFT) 和逆变换 (IFFT)。

* `np.fft.fft(a)`: 对数组 a 进行快速傅里叶变换。
* `np.fft.ifft(a)`: 对数组 a 进行快速傅里叶逆变换。

```python
import numpy as np
import matplotlib.pyplot as plt

# 生成一个示例信号
t = np.arange(0, 1, 0.01)
signal = np.sin(2*np.pi*5*t) + np.sin(2*np.pi*10*t)

# 进行快速傅里叶变换
fft_result = np.fft.fft(signal)

# 计算频率轴
freq = np.fft.fftfreq(signal.size, d=0.01)

# 绘制原始信号和频谱图
plt.figure(figsize=(12, 4))

plt.subplot(1, 2, 1)
plt.plot(t, signal)
plt.title("Original Signal")

plt.subplot(1, 2, 2)
plt.plot(freq, np.abs(fft_result))
plt.title("Frequency Spectrum")

plt.show()
```

### 随机数生成

NumPy 提供了 `numpy.random` 模块，可以生成各种分布的随机数，用于模拟、统计分析等。

* `np.random.rand(d0, d1, ..., dn)`: 生成服从均匀分布的随机数，取值范围在 [0, 1) 之间。
* `np.random.randn(d0, d1, ..., dn)`: 生成服从标准正态分布的随机数，均值为 0，标准差为 1。
* `np.random.randint(low, high, size)`: 生成指定范围内的随机整数，范围为 [low, high)。

```python
import numpy as np

# 生成服从均匀分布的随机数
uniform_random = np.random.rand(2, 3)

# 生成服从标准正态分布的随机数
normal_random = np.random.randn(2, 3)

# 生成指定范围内的随机整数
integer_random = np.random.randint(1, 10, size=(2, 3))

print("均匀分布随机数：\n", uniform_random)
print("标准正态分布随机数：\n", normal_random)
print("指定范围内的随机整数：\n", integer_random)
```

### 结构化数组

NumPy 可以创建结构化数组，用于存储不同类型的数据，类似于 C 语言中的结构体。

```python
import numpy as np

# 创建一个存储学生信息的结构化数组
student_dtype = np.dtype([('name', 'U10'), ('age', 'i4'), ('scores', 'f8', (3,))])
students = np.zeros(3, dtype=student_dtype)

# 为数组赋值
students[0] = ('Alice', 18, (90, 85, 92))
students[1] = ('Bob', 19, (80, 88, 95))
students[2] = ('Charlie', 20, (95, 90, 87))

# 打印数组内容
print(students)

# 访问结构化数组的字段
print(students['name'])  # 打印所有学生的姓名
print(students[0]['age'])  # 打印第一个学生的年龄
print(students[1]['scores'])  # 打印第二个学生的所有成绩
```

### 总结

本章介绍了 NumPy 的一些高级应用，包括线性代数运算、傅里叶变换、随机数生成和结构化数组等。这些功能使得 NumPy 成为数据科学领域不可或缺的工具之一，可以帮助我们更高效地进行数据分析、机器学习等工作。 

## 案例：使用 NumPy 分析 Nginx 日志数据

### 场景

我们希望分析一段时间内的 Nginx 服务器日志，提取关键信息并进行统计分析，例如：

1.  **请求数量统计:** 统计每天的请求总数。
2.  **状态码分布:** 分析不同 HTTP 状态码的出现频率。
3.  **访问峰值时间段:** 找出每天访问量最大的小时段。

```
199.72.81.55 - - [01/Jul/1995:00:00:01 -0400] "GET /history/apollo/ HTTP/1.0" 200 6245
unicomp6.unicomp.net - - [01/Jul/1995:00:00:06 -0400] "GET /shuttle/countdown/ HTTP/1.0" 200 3985
199.120.110.21 - - [01/Jul/1995:00:00:09 -0400] "GET /shuttle/missions/sts-73/mission-sts-73.html HTTP/1.0" 200 4085
burger.letters.com - - [01/Jul/1995:00:00:11 -0400] "GET /shuttle/countdown/liftoff.html HTTP/1.0" 304 0
199.120.110.21 - - [01/Jul/1995:00:00:11 -0400] "GET /shuttle/missions/sts-73/sts-73-patch-small.gif HTTP/1.0" 200 4179
burger.letters.com - - [01/Jul/1995:00:00:12 -0400] "GET /images/NASA-logosmall.gif HTTP/1.0" 304 0
burger.letters.com - - [01/Jul/1995:00:00:12 -0400] "GET /shuttle/countdown/video/livevideo.gif HTTP/1.0" 200 0
205.212.115.106 - - [01/Jul/1995:00:00:12 -0400] "GET /shuttle/countdown/countdown.html HTTP/1.0" 200 3985
d104.aa.net - - [01/Jul/1995:00:00:13 -0400] "GET /shuttle/countdown/ HTTP/1.0" 200 3985
129.94.144.152 - - [01/Jul/1995:00:00:13 -0400] "GET / HTTP/1.0" 200 7074
```

提供的 Nginx 日志示例中，每一行代表一条访问记录，每个字段由空格分隔，含义如下：

1. **`199.72.81.55` (remote_addr):** 客户端的 IP 地址，这里表示发起请求的客户端地址是 `199.72.81.55`。
2. **`-` (remote_ident):**  远程用户身份，由客户端 identd 服务提供，通常为空白("-")。
3. **`-` (remote_user):**  HTTP 认证的用户名称，如果没有认证则显示为"-"。
4. **`[01/Jul/1995:00:00:01 -0400]` (time_local):**  服务器记录请求的时间，格式为 `[日/月/年:时:分:秒 时区]`。 
    - 这里表示 1995 年 7 月 1 日 00:00:01，时区是 -0400。
5. **`"GET /history/apollo/ HTTP/1.0"` (request):**  客户端发起的 HTTP 请求信息，包含三个部分：
    - **`GET`:**  HTTP 请求方法，这里是获取资源的 GET 方法。
    - **`/history/apollo/`:**  请求的资源路径，这里是根目录下的 `/history/apollo/` 路径。
    - **`HTTP/1.0`:**  使用的 HTTP 协议版本，这里是 HTTP/1.0。
6. **`200` (status):**  服务器返回的 HTTP 状态码，200 表示请求成功。
7. **`6245` (body_bytes_sent):**  服务器发送给客户端的响应体字节数，不包括响应头的大小。

### 数据准备

数据下载链接：https://pan.baidu.com/s/1ybfJWcVhDrDe_1LBcw8UPw?pwd=maoh

假设我们已经将 Nginx 日志文件 "access_log_Aug95" 下载到本地

### 代码实现

```python
import re
from datetime import datetime
import numpy as np

# 读取日志文件
with open("./data/access_log_Aug95", "r", encoding="utf-8", errors="ignore") as f:
    logs = f.readlines()

# 1. 数据预处理
# 创建一个结构化数组存储提取的信息
log_dtype = np.dtype(
    [
        ("remote_addr", "U20"),  # 远程IP地址
        ("time_local", "datetime64[s]"),  # 请求时间
        ("request", "U100"),  # 请求路径
        ("status", "i4"),  # HTTP状态码
        ("body_bytes_sent", "i4"),  # 发送字节数
    ]
)
parsed_logs = np.zeros(len(logs), dtype=log_dtype)

# 正则表达式匹配日志行
log_pattern = re.compile(
    r'(?P<remote_addr>\S+) - - \[(?P<time_local>[^\]]+)\] "(?P<request>[^"]+)" (?P<status>\d{3}) (?P<body_bytes_sent>-|\d+)'
)

# 解析日志文件，提取关键信息
for i, log in enumerate(logs):
    match = log_pattern.match(log)

    if match:
        remote_addr = match.group("remote_addr")
        time_local_str = match.group("time_local")
        request = match.group("request")
        status = int(match.group("status"))
        body_bytes_sent = match.group("body_bytes_sent")
        body_bytes_sent = int(body_bytes_sent) if body_bytes_sent != "-" else 0

        # 去掉时区部分
        time_local_str = time_local_str[:-6]  # 去掉最后的时区信息（例如 -0400）

        # 解析日期和时间
        dt_object = datetime.strptime(time_local_str, "%d/%b/%Y:%H:%M:%S")

        parsed_logs[i] = (
            remote_addr,  # 远程IP地址
            np.datetime64(dt_object),  # 请求时间
            request,  # 请求路径
            status,  # HTTP状态码
            body_bytes_sent,  # 发送字节数
        )

# 2. 请求数量统计
# 提取日期信息
dates = np.array(parsed_logs["time_local"].astype("datetime64[D]"))
unique_dates, counts = np.unique(dates, return_counts=True)
print("每天请求数量：", dict(zip(unique_dates.astype(str), counts)))

# 3. 状态码分布
unique_status, status_counts = np.unique(parsed_logs["status"], return_counts=True)
print("状态码分布：", dict(zip(unique_status, status_counts)))

# 4. 访问峰值时间段
hours = np.array(parsed_logs["time_local"].astype("datetime64[h]")).astype(int) % 24
unique_hours, hour_counts = np.unique(hours, return_counts=True)

# 找到访问量最大的小时
peak_hour = unique_hours[np.argmax(hour_counts)]
print("访问峰值时间段：", peak_hour)

# 5. 每天访问量最大的小时段
print("\n每天访问量最大的小时段：")
for date in np.unique(dates):
    daily_hours = hours[dates == date]
    unique_daily_hours, daily_hour_counts = np.unique(daily_hours, return_counts=True)
    peak_hour = unique_daily_hours[np.argmax(daily_hour_counts)]
    print(f"{date.astype(str)}: {peak_hour} 点 - {daily_hour_counts.max()} 次请求")
```

清洗数据要点

* access_log不可避免的存在错误，注意使用`errors="ignore"`忽略错误
* request路径也可以出现异常，比如`198.213.130.253 - - [03/Aug/1995:11:29:02 -0400] "GET /shuttle/missions/sts-34/mission-sts-34.html"><IMG images/ssbuv1.gif SRC="images/small34p.gif/ HTTP/1.0" 404 -`，路径中包含空格，需要用正则表达式分割日志，而不是简单的使用空格分割。

### 解释

1. **数据预处理:**  
   - 首先，我们定义了一个结构化数组 `log_dtype` 来存储从日志中提取的信息，包括 IP 地址、时间、请求路径、状态码和发送字节数。
   - 然后，我们遍历日志文件，使用字符串分割和类型转换提取关键信息，并将它们存储到结构化数组中。
2. **请求数量统计:**
   - 我们使用 `np.unique()` 函数统计每天出现的唯一日期以及对应的请求数量。
3. **状态码分布:**
   - 同样使用 `np.unique()` 函数统计不同状态码的出现次数。
4. **访问峰值时间段:**
   - 我们将时间信息转换为小时，并使用 `np.argmax()` 函数找到访问量最大的小时索引。

### 总结

这个案例展示了如何使用 NumPy 分析 Nginx 日志数据，提取关键信息并进行统计分析。通过灵活运用 NumPy 的数组操作、数据类型、统计函数等功能，我们可以快速地从原始日志数据中挖掘出有价值的信息。 

## 练习：分析 Nginx 日志，统计访问频率最高的资源路径

### 目标

1. **统计每个独立资源路径的访问次数。** 例如，`/history/apollo/` 和 `/history/apollo/index.html`  应该被视为两个不同的资源路径。
2. **找出访问频率最高的 10 个资源路径。**

### 数据

使用之前提供的 Nginx 日志数据

### 提示

1. **数据准备:**

   - 使用类似之前案例的方法，将日志数据读取到一个 NumPy 结构化数组中。建议存储以下字段：
     - `request`:  完整的请求信息，包含请求方法、路径和协议版本。
     - `request_path`:  仅包含资源路径的部分，需要从 `request` 字段中提取。

2. **提取资源路径:**

   - 使用 `np.char.split()` 函数，以空格为分隔符分割 `request` 字段，获取包含请求方法、路径和协议版本的列表。
   - 从分割后的列表中取出第二个元素（索引为 1），即为资源路径。将其存储到 `request_path` 字段。

3. **统计访问次数:**

   - 使用 `np.unique()` 函数，获取所有独立的资源路径，并统计每个路径出现的次数。

4. **排序和筛选:**

   - 使用 `np.argsort()` 函数对访问次数进行降序排序，得到排序后的索引数组。
   - 使用切片操作获取访问次数最多的前 10 个资源路径的索引。
   - 根据索引数组，从排序后的资源路径和访问次数数组中获取最终结果。
