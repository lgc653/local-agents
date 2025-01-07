# Vue UI组件库

Vue 是一个轻巧、高性能、可组件化的MVVM库，API简洁明了，上手快。从Vue推出以来，得到众多Web开发者的认可。

在公司的Web前端项目开发中，多个项目采用基于Vue的UI组件框架开发，并投入正式使用。

开发团队在使用Vue.js框架和UI组件库以后，开发效率大大提高，自己写的代码也少了，很多界面效果组件已经封装好了。

在选择Vue UI组件库的过程中，通过GitHub上根据star数量、文档丰富程度、更新的频率以及维护等因素，也收集整理了一些优秀的Vue UI组件库。

## iView UI组件库
iView 是一套基于 Vue.js 的开源 UI 组件库，主要服务于 PC 界面的中后台产品。iView的组件还是比较齐全的，更新也很快，文档写得很详细。有公司团队维护，比较可靠的Vue UI组件框架。iView生态也做得很好，还有开源了一个iView Admin，做后台非常方便。官网上介绍，iView已经应用在TalkingData、阿里巴巴、百度、腾讯、今日头条、京东、滴滴出行、美团、新浪、联想等大型公司的产品中。

iView官网：https://www.iviewui.com/

### 安装

使用 npm

```sh
$ npm install view-design --save
```

或使用 `<script>` 全局引用

```html
<script type="text/javascript" src="iview.min.js"></script>
```

### 示例

通过 CDN 可以快速使用 View UI 写出一个示例：

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>ViewUI example</title>
    <link rel="stylesheet" type="text/css" href="http://unpkg.com/view-design/dist/styles/iview.css">
    <script type="text/javascript" src="http://vuejs.org/js/vue.min.js"></script>
    <script type="text/javascript" src="http://unpkg.com/view-design/dist/iview.min.js"></script>
</head>
<body>
<div id="app">
    <i-button @click="show">Click me!</i-button>
    <Modal v-model="visible" title="Welcome">Welcome to ViewUI</Modal>
</div>
<script>
    new Vue({
        el: '#app',
        data: {
            visible: false
        },
        methods: {
            show: function () {
                this.visible = true;
            }
        }
    })
  </script>
</body>
</html>
```

### 引入 ViewUI

一般在 webpack 入口页面 `main.js` 中如下配置：

```javascript
import Vue from 'vue';
import VueRouter from 'vue-router';
import App from 'components/app.vue';
import Routers from './router.js';
import ViewUI from 'view-design';
import 'view-design/dist/styles/iview.css';

Vue.use(VueRouter);
Vue.use(ViewUI);

// The routing configuration
const RouterConfig = {
    routes: Routers
};
const router = new VueRouter(RouterConfig);

new Vue({
    el: '#app',
    router: router,
    render: h => h(App)
});
```

## Element UI组件库

Element，一套为开发者、设计师和产品经理准备的基于 Vue 2.0 的桌面端组件库。Element是饿了么前端开源维护的Vue UI组件库，更新频率还是很高的，基本一周到半个月都会发布一个新版本。组件齐全，基本涵盖后台所需的所有组件，文档讲解详细，例子也很丰富。没有实际使用过，网上的Element教程和文章比较多。Element应该是一个质量比较高的Vue UI组件库。

Element官网：https://element.eleme.cn/#/zh-CN

### 安装

#### npm 安装

推荐使用 npm 的方式安装，它能更好地和 [webpack](https://webpack.js.org/) 打包工具配合使用。

```shell
npm i element-ui -S
```

#### CDN

目前可以通过 [unpkg.com/element-ui](https://unpkg.com/element-ui/) 获取到最新版本的资源，在页面上引入 js 和 css 文件即可开始使用。

```html
<!-- 引入样式 -->
<link rel="stylesheet" href="https://unpkg.com/element-ui/lib/theme-chalk/index.css">
<!-- 引入组件库 -->
<script src="https://unpkg.com/element-ui/lib/index.js"></script>
```

### 示例

通过 CDN 可以快速使用 Element UI写出一个示例：

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <!-- import CSS -->
  <link rel="stylesheet" href="https://unpkg.com/element-ui/lib/theme-chalk/index.css">
</head>
<body>
  <div id="app">
    <el-button @click="visible = true">Button</el-button>
    <el-dialog :visible.sync="visible" title="Hello world">
      <p>Try Element</p>
    </el-dialog>
  </div>
</body>
  <!-- import Vue before Element -->
  <script src="https://unpkg.com/vue/dist/vue.js"></script>
  <!-- import JavaScript -->
  <script src="https://unpkg.com/element-ui/lib/index.js"></script>
  <script>
    new Vue({
      el: '#app',
      data: function() {
        return { visible: false }
      }
    })
  </script>
</html>
```

### 引入 Element

你可以引入整个 Element，或是根据需要仅引入部分组件。我们先介绍如何引入完整的 Element。

在 main.js 中写入以下内容：

```javascript
import Vue from 'vue';
import ElementUI from 'element-ui';
import 'element-ui/lib/theme-chalk/index.css';
import App from './App.vue';

Vue.use(ElementUI);

new Vue({
  el: '#app',
  render: h => h(App)
});
```

以上代码便完成了 Element 的引入。需要注意的是，样式文件需要单独引入。

## Ant Design Vue UI组件库

Ant Design Vue是 Ant Design 3.X 的 Vue 实现，开发和服务于企业级后台产品。在GitHub上可以找到几个Ant Design的Vue组件。不过相比较而言，Ant Design Vue更胜一筹。Ant Design Vue共享Ant Design of React设计工具体系，实现了所有Ant Design of React的组件，支持现代浏览器和 IE9 及以上（需要 polyfills）。可以让熟悉Ant Design的在使用Vue时，很容易的上手。

Ant Design Vue官网：https://vuecomponent.github.io/ant-design-vue/docs/vue/introduce-cn/

### 安装 

#### 使用 npm 或 yarn 安装 
我们推荐使用 npm 或 yarn 的方式进行开发，不仅可在开发环境轻松调试，也可放心地在生产环境打包部署使用，享受整个生态圈和工具链带来的诸多好处。

```sh
$ npm install ant-design-vue --save
$ yarn add ant-design-vue
```

如果你的网络环境不佳，推荐使用 cnpm。

#### 浏览器引入 

在浏览器中使用 `script` 和 `link` 标签直接引入文件，并使用全局变量 `antd`。

开发团队在 npm 发布包内的 `ant-design-vue/dist` 目录下提供了 `antd.js` `antd.css` 以及 `antd.min.js` `antd.min.css`。你也可以通过 [jsdelivr](https://www.jsdelivr.com/package/npm/ant-design-vue) 或 [UNPKG](https://unpkg.com/ant-design-vue/dist/) 进行下载。

### 示例

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>Document</title>
        <script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.6.10/vue.js"></script>
        <script src="https://cdn.jsdelivr.net/npm/ant-design-vue@1.7.4/dist/antd.min.js"></script>
        <script src="https://cdnjs.cloudflare.com/ajax/libs/moment.js/2.24.0/moment.js"></script>
        <link
            href="https://cdn.jsdelivr.net/npm/ant-design-vue@1.7.4/dist/antd.min.css"
            rel="stylesheet"
            type="text/css"
        />
        <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.4.1/jquery.js"></script>
    </head>

    <body>
        <div id="root">
            <template>
                <a-cascader :options="options" :default-value="['zhejiang', 'hangzhou', 'xihu']" style="width: 100%;">
                    <template slot="displayRender" slot-scope="{ labels, selectedOptions }">
                        <span v-for="(label, index) in labels" :key="selectedOptions[index].value">
                            <span v-if="index === labels.length - 1">
                                {{ label }} (<a @click="e => handleAreaClick(e, label, selectedOptions[index])"
                                    >{{ selectedOptions[index].code }}</a
                                >)
                            </span>
                            <span v-else @click="onChange"> {{ label }} / </span>
                        </span>
                    </template>
                </a-cascader>
            </template>
        </div>

        <script>
            var vue = new Vue({
                el: '#root',
                data() {
                    return {
                        options: [
                            {
                                value: 'zhejiang',
                                label: 'Zhejiang',
                                children: [
                                    {
                                        value: 'hangzhou',
                                        label: 'Hangzhou',
                                        children: [
                                            {
                                                value: 'xihu',
                                                label: 'West Lake',
                                                code: 752100
                                            }
                                        ]
                                    }
                                ]
                            },
                            {
                                value: 'jiangsu',
                                label: 'Jiangsu',
                                children: [
                                    {
                                        value: 'nanjing',
                                        label: 'Nanjing',
                                        children: [
                                            {
                                                value: 'zhonghuamen',
                                                label: 'Zhong Hua Men',
                                                code: 453400
                                            }
                                        ]
                                    }
                                ]
                            }
                        ]
                    }
                },
                methods: {
                    onChange(value) {
                        console.log(value)
                    },
                    handleAreaClick(e, label, option) {
                        e.stopPropagation()
                        console.log('clicked', label, option)
                    }
                }
            })
        </script>
    </body>
</html>
```

### 引入Ant Design Vue

```jsx
import Vue from 'vue';
import { DatePicker } from 'ant-design-vue';
Vue.use(DatePicker);
```

引入样式：

```jsx
import 'ant-design-vue/dist/antd.css'; // or 'ant-design-vue/dist/antd.less'
```

## Mint UI

Mint UI 由饿了么前端团队推出的 Mint UI 是一个基于 Vue.js 的移动端组件库

Mint UI 包含丰富的 CSS 和 JS 组件，能够满足日常的移动端开发需要。通过它，可以快速构建出风格统一的页面，提升开发效率。

真正意义上的按需加载组件。可以只加载声明过的组件及其样式文件，无需再纠结文件体积过大。

考虑到移动端的性能门槛，Mint UI 采用 CSS3 处理各种动效，避免浏览器进行不必要的重绘和重排，从而使用户获得流畅顺滑的体验。

依托 Vue.js 高效的组件化方案，Mint UI 做到了轻量化。即使全部引入，压缩后的文件体积也仅有 ~30kb (JS + CSS) gzip。

Mint UI官网：http://mint-ui.github.io/#!/zh-cn

### 安装

#### npm 安装

推荐使用 npm 的方式安装，它能更好地和 [webpack](https://webpack.js.org/) 打包工具配合使用。

```shell
npm i mint-ui -S
```

#### CDN

目前可以通过 [unpkg.com/mint-ui](https://unpkg.com/mint-ui/) 获取到最新版本的资源，在页面上引入 js 和 css 文件即可开始使用。

```html
<!-- 引入样式 -->
<link rel="stylesheet" href="https://unpkg.com/mint-ui/lib/style.css">
<!-- 引入组件库 -->
<script src="https://unpkg.com/mint-ui/lib/index.js"></script>
```

### 示例

通过 CDN 的方式我们可以很容易地使用 Mint UI 写出一个 Hello world 页面。

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <!-- 引入样式 -->
  <link rel="stylesheet" href="https://unpkg.com/mint-ui/lib/style.css">
</head>
<body>
  <div id="app">
    <mt-button @click.native="handleClick">按钮</mt-button>
  </div>
</body>
  <!-- 先引入 Vue -->
  <script src="https://unpkg.com/vue/dist/vue.js"></script>
  <!-- 引入组件库 -->
  <script src="https://unpkg.com/mint-ui/lib/index.js"></script>
  <script>
    new Vue({
      el: '#app',
      methods: {
        handleClick: function() {
          this.$toast('Hello world!')
        }
      }
    })
  </script>
</html>
```

### 引入 Mint UI

你可以引入整个 Mint UI，或是根据需要仅引入部分组件。我们先介绍如何引入完整的 Mint UI。

在 main.js 中写入以下内容：

```javascript
import Vue from 'vue'
import MintUI from 'mint-ui'
import 'mint-ui/lib/style.css'
import App from './App.vue'

Vue.use(MintUI)

new Vue({
  el: '#app',
  components: { App }
})
```

以上代码便完成了 Mint UI 的引入。需要注意的是，样式文件需要单独引入。

## VUX - Vue 移动端 UI 组件库

Vux（读音 [v'ju:z]，同views）是基于 WeUI 和 Vue(2.x) 开发的移动端UI组件库，主要服务于微信页面。 

基于webpack+vue-loader+vux可以快速开发移动端页面，配合vux-loader方便你在WeUI的基础上定制需要的样式。 

vux-loader保证了组件按需使用，因此不用担心最终打包了整个vux的组件库代码。  

VUX官网：https://vux.li/

### 安装

直接安装或者更新：

```sh
npm install vux --save
```

或者使用 `yarn`

```sh
yarn add vux // 安装
yarn upgrade vux // 更新
```

### vux2 模板

```sh
npm install vue-cli -g # 如果还没安装
vue init airyland/vux2 projectPath

cd projectPath
npm install --registry=https://registry.npm.taobao.org # 或者 cnpm install 或者  yarn
npm run dev #  或者  yarn dev
```

### 示例

#### .vue文件中调用组件

```html
<template>
  <div>
    <group>
      <cell title="title" value="value"></cell>
    </group>
  </div>
</template>

<script>
import { Group, Cell } from 'vux'

export default {
  components: {
    Group,
    Cell
  }
}
</script>
```

#### main.js中调用plugin

```javascript
import { AlertPlugin, ToastPlugin } from 'vux'

Vue.use(AlertPlugin)
Vue.use(ToastPlugin)

// 详细使用请参考对应组件文档
```

## nutui

NutUI 是京东风格的移动端组件库，使用 Vue 语言来编写可以在 H5，小程序平台上的应用，帮助研发人员提升开发效率，改善开发体验。

官网：https://nutui.jd.com/

### 特性

- 🚀 70+ 高质量组件，覆盖移动端主流场景
- 💪 支持一套代码同时开发多端小程序+H5
- 📖 基于京东APP 10.0 视觉规范
- 🍭 支持按需引用
- 📖 详尽的文档和示例
- 💪 支持 TypeScript
- 💪 支持服务端渲染（测试阶段）
- 🍭 支持定制主题，内置 700+ 个主题变量
- 🌍 国际化支持
- 🍭 单元测试覆盖率超过 80%，保障稳定性
- 📖 提供 Sketch 设计资源

### 快速上手

#### NPM 安装

```bash
# Vue2 项目 需要参考 2.x 文档 https://nutui.jd.com/2x
npm i @nutui/nutui@2

# Vue3 H5 项目
npm i @nutui/nutui

# Taro + Vue3 多端小程序项目
npm i @nutui/nutui-taro
```

#### NPM 使用示例

```javascript
import { createApp } from "vue";
import App from "./App.vue";
// 注意：这种方式将会导入所有组件
import NutUI from "@nutui/nutui";
// 采用按需加载时  此全局css样式，需要删除
import "@nutui/nutui/dist/style.css";
createApp(App).use(NutUI).mount("#app");
```

### 示例

初始化项目

```sh
vue create nutui
cd nutui  
npm i eslint-plugin-html -D
npm i @nutui/nutui@2
npm i axios
# 可以用cnpm
npm i node-sass@5 -D
npm i sass-loader@10 -D
```

修改main.js

```javascript
import Vue from 'vue'
import App from './App.vue'
import NutUI from '@nutui/nutui'

// 采用按需加载时  此全局css样式，需要删除
import '@nutui/nutui/dist/nutui.scss'

Vue.config.productionTip = false
Vue.use(NutUI)

new Vue({
  render: h => h(App)
}).$mount('#app')
```

追加src\api\api.js

```javascript
import axios from 'axios'
import qs from 'qs'
import NutUI from '@nutui/nutui'
const { Toast } = NutUI

const api = {}
let apiHomeDomain = '//service.mohou.com'
if (process.env.NODE_ENV === 'development') {
  apiHomeDomain = 'http://localservice.mohou.com'
}

api.http = axios.create({
  timeout: 30000
})
api.loading = null

// 添加请求拦截器
api.http.interceptors.request.use(
  function(config) {
    api.loading = Toast.loading()
    const token = sessionStorage.getItem('mohou_token')
    const params = {
      mohou_token: token
    }
    if (token) {
      // 不加入非默认的header，否则会触发OPTIONS请求，token通过追加token参数的方式解决
      // config.headers['X-Access-Token'] = token
    }
    if (config.method === 'post' || config.method === 'put') {
      config.headers['Content-Type'] = 'application/x-www-form-urlencoded'
      if (token) {
        Object.assign(config.data, params)
      }
      config.data = qs.stringify(config.data)
    }
    if (config.method === 'get' || config.method === 'delete') {
      if (token) {
        if (config.url.indexOf('?') !== -1) {
          config.url = config.url + '&' + qs.stringify(params)
        } else {
          config.url = config.url + '?' + qs.stringify(params)
        }
      }
    }
    return config
  },
  function(error) {
    api.loading.hide()
    Toast.fail('请求超时')
    return Promise.reject(error)
  }
)

// 添加响应拦截器
api.http.interceptors.response.use(
  function(response) {
    api.loading.hide()
    if (response.status === 200) {
      console.log(response.data)
      if (response.data.code === 516) {
        Toast.fail('您的会话已过期，请重新登陆')
      } else if (response.data.code === 500 && !response.data.msg) {
        Toast.fail('系统错误')
      } else if (response.data.code !== 0) {
        if (!response.data.msg) {
          Toast.fail('系统错误')
        }
      }
      return response.data
    }
    return response
  },
  function(error) {
    api.loading.hide()
    Toast.fail('网络请求错误')
    return Promise.reject(error)
  }
)
api.apiHomeDomain = apiHomeDomain
export default api
```

修改\src\components\HelloWorld.vue

```vue
<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <nut-row>
      <nut-col :span="12">
        <div class="flex-content"><nut-button type="primary">主要按钮</nut-button></div>
      </nut-col>
      <nut-col :span="12">
        <div class="flex-content flex-content-light"><nut-button type="default">默认按钮</nut-button></div>
      </nut-col>
    </nut-row>
    <div
      v-for="mat in materials"
      :key="mat.id"
      class="card"
    >
      <div class="card-img">
        <div
          v-if="mat.is_active === 1"
          class="fire-button"
        >🔥</div>
        <img v-lazy="mat.new_img_path">
      </div>
      <div class="card-desc">
        <h3>{{ mat.name }}</h3>
        <p>{{ mat.price + mat.price_unit }}</p>
        <p>{{ mat.suit }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import Api from '@/api/api'
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      materials: []
    }
  },
  created() {
    sessionStorage.setItem('mohou_token', 'eyJpdiI6ImJvdDNvVjhxVlBcL21KTUtyMWVMc2t3PT0iLCJ2YWx1ZSI6Ikdvd3FoSlhKWnZ5RUR2MkJ5ckxpbEJ3MVZPZ3kxbHZoMWU3eGZwaExrd002U0dyTUlNc3Y1S1VPdVNmcGFGMUhNXC9pVno2UlI1SVoyT1liVzlESzZHdz09IiwibWFjIjoiNzMyZmY0NmEwZjcxZjQ2OThhNGZiY2JhNTk4NjNiMDE2OGVhOWI0NmRjYmE5MmNmZmM5YjAyNzE5OTU2ZjY5YSJ9')
  },
  mounted() {
    this.getPrintMaterials()
  },
  methods: {
    getPrintMaterials: async function () {
      try {
        const resp = await Api.http.get(Api.apiHomeDomain + '/mohou_outer/v11/print_material')
        if (resp.code === 0) {
          this.materials = resp.data
        }
      } catch (error) {
        console.log(error)
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.card-img {
  position: relative;
}
.card-img img {
  width: 90%;
  object-fit: cover;
}
.fire-button {
  background: #000;
  opacity: 0.7;
  color: #e0e0e0;
  font-size: 32px;
  line-height: 60px;
  text-align: center;
  right: 10px;
  top: 10px;
  width: 60px;
  height: 60px;
  display: inline-block;
  position: absolute;
  border-radius: 50%;
  border: 1px #e0e0e0 solid;
}
.card-desc {
  display: flex;
  flex-direction: column;
}
button {
  background-color: DodgerBlue;
  color: white;
  border-radius: 5px;
}
</style>
```

