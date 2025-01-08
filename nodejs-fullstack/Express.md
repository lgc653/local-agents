# Express 

Express 是一个保持最小规模的灵活的 Node.js Web 应用程序开发框架，为 Web 和移动应用程序提供一组强大的功能。

## 安装

首先假定你已经安装了 [Node.js](https://nodejs.org/)，接下来为你的应用创建一个目录，然后进入此目录并将其作为当前工作目录。

```sh
$ mkdir myapp
$ cd myapp
```

通过 `npm init` 命令为你的应用创建一个 `package.json` 文件。 欲了解 `package.json` 是如何起作用的，请参考 [Specifics of npm’s package.json handling](https://docs.npmjs.com/files/package.json).

```sh
$ npm init
```

此命令将要求你输入几个参数，例如此应用的名称和版本。 你可以直接按“回车”键接受大部分默认设置即可，下面这个除外：

```sh
entry point: (index.js)
```

键入 `app.js` 或者你所希望的名称，这是当前应用的入口文件。如果你希望采用默认的 `index.js` 文件名，只需按“回车”键即可。

接下来在 `expressjs`目录下安装 Express 并将其保存到依赖列表中。如下：

```sh
$ npm install express --save
```

如果只是临时安装 Express，不想将它添加到依赖列表中，可执行如下命令：

```sh
$ npm install express --no-save
```

## Hello world

```javascript
const express = require('express')
const app = express()

app.get('/', (req, res) => res.send('Hello World!'))

app.listen(3000, () => console.log('Example app listening on port 3000!'))
```

```sh
$ node app.js
```

然后打开http://localhost:3000/就能看到效果了

## Express 应用程序生成器

通过应用生成器工具 `express-generator` 可以快速创建一个应用的骨架。

`express-generator` 包含了 `express` 命令行工具。通过如下命令即可安装：

```sh
$ npm install express-generator -g
```

`-h` 参数可以列出所有可用的命令行参数：

```sh
$ express -h

  Usage: express [options] [dir]

  Options:

    -h, --help          输出使用方法
        --version       输出版本号
    -e, --ejs           添加对 ejs 模板引擎的支持
        --hbs           添加对 handlebars 模板引擎的支持
        --pug           添加对 pug 模板引擎的支持
    -H, --hogan         添加对 hogan.js 模板引擎的支持
        --no-view       创建不带视图引擎的项目
    -v, --view <engine> 添加对视图引擎（view） <engine> 的支持 (ejs|hbs|hjs|jade|pug|twig|vash) （默认是 jade 模板引擎）
    -c, --css <engine>  添加样式表引擎 <engine> 的支持 (less|stylus|compass|sass) （默认是普通的 css 文件）
        --git           添加 .gitignore
    -f, --force         强制在非空目录下创建
```

例如，如下命令创建了一个名称为 *expressjs* 的 Express 应用。此应用将在当前目录下的 *myapp* 目录中创建，并且设置为使用 [Pug](https://pugjs.org/) 模板引擎（view engine）：

```sh
$ express --view=ejs expressjs
```

然后安装所有依赖包：

```sh
$ cd expressjs
$ npm install
```

在 MacOS 或 Linux 中，通过如下命令启动此应用：

```sh
$ DEBUG=expressjs:* npm start
```

在 Windows 中，通过如下命令启动此应用：

```sh
> set DEBUG=expressjs:* & npm start
```

然后在浏览器中打开 `http://localhost:3000/` 网址就可以看到这个应用了。

通过生成器创建的应用一般都有如下目录结构：

```sh
.
├── app.js
├── bin
│   └── www
├── package.json
├── public
│   ├── images
│   ├── javascripts
│   └── stylesheets
│       └── style.css
├── routes
│   ├── index.js
│   └── users.js
└── views
    ├── error.pug
    ├── index.pug
    └── layout.pug

7 directories, 9 files
```

>  通过 Express 应用生成器创建应用只是众多方法中的一种。你可以不使用它，也可以修改它让它符合你的需求。

## 路由

```javascript
// app.METHOD(PATH, HANDLER)
app.get('/', function (req, res) {
  res.send('Hello World!')
})
app.post('/', function (req, res) {
  res.send('Got a POST request')
})
app.put('/user', function (req, res) {
  res.send('Got a PUT request at /user')
})
app.delete('/user', function (req, res) {
  res.send('Got a DELETE request at /user')
})
```

## 利用 Express 托管静态文件

为了提供诸如图像、CSS 文件和 JavaScript 文件之类的静态文件，请使用 Express 中的 `express.static` 内置中间件函数。

此函数特征如下：

```javascript
express.static(root, [options])
```

例如，通过如下代码就可以将 `public` 目录下的图片、CSS 文件、JavaScript 文件对外开放访问了：

```javascript
app.use(express.static('public'))
```

现在，你就可以访问 `public` 目录中的所有文件了：

```plain-text
http://localhost:3000/images/kitten.jpg
http://localhost:3000/css/style.css
http://localhost:3000/js/app.js
http://localhost:3000/images/bg.png
http://localhost:3000/hello.html
```

Express 在静态目录查找文件，因此，存放静态文件的目录名不会出现在 URL 中。

如果要使用多个静态资源目录，请多次调用 `express.static` 中间件函数：

```javascript
app.use(express.static('public'))
app.use(express.static('files'))
```

访问静态资源文件时，`express.static` 中间件函数会根据目录的添加顺序查找所需的文件。

## 通过Express开发RESTful API

```sh
npm install mongodb
npm install lionsoul-ip2region --save
"c:\Tools\mongodb\bin\mongod.exe" --config c:\Dev\mongodb\mongo.conf
```

express获取参数有三种方法：官网实例： 

* Checks route params (req.params), ex: /user/:id 
* Checks query string params (req.query), ex: ?id=12 
* Checks urlencoded body params (req.body), ex: id=

```javascript
var express = require("express");
var router = express.Router();
var MongoClient = require("mongodb").MongoClient;

/* GET users listing. */
router.post("/:app_uuid", function(req, res, next) {
	console.log(req.params);
	// 此处注意，此处有windows平台用localhost连接比127.0.0.1慢N倍的坑
	var url = "mongodb://adsadmin:adsadmin@127.0.0.1:27017/ads?maxPoolSize=10";
	MongoClient.connect(
		url,
		function(err, db) {
			if (err) throw err;
			var dbo = db.db("ads");
			var whereStr = { app_uuid: req.params.app_uuid };
			dbo.collection("app")
				.find(whereStr)
				.toArray(function(err, result) {
					// 返回集合中所有数据
					if (err) throw err;
					console.log(result);
					var whereStr = { app_uuid: req.params.app_uuid };
					const searcher = require("lionsoul-ip2region").create();
					const region = searcher.btreeSearchSync("27.18.165.1");
					console.dir(region);
					dbo.collection("ad")
						.find({ ad_type: "self" })
						.sort({ weight: -1 })
						.limit(4)
						.toArray(function(err, result) {
							// 返回集合中所有数据
							if (err) throw err;
							// console.log(result);
							res.json(result); //以json格式输出
							let timeUnix = Date.parse(new Date()) / 1000;
							dbo.collection("client").findAndModify(
								{ client_uuid: req.body.client_uuid }, // query
								[["_id", "asc"]], // sort order
								{ $set: { client_uuid: req.body.client_uuid, time: timeUnix } }, // replacement, replaces only the field "hi"
								{ new: true, upsert: true }, // options
								function(err, object) {
									if (err) {
										console.warn(err.message); // returns error if no matching object found
									} else {
										console.dir(object);
										db.close();
									}
								}
							);
						});
				});
		}
	);
});

router.post("/await/:app_uuid", function(req, res, next) {
	(async function() {
		// 此处注意，此处有windows平台用localhost连接比127.0.0.1慢N倍的坑
		var url = "mongodb://adsadmin:adsadmin@127.0.0.1:27017/ads?maxPoolSize=10";
		const db = await MongoClient.connect(url);
		let dbo = await db.db("ads");
		var whereStr = { app_uuid: req.params.app_uuid };
		let resultApp = await dbo
			.collection("ad")
			.find({ ad_type: "self" })
			.sort({ weight: -1 })
			.limit(4)
			.toArray();
		const searcher = require("lionsoul-ip2region").create();
		const region = searcher.btreeSearchSync("27.18.165.1");
		console.dir(region);
		let resultAds = await dbo
			.collection("ad")
			.find({ ad_type: "self" })
			.sort({ weight: -1 })
			.limit(4)
			.toArray();
		let timeUnix = Date.parse(new Date()) / 1000;
		let object = await dbo.collection("client").findAndModify(
			{ client_uuid: req.body.client_uuid }, // query
			[["_id", "asc"]], // sort order
			{ $set: { client_uuid: req.body.client_uuid, time: timeUnix } }, // replacement, replaces only the field "hi"
			{ new: true, upsert: true }
		);
		console.dir(object);
		await db.close();
		res.json(resultAds);
	})();
});

module.exports = router;
```

## 项目示例

本项目综合运用了EJS 模板语言 + RESTful API

> 随着时代的发展，Express多被用于RESTful API的开发，EJS 模板语言的应用越来越少了。

### 项目架构

```mermaid
graph LR
    subgraph 前端
        A[index.ejs] --> B(header.ejs)
        A --> C(footer.ejs)
        A -- Ajax 请求 --> D["/task/get"]
        A -- Ajax 请求 --> E["/task/update"]
        A -- Ajax 请求 --> F["/task/delete"]
        C --> L[page.index.js]
    end
    subgraph 后端
        D["/task/get"] --> M[index.js]
        E["/task/update"] --> M
        F["/task/delete"] --> M
        M -- 数据库操作 --> N[task_management 数据库]
    end
    N -- 数据 --> M
    M -- 渲染 --> A
```

**说明:**

*   **index.ejs**: 主页面模板，包含了任务列表的 HTML 结构。它通过 `include` 指令引入 `header.ejs` 和 `footer.ejs`。
*   **header.ejs**: 页面头部模板，包含了 `<head>` 部分，例如标题、CSS 链接等。
*   **footer.ejs**: 页面底部模板，包含了 `<script>` 部分，用于引入 JavaScript 文件。
*   **page.index.js**: 页面特定的 JavaScript 逻辑，例如处理 Ajax 请求、操作 DOM 等。
*   **index.js**: 后端路由处理程序，处理 `/task/get`、`/task/update` 和 `/task/delete` 请求。
*   **task_management 数据库**: 存储任务数据的数据库。

**流程:**

1.  用户访问网站，服务器渲染 `index.ejs` 模板，生成 HTML 页面并返回给浏览器。
2.  浏览器加载页面，并执行 `page.index.js` 中的 JavaScript 代码。
3.  用户在页面上进行操作，例如点击“编辑”或“删除”按钮，触发 Ajax 请求。
4.  `page.index.js` 发送 Ajax 请求到后端相应的路由，例如 `/task/update` 或 `/task/delete`。
5.  `index.js` 接收请求，并与 `task_management` 数据库交互，执行相应的数据库操作。
6.  `index.js` 将操作结果返回给前端。
7.  `page.index.js` 接收后端返回的结果，并更新页面。

### index.ejs

```ejs
<% include header.ejs %>
<div>
	<h1>任务列表</h1>
	<p><div class="alert alert-info" role="alert">
		提示：双击日期时间即可修改
	</div></p>
	<table class="table table-striped">
		<thead>
			<tr>
				<th>任务名称</th>
				<th>开始时间</th>
				<th>结束时间</th>
				<th>状态</th>  <!-- 新增状态列 -->
				<th>操作</th>
			</tr>
		</thead>
		<tbody>
			<% for(var i=0; i<tasks.length; i++) { %>
			<tr>
				<td><%= tasks[i].taskName %></td>
				<td>
					<input id="startTime<%= tasks[i].id %>" type="text" value="<%= tasks[i].startTime %>" readonly class="form_datetime">
				</td>
				<td>
					<input id="endTime<%= tasks[i].id %>" type="text" value="<%= tasks[i].endTime %>" readonly class="form_datetime">
				</td>
				<td><%= tasks[i].status %></td> <!-- 显示任务状态 -->
				<td>
					<input id="btnEdit<%= tasks[i].id %>" class="btn btn-primary btnEdit" type="button" value="编辑" data-id="<%= tasks[i].id %>">
					<input id="btnDelete<%= tasks[i].id %>" class="btn btn-danger btnDelete" type="button" value="删除" data-id="<%= tasks[i].id %>">
				</td>
			</tr>
			<% } %>
		</tbody>
	</table>
</div>
<% include footer.ejs %>
```


### header.ejs

```ejs
<!DOCTYPE html>
<html lang="zh-CN">
<head>
<title><%= title %></title>
<link rel='stylesheet' href='/stylesheets/style.css' />
<link rel='stylesheet' href='/stylesheets/datetimepicker.css' />
</head>
<body>
```

### footer.ejs

```ejs
<script src="/js/LAB.min.js"></script>
<script src="/js/init.js"></script>
<script type="text/javascript">
$LAB
.script(arrjs).wait()
.script("/js/global.js")
.script("/js/page.<%= pageCode %>.js")
.wait(function(){
});
</script>
</body>
</html>
```

### page.index.js

```js
(function($) {
    $(".form_datetime").datetimepicker({
        format: 'yyyy-mm-dd hh:ii:ss',
        autoclose: true,
        language: "zh-CN"
    });

    // 编辑按钮点击事件
    $(".btnEdit").click(function() {
        var id = $(this).data("id");
        var startTimeInput = $("#startTime" + id);
        var endTimeInput = $("#endTime" + id);

        // 切换输入框的只读状态
        startTimeInput.prop("readonly", !startTimeInput.prop("readonly"));
        endTimeInput.prop("readonly", !endTimeInput.prop("readonly"));

        // 如果输入框变为可编辑状态，则显示保存按钮
        if (!startTimeInput.prop("readonly")) {
            $(this).val("保存");
            $(this).removeClass("btnEdit").addClass("btnSave"); // 更改class以区分编辑和保存状态
        }
    });


    // 保存按钮点击事件 (动态绑定)
    $(document).on("click", ".btnSave", function() {
        var id = $(this).data("id");
        var startTime = $("#startTime" + id).val();
        var endTime = $("#endTime" + id).val();

        $.ajax({
            url: '/task/update',
            type: 'POST',
            data: { id: id, startTime: startTime, endTime: endTime },
            dataType: 'json',
            success: function(response) {
                if (response.flg) {
                    showAlertPanel("更新成功！");
                    // 更新按钮状态
                    $(`#btnEdit${id}`).val("编辑").removeClass("btnSave").addClass("btnEdit");
                    $("#startTime" + id).prop("readonly", true);
                    $("#endTime" + id).prop("readonly", true);
                } else {
                    showAlertPanel("更新失败：" + response.err);
                }
            },
            error: function() {
                showAlertPanel("更新失败：网络错误");
            }
        });
    });

    // 删除按钮点击事件
    $(".btnDelete").click(function() {
        var id = $(this).data("id");
        if (confirm("确定要删除此任务吗？")) {
            $.ajax({
                url: '/task/delete',
                type: 'POST',
                data: { id: id },
                dataType: 'json',
                success: function(response) {
                    if (response.flg) {
                        showAlertPanel("删除成功！");
                        // 移除对应的行
                        $(`#btnEdit${id}`).closest('tr').remove();
                    } else {
                        showAlertPanel("删除失败：" + response.err);
                    }
                },
                error: function() {
                    showAlertPanel("删除失败：网络错误");
                }
            });
        }
    });


}(jQuery));
```

### index.js

```javascript
var express = require('express');
var router = express.Router();
var mysql = require('mysql');
var moment = require('moment');
moment.locale("zh-cn");

// 数据库连接信息
var pool = mysql.createPool({
	host: 'localhost',
	port: '3306',
	user: 'root',
	password: '',
	database: 'task_management',
	dateStrings: true
});

/* GET 获取任务列表 */
router.get('/', function(req, res, next) {
	pool.getConnection(function(err, connection) {
		// 查询 tasks 表，并按 id 倒序排列
		connection.query("SELECT * from tasks order by id desc", function(err, rows, fields) {
			if (err) throw err;
			res.render('index', {
				title: '任务管理系统',
				pageCode: 'index',
				tasks: rows
			});
		});
		connection.release();
	});
});

/* 获取单个任务 */
router.get('/task/get', function(req, res, next) {
	var id = req.query.id;
	pool.getConnection(function(err, connection) {
		connection.query("SELECT * from tasks where id = ?", [id], function(err, rows) { // 使用参数化查询
			if (err) throw err;
			res.json({ tasks: rows });
		});
		connection.release();
	});
});

/* 更新任务 */
router.post('/task/update', function(req, res, next) {
	var id = req.body.id;
	var startTime = req.body.startTime;
	var endTime = req.body.endTime;

    // 输入校验
    if (!moment(startTime, "YYYY-MM-DD HH:mm:ss").isValid()) {
        return res.json({ flg: false, err: "开始时间格式错误" });
    }
    if (!moment(endTime, "YYYY-MM-DD HH:mm:ss").isValid()) {
        return res.json({ flg: false, err: "结束时间格式错误" });
    }

	pool.getConnection(function(err, connection) {
		connection.query("UPDATE tasks SET startTime = ?, endTime = ? WHERE id = ?", [startTime, endTime, id], function(err, result) { // 使用参数化查询
			if (err) {
				res.json({ flg: false, err: err });
			} else {
				res.json({ flg: true });
			}
		});
		connection.release();
	});
});


/* 删除任务 */
router.post('/task/delete', function(req, res, next) {
	var id = req.body.id;
	pool.getConnection(function(err, connection) {
		connection.query("DELETE FROM tasks WHERE id = ?", [id], function(err, result) { // 使用参数化查询
			if (err) {
				res.json({ flg: false, err: err });
			} else {
				res.json({ flg: true });
			}
		});
		connection.release();
	});
});


module.exports = router;
```

## PM2

PM2是node进程管理工具，可以利用它来简化很多node应用管理的繁琐任务，如性能监控、自动重启、负载均衡等，而且使用非常简单。

```sh
sudo npm install pm2@latest -g
```

### 用法

- 最简单的启用一个应用:  `pm2 start app.js` 
- 停止：`pm2 stop app_name|app_id` 
- 删除：`pm2 delete app_name|app_id` 
- 重启：`pm2 restart app_name|app_id` 
- 停止所有：`pm2 stop all` 
- 查看所有的进程：`pm2 list` 
- 查看所有的进程状态：`pm2 status` 
- 查看某一个进程的信息：`pm2 describe app_name|app_id` 

### 参数说明

-  `--watch`：监听应用目录源码的变化，一旦发生变化，自动重启。如果要精确监听、不见听的目录，最好通过配置文件
-  `-i --instances`：启用多少个实例，可用于负载均衡。如果`-i 0`或者`-i max`，则根据当前机器核数确定实例数目，可以弥补node.js缺陷
-  `--ignore-watch`：排除监听的目录/文件，可以是特定的文件名，也可以是正则。比如`--ignore-watch="test node_modules "some scripts"` 
-  `-n --name`：应用的名称。查看应用信息的时候可以用到
-  `-o --output <path>`：标准输出日志文件的路径，有默认路径
-  `-e --error <path>`：错误输出日志文件的路径，有默认路径
-  `--interpreter <interpreter>`：the interpreter pm2 should use for executing app (bash, python...)。比如你用的coffee script来编写应用

### 完整参数命令

```sh
pm2 start ./bin/www -i max --watch
```

## ESLint 

ESLint 是一个代码规范和错误检查工具

```json
{
  "name": "expressjs",
  "version": "0.0.0",
  "private": true,
  "scripts": {
    "start": "node ./bin/www"
  },
  "dependencies": {
    "cookie-parser": "~1.4.3",
    "debug": "~2.6.9",
    "ejs": "~2.5.7",
    "express": "~4.16.0",
    "http-errors": "~1.6.2",
    "lionsoul-ip2region": "0.0.1",
    "mongodb": "^3.1.13",
    "morgan": "~1.9.0"
  },
  "devDependencies": {
    "babel-core": "^6.22.1",
    "babel-eslint": "^7.1.1",
    "eslint": "^3.19.0",
    "eslint-config-standard": "^10.2.1",
    "eslint-friendly-formatter": "^3.0.0",
    "eslint-loader": "^1.7.1",
    "eslint-plugin-html": "^3.0.0",
    "eslint-plugin-import": "^2.7.0",
    "eslint-plugin-node": "^5.2.0",
    "eslint-plugin-promise": "^3.4.0",
    "eslint-plugin-standard": "^3.0.1"
  }
}
```

```sh
eslint --init
```

.eslintrc.js

```javascript
// https://eslint.org/docs/user-guide/configuring

module.exports = {
  root: true,
  parser: 'babel-eslint',
  parserOptions: {
    sourceType: 'module'
  },
  env: {
    browser: true,
  },
  // https://github.com/standard/standard/blob/master/docs/RULES-en.md
  extends: 'standard',
  // required to lint *.vue files
  plugins: [
    'html'
  ],
  // add your custom rules here
  'rules': {
    // allow paren-less arrow functions
    'arrow-parens': 0,
    // allow async-await
    'generator-star-spacing': 0,
    // allow debugger during development
    'no-debugger': process.env.NODE_ENV === 'production' ? 2 : 0
  }
}
```

## 使用Express的项目

Taipower核电站疏散信息平台

![Taipower核电站疏散信息平台](Express.assets/Taipower.jpg)

## AI实战

### 根据界面截图生成RESTful API

![image-20250107212905616](Express.assets/image-20250107212905616.png)

```
我这里提供了一个待办事项的界面，请用express开发为该界面服务的RESTful API，给出express的源码
```

```javascript
const express = require('express');
const app = express();
const port = 3000; // 端口号，可以根据需要修改

// 使用 JSON 中间件解析请求体
app.use(express.json());

// 模拟数据存储，实际应用中应该使用数据库
let todos = [
  { id: 1, text: '学习 Express', completed: false },
  { id: 2, text: '完成项目', completed: true },
];

let nextId = 3; // 用于生成新的 todo id

// 获取所有待办事项
app.get('/todos', (req, res) => {
  res.json(todos);
});

// 获取单个待办事项
app.get('/todos/:id', (req, res) => {
  const todo = todos.find(todo => todo.id === parseInt(req.params.id));
  if (!todo) {
    return res.status(404).json({ message: '待办事项不存在' });
  }
  res.json(todo);
});

// 创建新的待办事项
app.post('/todos', (req, res) => {
  const { text } = req.body;
  if (!text) {
    return res.status(400).json({ message: '缺少 text 字段' });
  }

  const newTodo = {
    id: nextId++,
    text,
    completed: false,
  };
  todos.push(newTodo);
  res.status(201).json(newTodo);
});

// 更新待办事项
app.put('/todos/:id', (req, res) => {
  const todo = todos.find(todo => todo.id === parseInt(req.params.id));
  if (!todo) {
    return res.status(404).json({ message: '待办事项不存在' });
  }

  const { text, completed } = req.body;
  if (text) {
    todo.text = text;
  }
  if (typeof completed === 'boolean') {
    todo.completed = completed;
  }

  res.json(todo);
});


// 删除待办事项
app.delete('/todos/:id', (req, res) => {
  const index = todos.findIndex(todo => todo.id === parseInt(req.params.id));
  if (index === -1) {
    return res.status(404).json({ message: '待办事项不存在' });
  }

  todos.splice(index, 1);
  res.status(204).send(); // 204 No Content
});

// 启动服务器
app.listen(port, () => {
  console.log(`服务器运行在 http://localhost:${port}`);
});

```

**代码解释和使用方法：**

1. **依赖：** 需要安装 `express`： `npm install express`

2. **数据存储：**  代码中使用 `todos` 数组模拟数据存储。在实际应用中，应该使用数据库（例如 MongoDB、MySQL 等）。

3. **路由：**
    * `GET /todos`: 获取所有待办事项。
    * `GET /todos/:id`: 获取指定 ID 的待办事项。
    * `POST /todos`: 创建新的待办事项。请求体中需要包含 `text` 字段。
    * `PUT /todos/:id`: 更新指定 ID 的待办事项。请求体中可以包含 `text` 和 `completed` 字段。
    * `DELETE /todos/:id`: 删除指定 ID 的待办事项。

4. **错误处理：**  代码中包含了简单的错误处理，例如当待办事项不存在时返回 404 错误。

5. **启动服务器：**  运行 `node <文件名>.js` 启动服务器。

**前端如何使用 API：**

前端可以使用 `fetch` 或 `axios` 等库发送 HTTP 请求到这些 API 接口。例如，使用 `axios` 获取所有待办事项：

```javascript
axios.get('/todos')
  .then(response => {
    console.log(response.data); // 获取到的待办事项数据
  })
  .catch(error => {
    console.error(error);
  });
```


**进一步改进：**

* **数据库集成：**  使用数据库代替数组存储数据。
* **更完善的错误处理：**  处理各种可能的错误情况。
* **数据验证：**  对请求数据进行验证，确保数据的有效性。
* **身份验证和授权：**  如果需要，添加身份验证和授权机制。


这个示例代码提供了一个基本的 RESTful API 框架，您可以根据您的具体需求进行修改和扩展。

### 给出测试命令

```sh
给一个curl测试命令
```

以下是一些 curl 命令示例，用于测试上面提供的 Express API：

**1. 获取所有待办事项 (GET /todos):**

```bash
curl http://localhost:3000/todos
```

**2. 获取指定 ID 的待办事项 (GET /todos/:id):**  (例如，获取 ID 为 1 的待办事项)

```bash
curl http://localhost:3000/todos/1
```

**3. 创建新的待办事项 (POST /todos):**

```bash
curl -X POST -H "Content-Type: application/json" -d '{"text": "新待办事项"}' http://localhost:3000/todos
```

**4. 更新待办事项 (PUT /todos/:id):** (例如，更新 ID 为 2 的待办事项)

```bash
curl -X PUT -H "Content-Type: application/json" -d '{"text": "更新后的待办事项", "completed": true}' http://localhost:3000/todos/2
```

**5. 删除待办事项 (DELETE /todos/:id):** (例如，删除 ID 为 1 的待办事项)

```bash
curl -X DELETE http://localhost:3000/todos/1
```

**说明：**

*  `-X`: 指定 HTTP 方法 (GET, POST, PUT, DELETE 等)。
*  `-H "Content-Type: application/json"`:  对于 POST 和 PUT 请求，设置 Content-Type 为 application/json，告诉服务器请求体是 JSON 格式。
*  `-d`:  指定请求体数据。


**运行 curl 命令之前，请确保：**

1. 你的 Express 服务器已经在运行 (使用 `node <文件名>.js` 启动)。
2. 将 `localhost:3000` 替换为你服务器实际的地址和端口。


这些 curl 命令可以帮助你测试 API 的不同功能。 你可以根据需要修改这些命令，例如更改请求体数据或待办事项 ID。  建议使用 Postman 或 Insomnia 等 API 测试工具，它们提供更方便的界面和功能来测试 API。

### 使用SQLite存储

```
使用SQLite存储
```

```javascript
const express = require('express');
const app = express();
const port = 3000;
const sqlite3 = require('sqlite3').verbose();

// 创建或连接到 SQLite 数据库
const db = new sqlite3.Database('todos.db');

// 创建 todos 表（如果不存在）
db.run(`
  CREATE TABLE IF NOT EXISTS todos (
    id INTEGER PRIMARY KEY AUTOINCREMENT,
    text TEXT NOT NULL,
    completed INTEGER NOT NULL DEFAULT 0 -- 0: 未完成, 1: 完成
  )
`);

app.use(express.json());


// 获取所有待办事项
app.get('/todos', (req, res) => {
  db.all('SELECT * FROM todos', (err, rows) => {
    if (err) {
      return res.status(500).json({ message: '数据库错误' });
    }
    res.json(rows);
  });
});

// 获取单个待办事项
app.get('/todos/:id', (req, res) => {
  const id = req.params.id;
  db.get('SELECT * FROM todos WHERE id = ?', [id], (err, row) => {
    if (err) {
      return res.status(500).json({ message: '数据库错误' });
    }
    if (!row) {
      return res.status(404).json({ message: '待办事项不存在' });
    }
    res.json(row);
  });
});

// 创建新的待办事项
app.post('/todos', (req, res) => {
  const { text } = req.body;
  if (!text) {
    return res.status(400).json({ message: '缺少 text 字段' });
  }

  db.run('INSERT INTO todos (text) VALUES (?)', [text], function(err) {
    if (err) {
      return res.status(500).json({ message: '数据库错误' });
    }
    res.status(201).json({ id: this.lastID, text, completed: false }); // 返回新创建的待办事项
  });
});

// 更新待办事项
app.put('/todos/:id', (req, res) => {
  const id = req.params.id;
  const { text, completed } = req.body;

  db.run('UPDATE todos SET text = ?, completed = ? WHERE id = ?', [text, completed ? 1 : 0, id], function(err) {
    if (err) {
      return res.status(500).json({ message: '数据库错误' });
    }
    if (this.changes === 0) {
      return res.status(404).json({ message: '待办事项不存在' });
    }
    res.json({ id, text, completed }); // 返回更新后的待办事项
  });
});

// 删除待办事项
app.delete('/todos/:id', (req, res) => {
  const id = req.params.id;
  db.run('DELETE FROM todos WHERE id = ?', [id], function(err) {
    if (err) {
      return res.status(500).json({ message: '数据库错误' });
    }
    if (this.changes === 0) {
      return res.status(404).json({ message: '待办事项不存在' });
    }
    res.status(204).send();
  });
});


// 启动服务器
app.listen(port, () => {
  console.log(`服务器运行在 http://localhost:${port}`);
});
```


**主要变化：**

* **数据库连接：** 使用 `sqlite3` 模块连接到名为 `todos.db` 的 SQLite 数据库。如果数据库不存在，则会自动创建。
* **表创建：**  使用 `db.run()` 创建 `todos` 表，包含 `id`、`text` 和 `completed` 字段。 `completed` 字段使用整数类型，0 表示未完成，1 表示完成。
* **数据库操作：**  使用 `db.all()`、`db.get()`、`db.run()` 等方法进行数据库操作。
* **错误处理：**  添加了数据库错误处理。
* **返回值：**  修改了部分接口的返回值，使其更符合 RESTful API 的规范。


**使用方法：**

1. 安装 `sqlite3` 和 `express`:  `npm install sqlite3 express`
2. 运行代码: `node <文件名>.js`


现在，待办事项数据将存储在 `todos.db` 数据库文件中。 你可以使用之前的 curl 命令或其他 API 测试工具来测试 API。


**改进建议：**

* **使用 ORM：** 考虑使用 Sequelize 或 TypeORM 等 ORM 库来简化数据库操作。
* **输入验证：**  添加更严格的输入验证，防止 SQL 注入等安全问题。
* **事务处理：**  对于涉及多个数据库操作的接口，使用事务来确保数据一致性。


这个改进后的代码使用 SQLite 数据库来存储待办事项数据，使其更接近实际应用场景。

### 生成swagger的接口文档

```
生成swagger的接口文档
```

```json
{
  "openapi": "3.0.0",
  "info": {
    "title": "待办事项 API",
    "version": "1.0.0",
    "description": "用于管理待办事项的 RESTful API"
  },
  "paths": {
    "/todos": {
      "get": {
        "summary": "获取所有待办事项",
        "responses": {
          "200": {
            "description": "返回所有待办事项",
            "content": {
              "application/json": {
                "schema": {
                  "type": "array",
                  "items": {
                    "$ref": "#/components/schemas/Todo"
                  }
                }
              }
            }
          }
        }
      },
      "post": {
        "summary": "创建新的待办事项",
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "$ref": "#/components/schemas/NewTodo"
              }
            }
          }
        },
        "responses": {
          "201": {
            "description": "成功创建待办事项",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/Todo"
                }
              }
            }
          }
        }
      }
    },
    "/todos/{id}": {
      "get": {
        "summary": "获取单个待办事项",
        "parameters": [
          {
            "in": "path",
            "name": "id",
            "schema": {
              "type": "integer"
            },
            "required": true,
            "description": "待办事项 ID"
          }
        ],
        "responses": {
          "200": {
            "description": "返回单个待办事项",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/Todo"
                }
              }
            }
          }
        }
      },
      "put": {
        "summary": "更新待办事项",
        "parameters": [
          {
            "$ref": "#/components/parameters/idParam"
          }
        ],
        "requestBody": {
          "required": true,
          "content": {
            "application/json": {
              "schema": {
                "$ref": "#/components/schemas/UpdateTodo"
              }
            }
          }
        },
        "responses": {
          "200": {
            "description": "成功更新待办事项",
            "content": {
              "application/json": {
                "schema": {
                  "$ref": "#/components/schemas/Todo"
                }
              }
            }
          }
        }
      },
      "delete": {
        "summary": "删除待办事项",
        "parameters": [
          {
            "$ref": "#/components/parameters/idParam"
          }
        ],
        "responses": {
          "204": {
            "description": "成功删除待办事项"
          }
        }
      }
    }
  },
  "components": {
    "schemas": {
      "Todo": {
        "type": "object",
        "properties": {
          "id": {
            "type": "integer",
            "description": "待办事项 ID"
          },
          "text": {
            "type": "string",
            "description": "待办事项内容"
          },
          "completed": {
            "type": "boolean",
            "description": "是否完成"
          }
        }
      },
      "NewTodo": {
        "type": "object",
        "properties": {
          "text": {
            "type": "string",
            "description": "待办事项内容"
          }
        },
        "required": [
          "text"
        ]
      },
      "UpdateTodo": {
        "type": "object",
        "properties": {
          "text": {
            "type": "string",
            "description": "待办事项内容"
          },
          "completed": {
            "type": "boolean",
            "description": "是否完成"
          }
        }
      }
    },
    "parameters": {
      "idParam": {
        "in": "path",
        "name": "id",
        "schema": {
          "type": "integer"
        },
        "required": true,
        "description": "待办事项 ID"
      }
    }
  }
}
```


这个 JSON 文档描述了待办事项 API 的各个接口，包括请求方法、路径、参数、请求体、响应状态码和响应数据结构。 你可以将这个 JSON 文件导入到 Swagger UI 或其他 API 文档工具中，以便查看和测试 API。


**一些关键改进：**

* **添加了 `UpdateTodo` schema:** 用于 PUT 请求，允许更新 `text` 和 `completed` 字段。
* **使用 `$ref` 引用参数定义:**  避免重复定义参数，使文档更简洁。
* **更清晰的描述:**  对各个字段和接口提供了更详细的描述。


这个 JSON 文档可以直接用于 Swagger UI 或其他 API 文档工具，无需使用 `swagger-jsdoc` 动态生成。  这对于静态文档生成或在不支持 `swagger-jsdoc` 的环境中使用 Swagger 非常有用。
