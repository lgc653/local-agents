# Vue3组件

## 引言

在现代 Web 开发中，我们往往需要构建复杂且交互丰富的用户界面。为了提高代码的可维护性、可复用性和开发效率，组件化开发应运而生。试想一下，如果每次需要构建一个新的页面元素，都需要从头开始编写 HTML、CSS 和 JavaScript 代码，那将是多么低效和容易出错的事情。

组件化开发的核心思想是将用户界面拆分成一个个独立的、可复用的组件，每个组件都包含了自己的结构、样式和行为。就像搭积木一样，我们可以将这些组件组合起来，构建出各种各样的页面和应用。

Vue.js 作为一款流行的 JavaScript 框架，为组件化开发提供了强大的支持。在 Vue.js 中，组件是构成应用的基本单元，它们可以嵌套组合，形成复杂的组件树，最终渲染出完整的用户界面。

![img](Vue3组件.assets/components.png)

## Vue.js 中的组件

组件是 Vue.js 应用的构建块，每个 Vue 组件都是一个独立的、可复用的 UI 单元。 它们可以被理解为自定义的 HTML 元素，拥有自己的模板、逻辑和样式。 组件可以嵌套，形成组件树，构建复杂的应用界面，就像用乐高积木搭建城堡一样。

## Vue.3 组件的定义和使用

### 单文件组件 (SFC)

Vue3 推荐使用单文件组件 (SFC) 来组织组件代码。SFC 使用 `.vue` 扩展名，将组件的模板、脚本和样式整合在一个文件中，结构清晰，易于维护。

```vue
<template>
  <div>{{ message }}</div>
</template>

<script>
import { defineComponent } from 'vue';

export default defineComponent({
  data() {
    return {
      message: 'Hello from MyComponent!'
    };
  }
});
</script>

<style scoped>
div {
  font-weight: bold;
}
</style>
```

### 使用 `defineComponent` 函数定义组件

在 SFC 的 `<script>` 标签中，我们使用 `defineComponent` 函数来定义一个 Vue 组件。

```javascript
import { defineComponent } from 'vue';

export default defineComponent({
  // 组件选项
});
```

### 注册组件

在使用组件之前，我们需要先将它注册到 Vue 应用中（全局注册）。

```javascript
import { createApp } from 'vue';
import MyComponent from './MyComponent.vue';

const app = createApp({});
app.component('my-component', MyComponent);
app.mount('#app');
```

### 使用组件

注册之后，我们就可以在模板中像使用普通的 HTML 元素一样使用组件了。

```vue
<template>
  <div>
    <my-component></my-component>
  </div>
</template>
```

### 局部注册

全局注册虽然很方便，但有以下几个问题：

1. 全局注册，但并没有被使用的组件无法在生产打包时被自动移除 (也叫“tree-shaking”)。如果你全局注册了一个组件，即使它并没有被实际使用，它仍然会出现在打包后的 JS 文件中。
2. 全局注册在大型项目中使项目的依赖关系变得不那么明确。在父组件中使用子组件时，不太容易定位子组件的实现。和使用过多的全局变量一样，这可能会影响应用长期的可维护性。

在使用 `<script setup>` 的单文件组件中，导入的组件可以直接在模板中使用，无需注册：

```vue
<script setup>
import ComponentA from './ComponentA.vue'
</script>

<template>
  <ComponentA />
</template>
```

如果没有使用 `<script setup>`，则需要使用 `components` 选项来显式注册：

```javascript
import ComponentA from './ComponentA.js'

export default {
  components: {
    ComponentA
  },
  setup() {
    // ...
  }
}
```

## 组件的构成

每个 Vue 组件都由三个部分组成：

### 模板 (Template)

组件的 HTML 结构，可以使用 Vue 的模板语法进行数据绑定、事件绑定等。

```vue
<template>
  <button @click="handleClick">{{ buttonText }}</button>
</template>
```

### 脚本 (Script)

组件的逻辑，使用 JavaScript 编写，包括：

* **数据 (data):** 组件内部的状态。
* **计算属性 (computed):** 根据数据计算得到的值。
* **方法 (methods):** 组件内部的函数。
* **生命周期钩子 (lifecycle hooks):** 在组件不同阶段执行的函数。

```javascript
<script>
export default {
  data() {
    return {
      count: 0
    };
  },
  computed: {
    doubleCount() {
      return this.count * 2;
    }
  },
  methods: {
    handleClick() {
      this.count++;
    }
  },
  mounted() {
    console.log('Component mounted!');
  }
};
</script>
```

### 样式 (Style)

组件的样式，可以使用 CSS 或预处理器。可以使用 `scoped` 属性将样式限制在当前组件内，避免样式污染。

```vue
<style scoped>
.button {
  background-color: #4CAF50;
  color: white;
}
</style>
```

## 组件间通信

在实际开发中，组件之间 often 需要进行数据传递和事件交互。

### 父子组件通信

* **Props down, Events up:**  这是 Vue.js 中推荐的父子组件通信方式。
* **`props`:** 父组件通过 `props` 向子组件传递数据。
* **`emits`:** 子组件通过 `emits` 向父组件发送事件。

#### 示例：显示用户详情

这个例子中，我们将创建一个父组件 `UserList` 和一个子组件 `UserDetail`。`UserList` 负责展示用户列表，点击用户时，将用户的详细信息传递给 `UserDetail` 进行展示。

**子组件 UserDetail.vue:**

```vue
<template>
  <div v-if="user" class="user-detail">
    <h3>{{ user.name }}</h3>
    <p>Email: {{ user.email }}</p>
    <p>Age: {{ user.age }}</p>
  </div>
</template>

<script>
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'UserDetail',
  props: {
    user: {
      type: Object,
      required: true,
    },
  },
});
</script>

<style scoped>
.user-detail {
  border: 1px solid #ccc;
  padding: 10px;
  margin-top: 10px;
}
</style>
```

**解释:**

* **`props`:** `UserDetail` 组件定义了一个名为 `user` 的 prop，用于接收父组件传递的用户信息。
* **`required: true`:**  表示 `user` prop 是必需的，父组件必须传递该 prop。
* **`v-if="user"`:**  只有当 `user` prop 存在时，才会渲染用户信息。

**父组件 UserList.vue:**

```vue
<template>
  <div>
    <h2>用户列表</h2>
    <ul>
      <li v-for="user in users" :key="user.id" @click="selectUser(user)">
        {{ user.name }}
      </li>
    </ul>
    <user-detail :user="selectedUser"></user-detail>
  </div>
</template>

<script>
import { defineComponent, ref } from 'vue';
import UserDetail from './UserDetail.vue';

export default defineComponent({
  name: 'UserList',
  components: {
    UserDetail,
  },
  setup() {
    const users = ref([
      { id: 1, name: '张三', email: 'zhangsan@example.com', age: 25 },
      { id: 2, name: '李四', email: 'lisi@example.com', age: 30 },
      { id: 3, name: '王五', email: 'wangwu@example.com', age: 28 },
    ]);
    const selectedUser = ref(null);

    const selectUser = (user) => {
      selectedUser.value = user;
    };

    return {
      users,
      selectedUser,
      selectUser,
    };
  },
});
</script>
```

**解释:**

* **注册子组件:** `UserList` 组件通过 `components` 选项注册了 `UserDetail` 子组件。
* **`v-for`:** 循环渲染用户列表。
* **`@click="selectUser(user)"`:**  点击用户时，调用 `selectUser` 方法，将当前用户对象传递给 `selectedUser`。
* **`:user="selectedUser"`:**  将 `selectedUser` 数据作为 prop 传递给 `UserDetail` 组件。

### 非父子组件通信

* **Provide / Inject:** 允许祖先组件向其所有后代组件注入依赖。
* **Event Bus:** 创建一个全局的事件总线，用于组件之间发送和接收事件。
* **Vuex / Pinia:**  使用状态管理库，集中管理应用状态，方便组件之间共享和修改数据。

#### 使用 Provide / Inject 实现深色模式切换、

> **Provide / Inject:**  适用于祖先组件和后代组件之间的通信，无论它们之间嵌套层级有多深。它可以避免 prop drilling (props 穿透) 的问题，使代码更加简洁易懂。

**创建一个提供主题的祖先组件:**

```vue
<template>
  <div>
    <slot />
  </div>
</template>

<script>
import { provide, ref } from 'vue';

export default {
  setup() {
    const theme = ref('light');

    provide('theme', theme);

    const toggleTheme = () => {
      theme.value = theme.value === 'light' ? 'dark' : 'light';
    };

    return {
      toggleTheme,
    };
  },
};
</script>
```

**解释:**

* 使用 `provide('theme', theme)` 将 `theme` 响应式数据提供给所有后代组件。
* 提供一个 `toggleTheme` 方法，用于切换主题。

**创建 ThemeSwitcher 组件:**

```vue
<template>
  <button @click="toggleTheme">
    {{ theme === 'light' ? '开启深色模式' : '关闭深色模式' }}
  </button>
</template>

<script>
import { inject } from 'vue';

export default {
  setup() {
    const theme = inject('theme');
    const toggleTheme = inject('toggleTheme');

    return {
      theme,
      toggleTheme,
    };
  },
};
</script>
```

**解释:**

* 使用 `inject('theme')` 获取祖先组件提供的 `theme` 数据。
* 使用 `inject('toggleTheme')` 获取祖先组件提供的 `toggleTheme` 方法。

**创建 Navbar 组件:**

```vue
<template>
  <nav :class="{ 'dark-theme': theme === 'dark' }">
    <!-- 导航栏内容 -->
  </nav>
</template>

<script>
import { inject } from 'vue';

export default {
  setup() {
    const theme = inject('theme');

    return {
      theme,
    };
  },
};
</script>
```

**解释:**

* 使用 `inject('theme')` 获取祖先组件提供的 `theme` 数据。

**在主应用中使用组件:**

```vue
<template>
  <theme-provider>
    <theme-switcher />
    <navbar />
  </theme-provider>
</template>

<script>
import ThemeProvider from './ThemeProvider.vue';
import ThemeSwitcher from './ThemeSwitcher.vue';
import Navbar from './Navbar.vue';

export default {
  components: {
    ThemeProvider,
    ThemeSwitcher,
    Navbar,
  },
};
</script>
```

**解释:**

* 将 `ThemeSwitcher` 和 `Navbar` 组件包裹在 `ThemeProvider` 组件内部，这样它们就可以访问到 `ThemeProvider` 提供的 `theme` 数据和 `toggleTheme` 方法。

#### 示例：使用 Event Bus 实现深色模式切换

> **Event Bus:**  适用于任意组件之间的通信，无论它们之间是否存在父子关系。它可以实现组件之间的解耦，但如果过度使用，可能会导致代码难以维护。

**1. 创建一个事件总线 (event bus):**

```javascript
// eventBus.js
import { reactive } from 'vue';

export const eventBus = reactive({
  theme: 'light',
  changeTheme(newTheme) {
    this.theme = newTheme;
  },
});
```

**2. ThemeSwitcher 组件:**

```vue
<template>
  <button @click="toggleTheme">
    {{ theme === 'light' ? '开启深色模式' : '关闭深色模式' }}
  </button>
</template>

<script>
import { eventBus } from './eventBus.js';

export default {
  setup() {
    const theme = eventBus.theme;

    const toggleTheme = () => {
      eventBus.changeTheme(theme === 'light' ? 'dark' : 'light');
    };

    return {
      theme,
      toggleTheme,
    };
  },
};
</script>
```

**解释:**

* `ThemeSwitcher` 组件导入了 `eventBus`。
* `theme` 数据直接从 `eventBus` 获取。
* 点击按钮时，调用 `toggleTheme` 方法，通过 `eventBus.changeTheme` 方法修改主题。

**3. Navbar 组件:**

```vue
<template>
  <nav :class="{ 'dark-theme': theme === 'dark' }">
    <!-- 导航栏内容 -->
  </nav>
</template>

<script>
import { eventBus } from './eventBus.js';

export default {
  setup() {
    const theme = eventBus.theme;

    return {
      theme,
    };
  },
};
</script>

<style>
.dark-theme {
  background-color: #333;
  color: white;
}
</style>
```

**解释:**

* `Navbar` 组件也导入了 `eventBus`。
* `theme` 数据直接从 `eventBus` 获取。
* 根据 `theme` 的值动态添加 `dark-theme` 类名，控制导航栏的样式。

**4. 在主应用中使用组件:**

```vue
<template>
  <div>
    <theme-switcher />
    <navbar />
  </div>
</template>

<script>
import ThemeSwitcher from './ThemeSwitcher.vue';
import Navbar from './Navbar.vue';

export default {
  components: {
    ThemeSwitcher,
    Navbar,
  },
};
</script>
```

## 高级组件特性

* **插槽 (Slots):** 允许父组件向子组件传递内容，使得组件更加灵活和可复用。
* **动态组件 (Dynamic Components):**  根据条件动态切换组件，例如根据用户角色显示不同的内容。
* **异步组件 (Async Components):** 延迟加载组件，提高应用性能，例如只在需要时才加载某个组件。

你总结得非常到位！Vue 3 的高级组件特性确实包括插槽、动态组件和异步组件，它们极大地提升了组件的灵活性和复用性。以下是一些更详细的解释和示例：

### 插槽 (Slots)

   - **作用：** 允许父组件向子组件传递内容，并在子组件的特定位置进行渲染。
   - **类型：**
      - **默认插槽：**  没有命名的插槽，用于传递主要内容。
      - **具名插槽：**  使用 `name` 属性定义，用于传递特定内容到子组件的不同部分。
      - **作用域插槽：**  允许子组件向父组件传递数据，并在父组件中渲染。

   **示例：**

   ```vue
   // 子组件：Alert.vue
   <template>
     <div class="alert">
       <slot name="icon"></slot>
       <slot></slot>
     </div>
   </template>

   // 父组件：App.vue
   <template>
     <Alert>
       <template #icon>
         <i class="warning icon"></i> 
       </template>
       This is an alert message.
     </Alert>
   </template>
   ```

   在这个例子中，`Alert` 组件定义了一个默认插槽和一个名为 `icon` 的具名插槽。父组件在使用 `Alert` 组件时，可以向这两个插槽传递内容。

### 动态组件 (Dynamic Components)

   - **作用：** 根据条件动态地切换不同的组件。
   - **实现：** 使用 `component` 组件，并通过 `is` 属性动态绑定要渲染的组件。

   **示例：**

   ```vue
   <template>
     <component :is="currentComponent"></component>
   </template>

   <script>
   import ComponentA from './ComponentA.vue';
   import ComponentB from './ComponentB.vue';

   export default {
     data() {
       return {
         currentComponent: 'ComponentA',
       };
     },
     components: {
       ComponentA,
       ComponentB,
     },
   };
   </script>
   ```

   在这个例子中，`currentComponent` 变量的值决定了要渲染哪个组件。

### 异步组件 (Async Components)

   - **作用：** 延迟加载组件，提高应用性能。
   - **实现：** 使用 `defineAsyncComponent` 函数定义异步组件。

   **示例：**

   ```vue
   <template>
     <component :is="asyncComponent"></component>
   </template>

   <script>
   import { defineAsyncComponent } from 'vue';

   export default {
     setup() {
       const asyncComponent = defineAsyncComponent(() =>
         import('./MyComponent.vue')
       );

       return {
         asyncComponent,
       };
     },
   };
   </script>
   ```

   在这个例子中，`MyComponent.vue` 组件只会在需要时才被加载。

## 组件的最佳实践

* **保持组件的单一职责原则:**  每个组件应该只关注一个特定的功能，避免组件过于庞大和复杂。
* **组件命名规范:**  使用清晰、语义化的名称来命名组件，例如使用 PascalCase 命名组件。
* **组件拆分和复用:**  将复杂的组件拆分成更小、更易于管理的子组件，提高代码复用率。
* **编写组件文档:**  为组件编写清晰的文档，说明组件的用途、使用方法和 API 等信息。

