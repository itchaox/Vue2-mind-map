# Vue2 风格指南

### 前提：整理自 [( Vue2 官网的风格指南 )](https://cn.vuejs.org/v2/style-guide/)

## 1. 必要规则（避免错误）

### 1.1 组件名为多个单词

### 1.2 组件数据为一个函数

### 1.3 Prop 定义尽量详细，至少需要指定其类型

### 1.4 为 v-for 设置 key

* 且 key 尽量是类似 id 这样唯一的属性值（使用 diff 算法，提高效率）

### 1.5 避免 v-if 和 v-for 一起使用

* 问题：`v-for` 比 `v-if` 具有更高的优先级，如果一起使用则在 `v-for` 遍历的时候，会多次执行 `v-if` 判断，降低性能
* 解决方案：
  1. 用计算属性过滤数组，将过滤后的新数组再进行 `v-for` 循环
  2. 将 `v-if` 放在 `v-for` 的外层进行判断，先判断是否为 true ，如果为 true 则进行后续 `v-for` 遍历操作

### 1.6 为组件样式设置作用域（类似 scoped 属性 等）

## 2. 强烈推荐规则（增加可读性）

### 2.1 单文件组件文件名的大小写

* 建议：始终是单词大小写开头（PascalCase），或始终是横线连接（kebab-case）
* 示例：
  1. 大小写开头：`MyComponent.vue`
  2. 横线连接：`my-component.vue`

### 2.2 紧密耦合的组件名

* 建议：和父组件紧密耦合的子组件应该以父组件名作为前缀命名

* 好例子：

  ```javascript
  components/
  |- TodoList.vue
  |- TodoListItem.vue
  |- TodoListItemButton.vue
  
  components/
  |- SearchSidebar.vue
  |- SearchSidebarNavigation.vue
  ```

### 2.3 组件名中的单词顺序

* 建议：组件名应该以高级别的 (通常是一般化描述的) 单词开头，以描述性的修饰词结尾

* 好例子：

  ```javascript
  components/
  |- SearchButtonClear.vue
  |- SearchButtonRun.vue
  |- SettingsCheckboxTerms.vue
  |- SettingsCheckboxLaunchOnStartup.vue
  ```

### 2.4 自闭合组件

* 建议：在单文件组件、字符串模板和 JSX 中没有内容的组件应该是自闭合的 — 但在 DOM 模板里永远不要这样做

* 好例子：

  ```javascript
  <!-- 在单文件组件、字符串模板和 JSX 中 -->
  <MyComponent/>
      
  <!-- 在 DOM 模板中 -->
  <my-component></my-component>
  ```

### 2.5 模板中的组件名大小写

* 建议：对于绝大多数项目来说，在单文件组件和字符串模板中组件名应该总是 PascalCase 的 — 但是在 DOM 模板中总是 kebab-case

* 好例子：

  ```javascript
  <!-- 在单文件组件和字符串模板中 -->
  <MyComponent/>
  <!-- 在 DOM 模板中 -->
  <my-component></my-component>
  
  或者
  <!-- 在所有地方 -->
  <my-component></my-component>
  ```

### 2.6 JS/JSX 中的组件名大小写

* 建议：JS / JSX 中的组件名应该始终是 PascalCase 的，尽管在较为简单的应用中只使用 `Vue.component` 进行全局组件注册时，可以使用 kebab-case 字符串

* 好例子：

  ```javascript
  Vue.component('MyComponent', {
    // ...
  })
  
  Vue.component('my-component', {
    // ...
  })
  
  import MyComponent from './MyComponent.vue'
  
  export default {
    name: 'MyComponent',
    // ...
  }
  ```

### 2.7 完整单词的组件名

* 建议：组件名应该倾向于完整单词而不是缩写

* 原因：编辑器中的自动补全已经让书写长命名的代价非常之低了，而其带来的明确性却是非常宝贵的。不常用的缩写尤其应该避免

* 好例子：

  ```javascript
  components/
  |- StudentDashboardSettings.vue
  |- UserProfileOptions.vue
  ```

### 2.8 Prop 名大小写

* 建议：在声明 prop 的时候，其命名应该始终使用 camelCase，而在模板和 JSX 中应该始终使用 kebab-case

* 原因：我们单纯的遵循每个语言的约定。在 JavaScript 中更自然的是 camelCase。而在 HTML 中则是 kebab-case

* 好例子：

  ```javascript
  props: {
    greetingText: String
  }
  
  <WelcomeMessage greeting-text="hi"/>
  ```

### 2.9 多个 attribute  的元素

* 建议：多个 attribute 的元素应该分多行编写，每个 attribute 一行

* 好例子：

  ```javascript
  <img
    src="https://vuejs.org/images/logo.png"
    alt="Vue Logo"
  >
        
  <MyComponent
    foo="a"
    bar="b"
    baz="c"
  />
  ```

### 2.10 模板中简单的表达式

* 建议：组件模板应该只包含简单的表达式，复杂的表达式则应该重构为计算属性或方法

* 原因：复杂表达式会让你的模板变得不那么声明式。我们应该尽量描述应该出现的*是什么*，而非*如何*计算那个值。而且计算属性和方法使得代码可以重用

* 好例子：

  ```javascript
  <!-- 在模板中 -->
  {{ normalizedFullName }}
  
  // 复杂表达式已经移入一个计算属性
  computed: {
    normalizedFullName: function () {
      return this.fullName.split(' ').map(function (word) {
        return word[0].toUpperCase() + word.slice(1)
      }).join(' ')
    }
  }
  ```

### 2.11 简单的计算属性

* 建议：应该把复杂计算属性分割为尽可能多的更简单的计算属性

* 好例子：

  ```javascript
  computed: {
    basePrice: function () {
      return this.manufactureCost / (1 - this.profitMargin)
    },
        
    discount: function () {
      return this.basePrice * (this.discountPercent || 0)
    },
        
    finalPrice: function () {
      return this.basePrice - this.discount
    }
  }
  ```

### 2.12 带引号的 attribute 值

* 建议：非空 HTML attribute 值应该始终带引号 (单引号或双引号，以 JS 中未使用的为准)

* 好例子：

  ```javascript
  <input type="text">
      
  <AppSidebar :style="{ width: sidebarWidth + 'px' }">
  ```

### 2.13 指令缩写

* 建议：指令缩写 (用 `:` 表示 `v-bind:`、用 `@` 表示 `v-on:` 和用 `#` 表示 `v-slot:`) 应该要么都用要么都不用

* 好例子：

  ```javascript
  <input
    :value="newTodoText"
    :placeholder="newTodoInstructions"
  >
  
  <input
    @input="onInput"
    @focus="onFocus"
  >
  
  <template #header>
    <h1>Here might be a page title</h1>
  </template>
  ```

## 3. 推荐规则（将选择和认知成本最小化）



