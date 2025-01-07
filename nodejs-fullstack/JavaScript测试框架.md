# JavaScript测试框架

## 课程简介

* 测试框架概述
* Jest
  * 基础测试
  * 异步测试
  * Vue测试
* Mocha
  * 基础测试
  * Mocha的高级应用
* 推荐组合
  * 单元测试：Jest
  * 功能测试：Jest + puppeteer
  * 性能测试：puppeteer
  * 接口管理、测试：Apifox
  * Mock：Apifox


## GitHub上的JavaScript测试框架

5 个领先的解决方案保持了和 2017 年相同的排名。Jest 比竞争者们进步更快，开发者们喜欢 Fackbook 的全功能测试框架所带来的效用 —— 无论是在前端（它最初被打算用于测试 React 组件）还是后端使用，而且它是零配置的。

![GitHub上的JavaScript测试框架](JavaScript%E6%B5%8B%E8%AF%95%E6%A1%86%E6%9E%B6.assets/download-1547710407309.jpg)

## JEST

Jest是Facebook开源的一套JavaScript测试框架， 它集成了断言、JSDom、覆盖率报告等开发者所需要的所有测试工具。

这些项目都在使用 Jest：[Babel](https://babeljs.io/)、 [TypeScript](https://www.typescriptlang.org/)、 [Node](https://nodejs.org/)、 [React](https://reactjs.org/)、 [Angular](https://angular.io/)、 [Vue](https://vuejs.org/) 等等！

### JEST起步

#### 安装

```bash
# 项目中使用
yarn init -y
yarn add --dev jest
# 或者全局安装，随时随地使用
yarn global add jest
npm i jest -g
```

#### hello world

编写以下两个js文件，控制台输入命令`jest --no-cache --verbose`(全局安装)，或者`npx jest --no-cache --verbose`（项目依赖安装），jest会搜索项目下所有测试脚本并执行输出测试结果。

**hello.js**

```js
module.exports = function(){
    return "hello world";
}
```

 **hello.test.js**

```javascript
const hello = require('./hello');

it('should ', () => {
    expect(hello()).toBe('hello world');
});
```

虽然Jest是号称0配置，但是还是要有个空白的配置文件`jest.config.js`，否则会报错，当然你也可以对他进行详细配置

**jest.config.js**

```js
module.exports = {}
```

运行测试

```sh
cd d:\Dev\lessons\Node.js\examples\Jest\ && d: && jest --no-cache --verbose
```

![运行测试](JavaScript%E6%B5%8B%E8%AF%95%E6%A1%86%E6%9E%B6.assets/image-20211128110730280.png)

### 基础测试知识

#### 文件和目录命名规范

待测试文件: `hello.js` 测试脚本文件取名：`hello.test.js`or`hello.spec.js` 测试目录:`tests`or`__tests__`

#### 测试函数

```js
test("测试用列描述信息",()=>{

})
// or
it("测试用例描述信息",()=>{

})
```

#### 断言函数

> 测试即运行结果是否与我们预期结果一致 断言函数用来验证结果是否正确

```js
exspect(运行结果).toBe(期望的结果);
//常见断言方法
expect({a:1}).toBe({a:1})//判断两个对象是否相等
expect(1).not.toBe(2)//判断不等
expect({ a: 1, foo: { b: 2 } }).toEqual({ a: 1, foo: { b: 2 } })
expect(n).toBeNull(); //判断是否为null
expect(n).toBeUndefined(); //判断是否为undefined
expect(n).toBeDefined(); //判断结果与toBeUndefined相反
expect(n).toBeTruthy(); //判断结果为true
expect(n).toBeFalsy(); //判断结果为false
expect(value).toBeGreaterThan(3); //大于3
expect(value).toBeGreaterThanOrEqual(3.5); //大于等于3.5
expect(value).toBeLessThan(5); //小于5
expect(value).toBeLessThanOrEqual(4.5); //小于等于4.5
expect(value).toBeCloseTo(0.3); // 浮点数判断相等
expect('Christoph').toMatch(/stop/); //正则表达式判断
expect(['one','two']).toContain('one'); //不解释
```

#### 分组函数

```js
describe("关于每个功能或某个组件的单元测试",()=>{
    // 不同用例的单元测试
})
```

#### 常见命令

```json
{
  "nocache": "jest --no-cache", //清除缓存
  "watch": "jest --watchAll", //实时监听
  "coverage": "jest --coverage",  //生成覆盖测试文档
  "verbose": "npx jest --verbose" //显示测试描述
}
```

### 基础测试

#### 对象等值测试

```js
describe('对象测试', () => {
    it('是否同一个对象', () => {
        const foo = { a: 1 }
        expect(foo).toBe(foo)
    })

    it('对象值是否相等', () => {
        expect({ a: 1, foo: { b: 2 } }).toEqual({ a: 1, foo: { b: 2 } })
    })

    test('对象赋值', () => {
        const data = { one: 1 }
        data['two'] = 2
        expect(data).toEqual({ one: 1, two: 2 })
    })
})
```

![运行测试](JavaScript%E6%B5%8B%E8%AF%95%E6%A1%86%E6%9E%B6.assets/image-20211128111045158.png)

#### 异步测试

##### done 

异步测试脚本执行完，单元测试就结束了，如果需要延时才能断言的结果，单元测试函数需要设置`done`形参，在定时回调函数中调用，显示的通过单元测试已完成。

> 设置了done 的参数。Jest 将在完成测试之前一直等到 done 回调被调用。所以不会提前结束

```js
describe('异步操作测试', () => {
    function foo(callback) {
        console.log('foo...')
        setTimeout(() => {
            callback && callback()
        }, 1000)
    }
    it('异步测试', done => {
        function bar() {
            console.log('bar..')
            done()
        }
        foo(bar)
    })
})
```

![运行测试](JavaScript%E6%B5%8B%E8%AF%95%E6%A1%86%E6%9E%B6.assets/image-20211128111307512.png)

##### 定时器测试（异步测试）及断言

基于jest提供的两个方法`jest.useFakeTimers`和`jest.runAllTimers`可以更优雅的对延时功能的测试。

```js
describe('定时器相关测试', () => {
    // 开启定时函数模拟
    jest.useFakeTimers()

    function foo(callback) {
        console.log('foo...')
        setTimeout(() => {
            callback && callback()
        }, 1000)
    }
    it('断言异步测试', () => {
        //创建mock函数，用于断言函数被执行或是执行次数的判断
        const callback = jest.fn()
        foo(callback)
        expect(callback).not.toBeCalled()
        //快进，使所有定时器回调
        jest.runAllTimers()
        expect(callback).toBeCalled()
    })
})
```

##### Promises

如果使用的是 promise，测试将更加简单。只需要在测试中返回一个 promise，Jest 会自动等待 promise 被解析处理，如果 promise 被拒绝，那么测试失败。

```javascript
function fetchData(err) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      if (err) {
        reject('error')
      } else {
        resolve('peanut butter')
      }
    }, 1000)
  })
}
test('Promise成功测试', () => {
  expect.assertions(1)
  return fetchData(false).then(data => {
    expect(data).toBe('peanut butter')
  })
})
test('Promise异常测试', () => {
  expect.assertions(1)
  return fetchData(true).catch(e => {
    expect(e).toMatch('error')
  })
})

```

> `expect.assertions（number）`验证在测试期间是否调用了一定数量的断言。
> 这在测试异步代码时通常很有用，以确保实际调用了回调中的断言。

##### Async/Await

同样，您也可以在测试中使用 async 和 await 关键字。想要编写异步测试，只需要在传递给 test 的函数前加上 async 关键字。
例如，可以使用以下方法测试相同的 fetchData 场景:

```javascript
function fetchData(err) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      if (err) {
        reject('error')
      } else {
        resolve('peanut butter')
      }
    }, 1000)
  })
}
test('Promise成功测试', async () => {
  expect.assertions(1)
  const data = await fetchData(false)
  expect(data).toBe('peanut butter')
})
test('Promise异常测试', async () => {
  expect.assertions(1)
  try {
    await fetchData(true)
  } catch (e) {
    expect(e).toMatch('error')
  }
})
```

> 注意：Async/Await测试异常时要加try、catch

#### Dom测试

实现dom渲染测试，以及点击事件等交互功能测试。

> 这时就需要我们修改jest.config.js了
>
> ```js
> module.exports = {
>   testEnvironment: 'jsdom'
> }
> ```

```js
describe('Dom测试', () => {
    it('测试按钮是否被渲染 ', () => {
        document.body.innerHTML = `
    <div>
        <button id='btn'>小按钮</button>
    </div> `
        console.log(document.getElementById('btn'), document.getElementById('btn').toString())
        expect(document.getElementById('btn')).not.toBeNull()
        expect(document.getElementById('btn').toString()).toBe('[object HTMLButtonElement]')
    })

    it('测试点击事件', () => {
        const onclick = jest.fn()
        document.body.innerHTML = `
        <div>
            <button id='btn'>小按钮</button>
        </div> `
        const btn = document.getElementById('btn')
        expect(onclick).not.toBeCalled()
        btn.onclick = onclick
        btn.click()
        expect(onclick).toBeCalled()
        expect(onclick).toHaveBeenCalledTimes(1)
        btn.click()
        btn.click()
        expect(onclick).toHaveBeenCalledTimes(3)
    })
})
```

### Vue测试

#### 安装unit-jest

如果你创建的项目没有安装unit-jest依赖包，可以通过`vue add @vue/unit-jest`命令添加。否则通过脚手架手动模式创建一个包含unit-jest的项目。

```sh
cd d:\Dev\lessons\Node.js\examples
vue create vue-jest-project
cd vue-jest-project
# 如果创建项目时没有选择使用jest作为单元测试框架，要重新添加
vue add @vue/unit-jest
# 执行测试
jest --no-cache --verbose
# 或者
npm run test:unit
```

选择使用Jest作为单元测试框架

![选择使用Jest作为单元测试框架](JavaScript%E6%B5%8B%E8%AF%95%E6%A1%86%E6%9E%B6.assets/image-20211128120018234.png)

测试结果

![测试结果](JavaScript%E6%B5%8B%E8%AF%95%E6%A1%86%E6%9E%B6.assets/image-20211128120213281.png)

#### 基础知识

**mount和shallowMount的区别** - shallowMount只挂载指定组件，不挂载子组件 - mount挂载所有组件

**Vue的渲染机制** 默认情况下 Vue 会异步地批量执行更新 (在下一轮 tick)，以避免不必要的 DOM 重绘或者是观察者计算

> 异步测试需要在nextTick()之后执行

#### hello Jest Vue

vue组件渲染测试

```js
import { shallowMount } from '@vue/test-utils'
import HelloWorld from '@/components/HelloWorld.vue'

describe('HelloWorld.vue', () => {
  it('renders props.msg when passed', () => {
    const msg = 'new message'
    const wrapper = shallowMount(HelloWorld, {
      propsData: { msg }
    })
    expect(wrapper.text()).toMatch(msg)
  })
})
```

> 1. jest.config.js已经默认生成了
> 2. 测试框架默认生成的HelloWorld.vue
> 3. 修改props.msg
> 4. 断言页面上是否渲染成功

#### 事件测试

新建组件`CountBtn.vue`

```vue
<template>
  <button v-on:click="countBtn">点击次数{{ count }}</button>
</template>

<script>
export default {
  name: 'CountBtn',
  data() {
    return {
      count: 0
    }
  },
  methods: {
    countBtn: function () {
      this.count++
    }
  }
}
</script>

<style scoped></style>
```

vue组件点击事件测试`click.spec.js`

```js
import { shallowMount } from '@vue/test-utils'
import CountBtn from '@/components/CountBtn.vue'

it('测试countBtn组件点击', done => {
  const wraper = shallowMount(CountBtn)
  const btn = wraper.find('button')
  expect(wraper.html()).toBe(`<button>点击次数0</button>`)
  btn.trigger('click')
  setTimeout(() => {
    expect(wraper.html()).toBe(`<button>点击次数1</button>`)
    done()
  }, 1000)
})

it('优雅的测试点击事件', async () => {
  const wraper = shallowMount(CountBtn)
  const btn = wraper.find('button')
  expect(wraper.html()).toBe(`<button>点击次数0</button>`)
  btn.trigger('click')
  await wraper.vm.$nextTick()
  expect(wraper.html()).toBe(`<button>点击次数1</button>`)
})
```

![image-20211128121559732](JavaScript%E6%B5%8B%E8%AF%95%E6%A1%86%E6%9E%B6.assets/image-20211128121559732.png)

#### axios异步请示测试

##### 使用ApiFox设定Mock数据

通过ApiFox设定Mock数据，方便坐异步请求测试

![通过ApiFox设定Mock数据](JavaScript%E6%B5%8B%E8%AF%95%E6%A1%86%E6%9E%B6.assets/image-20211128123119243.png)

![通过ApiFox设定Mock数据](JavaScript%E6%B5%8B%E8%AF%95%E6%A1%86%E6%9E%B6.assets/image-20211128123246524.png)

模拟异步请示，测试渲染结果是否一致

##### 安装axios

```sh
npm install axios
```

##### 编写User.vue

```vue
<!-- User.vue -->
<template>
    <table>
        <tr v-for="item in list" :key="item.id">
            <td>{{ item.id }}</td>
            <td>{{ item.name }}</td>
            <td>{{ item.age }}</td>
        </tr>
    </table>
</template>

<script>
import axios from 'axios'
export default {
    data() {
        return {
            api: axios,
            list: []
        }
    },
    created() {
        this.api
            .get('http://127.0.0.1:4523/mock/2717/users')
            .then(resp => (this.list = resp.data.data))
            .catch(function (error) {
                // 请求失败处理
                console.log(error)
            })
    }
}
</script>
```

```javascript
import { mount } from '@vue/test-utils'
import User from '@/components/User'
import axios from 'axios'
it('测试用户组件', async () => {
    const wrapper = mount(User)
    console.log(wrapper.html())
    // 渲染前
    expect(wrapper.html()).toBe('<table></table>')
    let apiData = await callApi()
    await wrapper.setData({
        list: apiData.data
    })
    await wrapper.vm.$nextTick()
    // 渲染后
    // console.log(wrapper.html())
    // console.log(wrapper.find('tr'))
    expect(wrapper.findAll('tr').length).toBe(apiData.data.length)
    expect(wrapper.findAll('td').at(2).html()).toBe('<td>' + apiData.data[0].age + '</td>')
})

function callApi() {
    return new Promise((resolve, reject) =>
        axios
            .get('http://127.0.0.1:4523/mock/2717/users')
            .then(resp => {
                resolve(resp.data)
            })
            .catch(function (error) {
                // 请求失败处理
                console.log(error)
                reject(error)
            })
    )
}
```

## Mocha

[`Mocha`](https://mochajs.org/)（发音"摩卡"）诞生于2011年，是现在最流行的JavaScript测试框架之一，在浏览器和Node环境都可以使用。

所谓"测试框架"，就是运行测试的工具。通过它，可以为JavaScript应用添加测试，从而保证代码的质量。

![Mocha](JavaScript%E6%B5%8B%E8%AF%95%E6%A1%86%E6%9E%B6.assets/bg2015120301.png)



### 安装

```sh
$ npm install --global mocha
```

### 测试脚本的写法

`Mocha`的作用是运行测试脚本，首先必须学会写测试脚本。所谓"测试脚本"，就是用来测试源码的脚本。

下面是一个加法模块[`add.js`](https://github.com/ruanyf/mocha-demos/blob/master/demo01/add.js)的代码。

```javascript
// add.js
function add(x, y) {
  return x + y;
}

module.exports = add;
```

要测试这个加法模块是否正确，就要写测试脚本。

通常，测试脚本与所要测试的源码脚本同名，但是后缀名为`.test.js`（表示测试）或者`.spec.js`（表示规格）。比如，`add.js`的测试脚本名字就是`add.test.js`。

```javascript
// add.test.js
var add = require('./add.js');
var expect = require('chai').expect;

describe('加法函数的测试', function() {
  it('1 加 1 应该等于 2', function() {
    expect(add(1, 1)).to.be.equal(2);
  });
});
```

上面这段代码，就是测试脚本，它可以独立执行。测试脚本里面应该包括一个或多个`describe`块，每个`describe`块应该包括一个或多个`it`块。

`describe`块称为"测试套件"（test suite），表示一组相关的测试。它是一个函数，第一个参数是测试套件的名称（"加法函数的测试"），第二个参数是一个实际执行的函数。

`it`块称为"测试用例"（test case），表示一个单独的测试，是测试的最小单位。它也是一个函数，第一个参数是测试用例的名称（"1 加 1 应该等于 2"），第二个参数是一个实际执行的函数。

### 断言库的用法

```sh
$ npm install chai
```

上面的测试脚本里面，有一句断言。

```javascript
expect(add(1, 1)).to.be.equal(2);
```

所谓"断言"，就是判断源码的实际执行结果与预期结果是否一致，如果不一致就抛出一个错误。上面这句断言的意思是，调用`add(1, 1)`，结果应该等于2。

所有的测试用例（it块）都应该含有一句或多句的断言。它是编写测试用例的关键。断言功能由断言库来实现，Mocha本身不带断言库，所以必须先引入断言库。

```javascript
var expect = require('chai').expect;
```

断言库有很多种，Mocha并不限制使用哪一种。上面代码引入的断言库是[`chai`](http://chaijs.com/)，并且指定使用它的[`expect`](http://chaijs.com/api/bdd/)断言风格。

`expect`断言的优点是很接近自然语言，下面是一些例子。

```javascript
// 相等或不相等
expect(4 + 5).to.be.equal(9);
expect(4 + 5).to.be.not.equal(10);
expect(foo).to.be.deep.equal({ bar: 'baz' });

// 布尔值为true
expect('everthing').to.be.ok;
expect(false).to.not.be.ok;

// typeof
expect('test').to.be.a('string');
expect({ foo: 'bar' }).to.be.an('object');
expect(foo).to.be.an.instanceof(Foo);

// include
expect([1,2,3]).to.include(2);
expect('foobar').to.contain('foo');
expect({ foo: 'bar', hello: 'universe' }).to.include.keys('foo');

// empty
expect([]).to.be.empty;
expect('').to.be.empty;
expect({}).to.be.empty;

// match
expect('foobar').to.match(/^foo/);
```

基本上，`expect`断言的写法都是一样的。头部是`expect`方法，尾部是断言方法，比如`equal`、`a`/`an`、`ok`、`match`等。两者之间使用`to`或`to.be`连接。

如果`expect`断言不成立，就会抛出一个错误。事实上，只要不抛出错误，测试用例就算通过。

```javascript
it('1 加 1 应该等于 2', function() {});
```

上面的这个测试用例，内部没有任何代码，由于没有抛出了错误，所以还是会通过。

### Mocha的基本用法

有了测试脚本以后，就可以用Mocha运行它。

```sh
$ mocha add.test.js

  加法函数的测试
    ✓ 1 加 1 应该等于 2

  1 passing (8ms)
```

上面的运行结果表示，测试脚本通过了测试，一共只有1个测试用例，耗时是8毫秒。

`mocha`命令后面紧跟测试脚本的路径和文件名，可以指定多个测试脚本。

```sh
$ mocha file1 file2 file3
```

Mocha默认运行`test`子目录里面的测试脚本。所以，一般都会把测试脚本放在`test`目录里面，然后执行`mocha`就不需要参数了。

```sh
$ mocha

  加法函数的测试
    ✓ 1 加 1 应该等于 2
    ✓ 任何数加0应该等于自身

  2 passing (9ms)
```

这时可以看到，`test`子目录里面的测试脚本执行了。但是，你打开`test`子目录，会发现下面还有一个`test/dir`子目录，里面还有一个测试脚本[`multiply.test.js`](https://github.com/ruanyf/mocha-demos/blob/master/demo02/test/dir/multiply.test.js)，并没有得到执行。原来，Mocha默认只执行`test`子目录下面第一层的测试用例，不会执行更下层的用例。

为了改变这种行为，就必须加上`--recursive`参数，这时`test`子目录下面所有的测试用例----不管在哪一层----都会执行。

```sh
$ mocha --recursive

  加法函数的测试
    ✓ 1 加 1 应该等于 2
    ✓ 任何数加0应该等于自身

  乘法函数的测试
    ✓ 1 乘 1 应该等于 1

  3 passing (9ms)
```

### 通配符

命令行指定测试脚本时，可以使用通配符，同时指定多个文件。

```sh
$ mocha spec/{my,awesome}.js
$ mocha test/unit/*.js
```

上面的第一行命令，指定执行`spec`目录下面的`my.js`和`awesome.js`。第二行命令，指定执行`test/unit`目录下面的所有js文件。

除了使用Shell通配符，还可以使用Node通配符。

```sh
$ mocha 'test/**/*.@(js|jsx)'
```

上面代码指定运行`test`目录下面任何子目录中、文件后缀名为`js`或`jsx`的测试脚本。注意，Node的通配符要放在单引号之中，否则星号（`*`）会先被Shell解释。

上面这行Node通配符，如果改用Shell通配符，要写成下面这样。

```sh
$ mocha test/{,**/}*.{js,jsx}
```

### 命令行参数

除了前面介绍的`--recursive`，Mocha还可以加上其他命令行参数。

#### --help, -h

`--help`或`-h`参数，用来查看Mocha的所有命令行参数。

```sh
$ mocha --help
```

#### --reporter, -R

`--reporter`参数用来指定测试报告的格式，默认是`spec`格式。

```sh
$ mocha
# 等同于
$ mocha --reporter spec
```

除了`spec`格式，官方网站还提供了其他许多[报告格式](https://mochajs.org/#reporters)。

```sh
$ mocha --reporter tap

1..2
ok 1 加法函数的测试 1 加 1 应该等于 2
ok 2 加法函数的测试 任何数加0应该等于自身
# tests 2
# pass 2
# fail 0
```

上面是`tap`格式报告的显示结果。

`--reporters`参数可以显示所有内置的报告格式。

```sh
$ mocha --reporters
```

使用[`mochawesome`](https://adamgruber.github.io/mochawesome/)模块，可以生成漂亮的HTML格式的报告。

![mochawesome](JavaScript%E6%B5%8B%E8%AF%95%E6%A1%86%E6%9E%B6.assets/bg2015120303.png)

```sh
$ npm install --save-dev mochawesome
$ .\node_modules\.bin\mocha add.test.js --reporter mochawesome
```

上面代码中，`mocha`命令使用了项目内安装的版本，而不是全局安装的版本，因为`mochawesome`模块是安装在项目内的。

然后，测试结果报告就在`mochaawesome-reports`子目录生成。

```sh
λ .\node_modules\.bin\mocha add.test.js --reporter mochawesome


  加法函数的测试
    √ 1 加 1 应该等于 2


  1 passing (7ms)

[mochawesome] Report JSON saved to d:\Dev\lessons\Node.js\examples\Mocha\mochawesome-report\mochawesome.json

[mochawesome] Report HTML saved to d:\Dev\lessons\Node.js\examples\Mocha\mochawesome-report\mochawesome.html
```

#### --growl, -G

打开[`--growl`](http://growl.info/)参数，就会将测试结果在桌面显示。

##### 安装growl

**macOS**

On OS X 10.8+, Notification Center is supported via [terminal-notifier](https://github.com/alloy/terminal-notifier/).

```
$ sudo gem install terminal-notifier
$ npm install growl
```

**Linux**

Install "notify-send" through the [libnotify-bin](https://packages.ubuntu.com/trusty/libnotify-bin) APT package. If you use RPM packages, substitute appropriately.

```
$ sudo apt-get install libnotify-bin
$ npm install growl
```

**Windows**

Download and install [Growl for Windows](https://github.com/briandunnington/growl-for-windows/releases/download/final/GrowlInstaller.exe) which contains [growlnotify (win)](https://github.com/briandunnington/growl-for-windows/blob/master/Growl Extras/growlnotify/growlnotify.exe). Assuming defaults were taken, "C:\Program Files (x86)\Growl for Windows" will be the installation directory.

[Adjust your **PATH** environment variable](https://docs.telerik.com/teststudio/features/test-runners/add-path-environment-variables) to add the Growl installation directory. Once that's done, turn Growl on and send yourself a test notification.

```
C:> growl start
C:> growlnotify "it works!"
```

Finally, install the npm package needed to allow Mocha to send you notifications.

```
C:> npm install growl
```

##### 使用growl

```sh
$ mocha --growl
```



![growl](JavaScript%E6%B5%8B%E8%AF%95%E6%A1%86%E6%9E%B6.assets/bg2015120304.png)

#### --watch，-w

`--watch`参数用来监视指定的测试脚本。只要测试脚本有变化，就会自动运行Mocha。

```sh
$ mocha --watch
```

上面命令执行以后，并不会退出。你可以另外打开一个终端窗口，修改`test`目录下面的测试脚本`add.test.js`，比如删除一个测试用例，一旦保存，Mocha就会再次自动运行。

#### --bail, -b

`--bail`参数指定只要有一个测试用例没有通过，就停止执行后面的测试用例。[这对]()[持续集成](https://www.ruanyifeng.com/blog/2015/09/continuous-integration.html)很有用。

```sh
$ mocha --bail
```

#### --grep, -g

`--grep`参数用于搜索测试用例的名称（即`it`块的第一个参数），然后只执行匹配的测试用例。

```sh
$ mocha --grep "1 加 1"
```

上面代码只测试名称中包含"1 加 1"的测试用例。

#### --invert, -i

`--invert`参数表示只运行不符合条件的测试脚本，必须与`--grep`参数配合使用。

```sh
$ mocha --grep "1 加 1" --invert
```

### 配置文件mocha.opts

Mocha允许在`test`目录下面，放置配置文件`mocha.opts`，把命令行参数写在里面。请先进入[`demo03`](https://github.com/ruanyf/mocha-demos/tree/master/demo03)目录，运行下面的命令。

```sh
$ mocha --recursive --reporter tap --growl
```

上面这个命令有三个参数`--recursive`、`--reporter tap`、`--growl`。

然后，把这三个参数写入`test`目录下的[`mocha.opts`](https://github.com/ruanyf/mocha-demos/blob/master/demo03/test/mocha.opts)文件。

```sh
--reporter tap
--recursive
--growl
```

然后，执行`mocha`就能取得与第一行命令一样的效果。

> ```bash
> $ mocha
> ```

如果测试用例不是存放在test子目录，可以在`mocha.opts`写入以下内容。

```sh
server-tests
--recursive
```

上面代码指定运行`server-tests`目录及其子目录之中的测试脚本。

### ES6测试

如果测试脚本是用ES6写的，那么运行测试之前，需要先用Babel转码。

```javascript
import add from '../src/add.js';
import chai from 'chai';

let expect = chai.expect;

describe('加法函数的测试', function() {
  it('1 加 1 应该等于 2', function() {
    expect(add(1, 1)).to.be.equal(2);
  });
});
```

ES6转码，需要安装Babel。

```sh
$ npm install babel-core babel-preset-es2015 --save-dev
```

然后，在项目目录下面，新建一个`.babelrc`配置文件。

```json
{
  "presets": [ "es2015" ]
}
```

最后，使用`--require`参数指定测试脚本的转码器。

```sh
$ .\node_modules\.bin\mocha es6.test.js --require babel-core/register
```

上面代码中，`--require`参数后面紧跟一个用冒号分隔的字符串，冒号左边是文件的后缀名，右边是用来处理这一类文件的模块名。上面代码表示，运行测试之前，先用`babel-core/register`模块，处理一下`.js`文件。由于这里的转码器安装在项目内，所以要使用项目内安装的Mocha；如果转码器安装在全局，就可以使用全局的Mocha。

下面是另外一个例子，使用Mocha测试CoffeeScript脚本。测试之前，先将`.coffee`文件转成`.js`文件。

```sh
$ mocha --require --require coffeescript/register
```

![测试结果](JavaScript%E6%B5%8B%E8%AF%95%E6%A1%86%E6%9E%B6.assets/image-20211128135424562.png)

注意，Babel默认不会对Iterator、Generator、Promise、Map、Set等全局对象，以及一些全局对象的方法（比如`Object.assign`）转码。如果你想要对这些对象转码，就要安装`babel-polyfill`。

```sh
$ npm install babel-polyfill --save
```

然后，在你的脚本头部加上一行。

```javascript
import 'babel-polyfill'
```

> 注意：原有的`--compilers`参数已经被`--require`参数替代
>
> - CoffeeScript: `--compilers coffee:coffee-script/register` becomes `--require coffeescript/register`
> - Babel 6: `--compilers js:babel-core/register` becomes `--require babel-core/register`
> - Babel 7: `--require babel-core/register` used if you are using Babel v6 becomes `--require @babel/register` with Babel v7.
> - TypeScript: `--compilers ts:ts-node/register` becomes `--require ts-node/register`
> - LiveScript: `--compilers ls:livescript` becomes `--require livescript`

### 异步测试

Mocha默认每个测试用例最多执行2000毫秒，如果到时没有得到结果，就报错。对于涉及异步操作的测试用例，这个时间往往是不够的，需要用`-t`或`--timeout`参数指定超时门槛。

```javascript
var expect = require('chai').expect
it('测试应该5000毫秒后结束', function (done) {
  var x = true
  var f = function () {
    x = false
    expect(x).to.be.not.ok
    done() // 通知Mocha测试结束
  }
  setTimeout(f, 4000)
})
```

上面的测试用例，需要4000毫秒之后，才有运行结果。所以，需要用`-t`或`--timeout`参数，改变默认的超时设置。

```sh
$ mocha -t 5000 timeout.test.js
```

上面命令将测试的超时时限指定为5000毫秒。

另外，上面的测试用例里面，有一个`done`函数。`it`块执行的时候，传入一个`done`参数，当测试结束的时候，必须显式调用这个函数，告诉Mocha测试结束了。否则，Mocha就无法知道，测试是否结束，会一直等到超时报错。你可以把这行删除试试看。

Mocha默认会高亮显示超过75毫秒的测试用例，可以用`-s`或`--slow`调整这个参数。

```sh
$ mocha -t 5000 -s 1000 timeout.test.js
```

上面命令指定高亮显示耗时超过1000毫秒的测试用例。

下面是另外一个异步测试的例子`async.test.js`。

```sh
npm i request
```

async.test.js

```javascript
var request = require('request')
var expect = require('chai').expect
it('异步请求应该返回一个对象', function (done) {
  request.get(
    {
      url: 'https://api.github.com'
    },
    (err, response, body) => {
      expect(response).to.be.an('object')
      done()
    }
  )
})
```

运行下面命令，可以看到这个测试会通过。

```sh
$ mocha -t 10000 async.test.js
```

另外，Mocha内置对Promise的支持，允许直接返回Promise，等到它的状态改变，再执行断言，而不用显式调用`done`方法。请看`promise.test.js`。

```javascript
var request = require('request')
var expect = require('chai').expect
it('异步请求应该返回一个对象', function () {
  return callApi().then(function (res) {
    expect(res).to.be.an('object')
  })
})

function callApi() {
  return new Promise((resolve, reject) =>
    request.post(
      {
        url: 'https://api.github.com'
      },
      (err, response, body) => {
        if (err) {
          reject(err)
        } else {
          resolve(response)
        }
      }
    )
  )
}
```

### 测试用例的钩子

Mocha在`describe`块之中，提供测试用例的四个钩子：`before()`、`after()`、`beforeEach()`和`afterEach()`。它们会在指定时间执行。

```javascript
describe('hooks', function() {

  before(function() {
    // 在本区块的所有测试用例之前执行
  });

  after(function() {
    // 在本区块的所有测试用例之后执行
  });

  beforeEach(function() {
    // 在本区块的每个测试用例之前执行
  });

  afterEach(function() {
    // 在本区块的每个测试用例之后执行
  });

  // test cases
});
```

`beforeEach`的例子`beforeEach.test.js`

```javascript
// beforeEach.test.js
describe('beforeEach示例', function() {
  var foo = false;

  beforeEach(function() {
    foo = true;
  });

  it('修改全局变量应该成功', function() {
    expect(foo).to.be.equal(true);
  });
});
```

上面代码中，`beforeEach`会在`it`之前执行，所以会修改全局变量。

另一个例子`beforeEach-async.test.js`则是演示，如何在`beforeEach`之中使用异步操作。

```javascript
var expect = require('chai').expect
describe('异步 beforeEach 示例', function () {
  var foo = false

  beforeEach(function (done) {
    setTimeout(function () {
      foo = true
      done()
    }, 50)
  })

  it('全局变量异步修改应该成功', function () {
    expect(foo).to.be.equal(true)
  })
})
```

### 测试用例管理

大型项目有很多测试用例。有时，我们希望只运行其中的几个，这时可以用`only`方法。`describe`块和`it`块都允许调用`only`方法，表示只运行某个测试套件或测试用例。

测试脚本`test/add.test.js`就使用了`only`。

```javascript
it.only('1 加 1 应该等于 2', function() {
  expect(add(1, 1)).to.be.equal(2);
});

it('任何数加0应该等于自身', function() {
  expect(add(1, 0)).to.be.equal(1);
});
```

上面代码中，只有带有`only`方法的测试用例会运行。

```sh
$ mocha test/add.test.js

  加法函数的测试
    ✓ 1 加 1 应该等于 2

  1 passing (10ms)
```

此外，还有`skip`方法，表示跳过指定的测试套件或测试用例。

```javascript
it.skip('任何数加0应该等于自身', function() {
  expect(add(1, 0)).to.be.equal(1);
});
```

上面代码的这个测试用例不会执行。

### 浏览器测试

除了在命令行运行，Mocha还可以在浏览器运行。

![Mocha还可以在浏览器运行](JavaScript%E6%B5%8B%E8%AF%95%E6%A1%86%E6%9E%B6.assets/bg2015120305.png)

首先，使用`mocha init`命令在指定目录生成初始化文件。

```sh
$ mocha init demo
```

运行上面命令，就会在`demo`目录下生成`index.html`文件，以及配套的脚本和样式表。

```html
<!DOCTYPE html>
<html>
  <body>
    <h1>Unit.js tests in the browser with Mocha</h1>
    <div id="mocha"></div>
    <script src="mocha.js"></script>
    <script>
      mocha.setup('bdd');
    </script>
    <script src="tests.js"></script>
    <script>
      mocha.run();
    </script>
  </body>
</html>
```

然后，新建一个源码文件`add.js`。

```javascript
// add.js
function add(x, y) {
  return x + y;
}
```

然后，把这个文件，以及断言库`chai.js`，加入`index.html`。

```html
<script>
  mocha.setup('bdd');
</script>
<script src="add.js"></script>
<script src="http://chaijs.com/chai.js"></script>
<script src="tests.js"></script>
<script>
  mocha.run();
</script>
```

最后，在`tests.js`里面写入测试脚本。

```javascript
var expect = chai.expect

describe('加法函数的测试', function () {
  it('1 加 1 应该等于 2', function () {
    expect(add(1, 1)).to.be.equal(2)
  })

  it('任何数加0等于自身', function () {
    expect(add(1, 0)).to.be.equal(1)
    expect(add(0, 0)).to.be.equal(0)
  })
})
```

现在，在浏览器里面打开`index.html`，就可以看到测试脚本的运行结果。

### 生成规格文件

Mocha支持从测试用例生成规格文件。

![Mocha支持从测试用例生成规格文件](JavaScript%E6%B5%8B%E8%AF%95%E6%A1%86%E6%9E%B6.assets/bg2015120306.png)

进入目录，运行下面的命令。

```sh
$ .\node_modules\.bin\mocha *.test.js -R markdown > spec.md --require babel-core/register
```

上面命令根据`test`目录的所有测试脚本，生成一个规格文件`spec.md`。`-R markdown`参数指定规格报告是markdown格式。

如果想生成HTML格式的报告`spec.html`，使用下面的命令。

```sh
$ .\node_modules\.bin\mocha *.test.js -R doc > spec.html --require babel-core/register
```

### 参考文章

[测试框架 Mocha 实例教程 - 阮一峰的网络日志 (ruanyifeng.com)](http://www.ruanyifeng.com/blog/2015/12/a-mocha-tutorial-of-examples.html)
