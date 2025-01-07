# JSON

JSON的全称是”JavaScript Object Notation”，意思是JavaScript对象表示法，它是一种基于文本，独立于语言的轻量级数据交换格式。

![img](JSON.assets/761770-20170914230529391-1432518430.png)

XML也是一种数据交换格式，为什么没有选择XML呢？因为XML虽然可以作为跨平台的数据交换格式，但是在JS(JavaScript的简写)中处理XML非常不方便，同时XML标记比数据多，增加了交换产生的流量，而JSON没有附加的任何标记，在JS中可作为对象处理，所以我们更倾向于选择JSON来交换数据。

## JSON vs XML

JSON 和 XML在写法上有所不同，如下所示：

### JSON 实例

```json
{
    "sites": [
    { "name":"菜鸟教程" , "url":"www.runoob.com" }, 
    { "name":"google" , "url":"www.google.com" }, 
    { "name":"微博" , "url":"www.weibo.com" }
    ]
}
```

### XML 实例

```xml
<sites>
  <site>
    <name>菜鸟教程</name> <url>www.runoob.com</url>
  </site>
  <site>
    <name>google</name> <url>www.google.com</url>
  </site>
  <site>
    <name>微博</name> <url>www.weibo.com</url>
  </site>
</sites>
```

JSON 与 XML 的相同之处：

- JSON 和 XML 数据都是 "自我描述" ，都易于理解。
- JSON 和 XML 数据都是有层次的结构
- JSON 和 XML 数据可以被大多数编程语言使用

JSON 与 XML 的不同之处：

- JSON 不需要结束标签
- JSON 更加简短
- JSON 读写速度更快
- JSON 可以使用数组

> **最大的不同是**：XML 需要使用 XML 解析器来解析，JSON 可以使用标准的 JavaScript 函数来解析。
>
> - `JSON.parse()`: 将一个 JSON 字符串转换为 JavaScript 对象。
> - `JSON.stringify()`: 于将 JavaScript 值转换为 JSON 字符串。

------

### 为什么 JSON 比 XML 更好？

* XML 比 JSON 更难解析。
* JSON 可以直接使用现有的 JavaScript 对象解析。
* 针对 AJAX 应用，JSON 比 XML 数据加载更快，而且更简单：

#### 使用 XML

- 获取 XML 文档
- 使用 XML DOM 迭代循环文档
- 接数据解析出来复制给变量

#### 使用 JSON

- 获取 JSON 字符串
- JSON.Parse 解析 JSON 字符串

## JSON的两种结构

JSON有两种表示结构，对象和数组。
对象结构以”{”大括号开始，以”}”大括号结束。中间部分由0或多个以”，”分隔的”key(关键字)/value(值)”对构成，关键字和值之间以”：”分隔，语法结构如代码。

```json
{
    key1:value1,
    key2:value2,
    ...
}
```

其中关键字是字符串，而值可以是字符串，数值，true，false，null，对象或数组

- 数字（整数或浮点数）
- 字符串（在双引号中）
- 逻辑值（true 或 false）
- 数组（在中括号中）
- 对象（在大括号中）
- null

举例

```json
{ "name":"菜鸟教程" , "url":"www.runoob.com" }
```



数组结构以”[”开始，”]”结束。中间由0或多个以”，”分隔的值列表组成，语法结构如代码。

```json
[
    {
        key1:value1,
        key2:value2 
    },
    {
         key3:value3,
         key4:value4   
    }
]
```

举例

```json
{
    "sites": [
        { "name":"菜鸟教程" , "url":"www.runoob.com" }, 
        { "name":"google" , "url":"www.google.com" }, 
        { "name":"微博" , "url":"www.weibo.com" }
    ]
}
```

## 认识JSON字符串

字符串：这个很好解释，指使用“”双引号或’’单引号包括的字符。例如：

```javascript
var comStr = 'this is string';
```

json字符串：指的是符合json格式要求的js字符串。例如：

```javascript
var jsonStr = "{StudentID:'100',Name:'tmac',Hometown:'usa'}";
```

json对象：指符合json格式要求的js对象。例如：

```javascript
var jsonObj = { StudentID: "100", Name: "tmac", Hometown: "usa" };
```

## JSON.parse()

> :zap:**将JSON数据解析为Javascript对象**
>
> ---
>
> JSON 通常用于与服务端交换数据。
>
> 在接收服务器数据时一般是字符串。
>
> 我们可以使用 JSON.parse() 方法将数据转换为 JavaScript 对象。

### 语法

```javascript
JSON.parse(text[, reviver])
```

### JSON 解析实例

例如我们从服务器接收了以下数据：

```json
{ "name":"runoob", "alexa":10000, "site":"www.runoob.com" }
```

我们使用 JSON.parse() 方法处理以上数据，将其转换为 JavaScript 对象：

```javascript
var obj = JSON.parse('{ "name":"runoob", "alexa":10000, "site":"www.runoob.com" }');
```

## JSON.stringify()

> :zap:**将对象序列化为JSON字符串**
>
> ---
>
> JSON 通常用于与服务端交换数据。
>
> 在向服务器发送数据时一般是字符串。
>
> 我们可以使用 JSON.stringify() 方法将 JavaScript 对象转换为字符串。

### 语法

```javascript
JSON.stringify(value[, replacer[, space]])
```

### JavaScript 对象转换

例如我们向服务器发送以下数据：

```javascript
var obj = { "name":"runoob", "alexa":10000, "site":"www.runoob.com"};
```

我们使用 JSON.stringify() 方法处理以上数据，将其转换为字符串：

```javascript
var myJSON = JSON.stringify(obj);
```

myJSON 为字符串。

我们可以将 myJSON 发送到服务器：

## 在JS中如何使用JSON

JSON是JS的一个子集，所以可以在JS中轻松地读，写JSON。读和写JSON都有两种方法，分别是利用”`.`”操作符和“`[key]`”的方式。

### 定义一个JSON对象

```javascript
var obj = {
            1: "value1",
            "2": "value2",
            count: 3,
            person: [ //数组结构JSON对象，可以嵌套使用
                        {
                            id: 1,
                            name: "张三"
                        },
                        {
                            id: 2,
                            name: "李四"
                        }
                   ],
            object: { //对象结构JSON对象
                id: 1,
                msg: "对象里的对象"    
            }
        };
```

### 从JSON中读数据

```javascript
function ReadJSON() {
            alert(obj.1); //会报语法错误，可以用alert(obj["1"]);说明数字最好不要做关键字
            alert(obj.2); //同上

            alert(obj.person[0].name); //或者alert(obj.person[0]["name"])
            alert(obj.object.msg); //或者alert(obj.object["msg"])
        }
```

### 向JSON中写数据

比如要往JSON中增加一条数据，代码如下：

```javascript
function Add() { 
            //往JSON对象中增加了一条记录
            obj.sex= "男" //或者obj["sex"]="男"
        }
```

增加数据后的JSON对象如图：

![json01](JSON.assets/08225650-078d12d29f9748c8b87fa022a8b50e38.jpg)

### 修改JSON中的数据

我们现在要修改JSON中count的值，代码如下：

```javascript
function Update() {
            obj.count = 10; //或obj["count"]=10
        }
```

修改后的JSON如图。

[![json02](JSON.assets/08225657-87384c796ecf4035b206c7e9432769c3.jpg)](https://images0.cnblogs.com/blog/311549/201306/08225654-7373ca8222ad4b999701ce3f988d5d68.jpg)

### 删除JSON中的数据

我们现在实现从JSON中删除count这条数据，代码如下：

```javascript
function Delete() {
            delete obj.count;
        }
```

删除后的JSON如图

![json03](JSON.assets/08225702-4a2ce57875bc4b0b8efe13eedcbd14df.jpg)

可以看到count已经从JSON对象中被删除了。

### 遍历JSON对象

可以使用for…in…循环来遍历JSON对象中的数据，比如我们要遍历输出obj对象的值，代码如下：

```javascript
function Traversal() {
            for (var c in obj) {
                console.log(c + ":", obj[c]);
            }
        }
```

程序输出结果为：

![json04](JSON.assets/08225707-40f4c05d2ae644368f4af6f281035220.jpg)