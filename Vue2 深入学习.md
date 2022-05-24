# Vue2 深入学习

## 1. Vue2 基础知识

# 2. Vue2 项目总结

## 脚手架

1. npm run serve 首先执行 main.js 文件

2. Vue 利用 vue-template-compiler 插件解析 <template></template> 标签

3. render 函数作用：解析模板

4. 不同版本的 Vue 区别：

   1. vue.js 与 vue.runtime.xxx.js 的区别：

      (1). vue.js 是完整版的 Vue，包含：核心功能 + 模板解析器

      (2). vue.runtime.xxx.js 是运行版本 Vue，只包含：核心功能，没有模板解析器

   2. 因为 vue.runtime.xxx.js 没有模板解析器，所以不能使用 template 配置项，需要使用 render 函数接收到的 createElement 函数去指定具体内容

5. 挂载节点方式：

   1. el 配置项：(必须在创建 Vue 实例时进行配置)

      ```javascript
      const app = new Vue({
        el:'#app'
        router,
        store,
        render: h => h(App)
      });
      ```

   2. $mount( ) 方法：（更加灵活，可自定义挂载时机）

      ```javascript
      const app = new Vue({
        router,
        store,
        render: h => h(App)
      });
      app.$mount("#app");
      ```

6. Vue 实例与 VueComponent 实例分析：

   * 相同点：绝大部分内容两者都是一致的，比如：data、methods、computed 等
   * 区别：
     1. Vue 实例可以使用 el 等配置项，VueComponent 实例不行
     2. Vue 实例的 data 配置项可以写成对象或者函数类型（只有一个 Vue 实例），VueComponent 实例的 data 配置项必须写成函数类型（会存在多个 VueComponent 实例）
   * 分析：
     1. 组件本质是一个 VueComponent 构造函数，是 Vue.extend 生成的
     2. 组件定义简写：`const school = Vue.extend(options)` => `const school = options`
   * 联系：`VueComponent.prototype.__proto__ === Vue.prototype` 
   * 图解：