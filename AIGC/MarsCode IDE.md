# MarsCode IDE：云端 AI IDE 平台

## MarsCode IDE简介

[MarsCode IDE](https://www.marscode.cn/dashboard) 是一个云端 AI IDE 平台。通过内置的 AI 编程助手，开箱即用的开发环境，你可以更专注于各类项目开发。​

> 简而言之MarsCode IDE就是一个Linux容器 + VSCode + MarsCode

### 工作台

它利用了VSCode构筑云端 IDE，所以你只需要一台可以访问浏览器的计算机、笔记本或者平板电脑便可以打开豆包 MarsCode 完成开发工作，而编辑体验和VSCode基本一致，但是插件支持比较有限

> 如下图，只有有台手机就能运行，调试（当然最好还是配套蓝牙键盘和鼠标），否则你会很痛苦
>
> ![2604535d7a59a4fc78d46d1f1a5b98a](MarsCode IDE.assets/2604535d7a59a4fc78d46d1f1a5b98a.jpg)

![image-20241011101013575](MarsCode IDE.assets/image-20241011101013575.png)

支持从模版创建项目

![image-20241011105434521](MarsCode IDE.assets/image-20241011105434521.png)

支持导入git仓库

![image-20241011105516617](MarsCode IDE.assets/image-20241011105516617.png)

### 内置MarsCode AI

内置了MarsCode AI 助手，提供代码自动补全与生成、问题修复、代码优化等能力，帮助你更高效地完成开发任务。试用了一下，和主流的竞品水平相当。

![image-20241011101329644](MarsCode IDE.assets/image-20241011101329644.png)

### 终端交互

由于每个项目都开辟了一个容器，根据你选择的编程语言，内置了一些开发环境，比如本项目，从GITHUB中导入后，自动部署了Node.js和pnpm。你也可以使用终端与该Linux虚拟环境交互，利用它的云端资源。如下图，终端中支持各种命令

![image-20241011101458320](MarsCode IDE.assets/image-20241011101458320.png)

试了一下可以安装软件，不需要太多资源、权限的软件可以正常运行，其它的比如mariadb之类运行起来比较麻烦，没有仔细研究

```sh
sudo apt-get update
sudo apt install nginx
/usr/sbin/nginx
```

编译安装软件也都可以，比如在终端中编译新版本的sqlite

```sh
wget https://www.sqlite.org/2024/sqlite-autoconf-3460100.tar.gz
tar -xvf sqlite-autoconf-3460100.tar.gz
cd sqlite-autoconf-3460100.tar.gz
./configure --enable-all
make
sudo make install
./sqlite3 --version                                            
3.46.1 2024-08-13 09:16:08 c9c2ab54ba1f5f46360f1b4f35d849cd3f080e6fc2b6c60e91b16c63f69a1e33 (64-bit)
```

### 网络服务

通过MarsCode IDE提供URL可以直接访问项目，运行成功后，可以在网络服务中找到URL访问项目

![image-20241011104555601](MarsCode IDE.assets/image-20241011104555601.png)

## 项目实践

导入一个前后端分离项目

### 后端

后端使用spring-boot，Maven这些环境都默认给配好了，会根据pom.xml自动下载

![image-20241011105650548](MarsCode IDE.assets/image-20241011105650548.png)

这里我用了内存数据库，`application.properties`配置如下

```properties
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.driverClassName=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=
spring.h2.console.enabled=true
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
```

运行项目后8080端口被绑定到网络服务，可以通过curl测试

首先创建用户

```sh
curl --location --request POST 'https://5gw4v7eo-fra5uj7x-pamustz8w3v4.vcc3.mcprev.cn//accounts' \
--header 'Content-Type: application/json' \
--data-raw '{
  "name": "Craig Walls",
  "email": "test@demo.com",
  "password": "9781617292545"
}'
```

返回

```json
{
    "id": 1,
    "name": "Craig Walls",
    "email": "test@demo.com",
    "password": "9781617292545"
}
```

使用该用户登录，获得token

```sh
curl --location --request GET 'https://5gw4v7eo-fra5uj7x-pamustz8w3v4.vcc3.mcprev.cn/auth?loginId=Craig%20Walls&loginPassword=9781617292545'
```

返回

```json
{
    "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhdWQiOiIwIiwiZXhwIjoxNzI4NjE4NDQyLCJ1c2VyTmFtZSI6IkNyYWlnIFdhbGxzIiwiaWF0IjoxNzI4NjE2NjQyfQ.t6y7iFLMOWNhGmmjRA-EZgyC76cf7sWe67m_jBS2DBc",
    "status": 200,
    "message": ""
}
```

### 前端

使用模版新建一个VUE3的项目，直接使用AI写代码

```sh
根据以下命令
curl --location --request GET 'https://5gw4v7eo-fra5uj7x-pamustz8w3v4.vcc3.mcprev.cn/auth?loginId=Craig%20Walls&loginPassword=9781617292545'
写一个简单的用户登陆界面，使用fetch调用该接口
正常的返回值为
{
    "token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhdWQiOiIwIiwiZXhwIjoxNzI4NjE4NDQyLCJ1c2VyTmFtZSI6IkNyYWlnIFdhbGxzIiwiaWF0IjoxNzI4NjE2NjQyfQ.t6y7iFLMOWNhGmmjRA-EZgyC76cf7sWe67m_jBS2DBc",
    "status": 200,
    "message": ""
}
保存token并提示用户
```

![image-20241011113123830](MarsCode IDE.assets/image-20241011113123830.png)

返回的代码有一点小bug，手动改了一下运行，可以直接出现web预览，也可以从web预览中拷贝URL到浏览器进行调试。

![image-20241011113249808](MarsCode IDE.assets/image-20241011113249808.png)

整个前后端分离项目正常运行