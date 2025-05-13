- [Vue2](#vue2)
  - [1. 生命周期](#1-生命周期)
    - [1.1 生命周期有哪些？发送请求在 created 还是 mounted？](#11-生命周期有哪些发送请求在-created-还是-mounted)
    - [1.2 为什么发送请求不在 beforeCreate 里？beforeCreate 和 created 有什么区别？](#12-为什么发送请求不在-beforecreate-里beforecreate-和-created-有什么区别)
    - [1.3 在 created 中如何获取 dom](#13-在-created-中如何获取-dom)
    - [1.4 一旦进入组件会执行哪些生命周期？](#14-一旦进入组件会执行哪些生命周期)
    - [1.5 第二次或者第 N 次进去组件会执行哪些生命周期？](#15-第二次或者第-n-次进去组件会执行哪些生命周期)
    - [1.6 父组件引入子组件，那么生命周期执行的顺序是？](#16-父组件引入子组件那么生命周期执行的顺序是)
    - [1.7 加入 keep-alive 会执行哪些生命周期？](#17-加入-keep-alive-会执行哪些生命周期)
    - [1.8 你在什么情况下用过哪些生命周期？说一说生命周期使用场景](#18-你在什么情况下用过哪些生命周期说一说生命周期使用场景)
  - [2. 组件](#2-组件)
    - [2.1 组件传值（通信）的方式](#21-组件传值通信的方式)
    - [2.2 父组件如何直接修改子组件的值](#22-父组件如何直接修改子组件的值)
    - [2.3 子组件如何直接修改父组件的值](#23-子组件如何直接修改父组件的值)
    - [2.4 如何找到父组件](#24-如何找到父组件)
    - [2.5 如何找到根组件](#25-如何找到根组件)
    - [2.6 keep-alive](#26-keep-alive)
    - [2.7 slot/插槽](#27-slot插槽)
    - [2.8 provide/inject](#28-provideinject)
    - [2.9 如何封装组件](#29-如何封装组件)
  - [3. Vuex](#3-vuex)
    - [3.1 Vuex 有哪些属性](#31-vuex-有哪些属性)
    - [3.2 Vuex 使用 state 值](#32-vuex-使用-state-值)
    - [3.3 Vuex 的 getters 值修改](#33-vuex-的-getters-值修改)
    - [3.4 Vuex 的 mutations 和 actions 区别](#34-vuex-的-mutations-和-actions-区别)
    - [3.5 Vuex 持久化存储 ：在页面使用了 state 值：1，然后把 1 修改成 2，然后刷新页面又回到了 1 为什么？](#35-vuex-持久化存储-在页面使用了-state-值1然后把-1-修改成-2然后刷新页面又回到了-1-为什么)
  - [4. 路由](#4-路由)
    - [4.1 路由的模式和区别](#41-路由的模式和区别)
    - [4.2 子路由和动态路由](#42-子路由和动态路由)
    - [4.3 路由传值](#43-路由传值)
    - [4.4 导航故障](#44-导航故障)
    - [4.5 $router和$route 区别](#45-router和route-区别)
    - [4.6 导航守卫](#46-导航守卫)
  - [5. API](#5-api)
    - [5.1 $set](#51-set)
    - [5.2 $nextTick](#52-nexttick)
    - [5.3 常用 API](#53-常用-api)
    - [5.4 数据定义在 data 的 return 内和 return 外的区别](#54-数据定义在-data-的-return-内和-return-外的区别)
    - [5.5 computed 计算属性](#55-computed-计算属性)
    - [5.6 watch](#56-watch)
    - [5.7 methods 和 computed 区别](#57-methods-和-computed-区别)
  - [6. 指令](#6-指令)
    - [6.1 如何自定义指令](#61-如何自定义指令)
    - [6.2 vue 单项绑定](#62-vue-单项绑定)
    - [6.3 v-if 和 v-for 优先级](#63-v-if-和-v-for-优先级)
  - [7. 原理](#7-原理)
    - [7.1 $nextTick 原理](#71-nexttick-原理)
    - [7.2 双向绑定原理](#72-双向绑定原理)
  - [8. axios 二次封装](#8-axios-二次封装)
- [Vue3](#vue3)
  - [1. vue2 和 vue3 的区别](#1-vue2-和-vue3-的区别)
  - [2. Vue3 用 setup 语法糖形式怎么组织代码](#2-vue3-用-setup-语法糖形式怎么组织代码)
  - [3. Vue 用 setup 语法糖形式写代码如何获取类似于 Vue2 中的 this](#3-vue-用-setup-语法糖形式写代码如何获取类似于-vue2-中的-this)
  - [4. Vue3 常用 API](#4-vue3-常用-api)
  - [5. Vue3 常用的响应式数据类型](#5-vue3-常用的响应式数据类型)
  - [6. Teleport 组件及其使用场景](#6-teleport-组件及其使用场景)

# Vue2

## 1. 生命周期

### 1.1 生命周期有哪些？发送请求在 created 还是 mounted？

Vue2.x 系统自带有 8 个

```
beforeCreate
created
beforeMount
mounted
beforeUpdate
updated
beforeDestroy
destroyed
```

发送请求在 created 还是 mounted？

这个问题具体要看项目和业务的情况了，因为组件的加载顺序是，父组件引入了子组件，那么先执行父的前 3 个生命周期，再执行子的前 4 个生命周期，那么如果我们的业务是父组件引入子组件，并且优先加载子组件的数据，那么在父组件中当前的请求要放在 mounted 中，如果当前组件没有依赖关系那么放在哪个生命周期中请求都是可以的。

### 1.2 为什么发送请求不在 beforeCreate 里？beforeCreate 和 created 有什么区别？

为什么发送请求不在 beforeCreate 里？
因为：如果请求是在 methods 封装好了，在 beforeCreate 调用的时候，beforeCreate 阶段是拿不到 methods 里面的方法的（会报错了）。

beforeCreate 和 created 有什么区别？
beforeCreate 没有$data
created中有$data
created 是可以拿到 methods 的方法的
beforeCreate 拿不到 methods 的方法

### 1.3 在 created 中如何获取 dom

- 只要写异步代码，获取 dom 是在异步中获取的，就可以了。例如：setTimeout、请求、Promise.xxx()等等...
- 使用 vue 系统内置的 this.$nextTick

### 1.4 一旦进入组件会执行哪些生命周期？

```
beforeCreate
created
beforeMount
mounted
```

### 1.5 第二次或者第 N 次进去组件会执行哪些生命周期？

如果当前组件加入了 keep-alive，只会执行一个生命周期

```
activated
```

如果没有加入 keep-alive

```
beforeCreate
created
beforeMount
mounted
```

### 1.6 父组件引入子组件，那么生命周期执行的顺序是？

```
父：beforeCreate、created、beforeMount
子：beforeCreate、created、beforeMount、mounted
...
父：mounted
```

### 1.7 加入 keep-alive 会执行哪些生命周期？

如果使用了 keep-alive 组件，当前的组件会额外增加 2 个生命周期（系统 8 + 2 ）

```
activated
deactivated
```

如果当前组件加入了 keep-alive 第一次进入这个组件会执行 5 个生命周期

```
beforeCreate
created
beforeMount
mounted
activated
```

### 1.8 你在什么情况下用过哪些生命周期？说一说生命周期使用场景

```
created    ===> 单组件请求
mounted    ===> 同步可以获取dom，如果先子组件请求后父组件请求
activated  ===> 判断id是否相等，如果不相同发起请求
destroyed  ===> 关闭页面记录视频播放的时间,初始化的时候从上一次的历史开始播放
```

## 2. 组件

### 2.1 组件传值（通信）的方式

```
父传后代 ( 后代拿到了父的数据 )
1. 父组件引入子组件，绑定数据
	 <List :str1='str1'></List>
	子组件通过props来接收
	props:{
		str1:{
			type:String,
			default:''
		}
	}
	***这种方式父传子很方便，但是父传给孙子辈分的组件就很麻烦（父=》子=》孙）
	这种方式：子不能直接修改父组件的数据

2. 子组件直接使用父组件的数据
	子组件通过：this.$parent.xxx使用父组件的数据
	这种方式：子可以直接修改父组件的数据

3. 依赖注入
	优势：父组件可以直接向某个后代组件传值(不让一级一级的传递)
```

```
后代传父 （父拿到了后代的数据）
1. 子组件传值给父组件
	子组件定义自定义事件 this.$emit
2. 父组件直接拿到子组件的数据
	<List ref='child'></List>
	this.$refs.child
```

```
平辈之间的传值 ( 兄弟可以拿到数据 )

通过新建bus.js文件来做
```

### 2.2 父组件如何直接修改子组件的值

```
<List ref='child'></List>
this.$refs.child.xxx = 'yyyy';
```

### 2.3 子组件如何直接修改父组件的值

```
子组件中可以使用：this.$parent.xxx去修改
```

### 2.4 如何找到父组件

```
this.$parent
```

### 2.5 如何找到根组件

```
this.$root
```

### 2.6 keep-alive

```
keep-alive的作用是什么：缓存当前组件
```

### 2.7 slot/插槽

- 匿名插槽：插槽没有名字
- 具名插槽：插槽有名字
- 作用域插槽：传值

### 2.8 provide/inject

```
provide/inject ===> 依赖注入
```

### 2.9 如何封装组件

```
组件一定要难点，涉及的知识点：slot、组件通信...
```

## 3. Vuex

### 3.1 Vuex 有哪些属性

- state：全局共享属性
- getters：针对 state 数据进行二次运算
- mutations：存放同步方法
- actions：存放异步方法，提交 mutations
- modules：把 vuex 进行模块之间的划分

### 3.2 Vuex 使用 state 值

1. this.$store.state.xxx
2. 辅助函数：mapState

以上俩种方式都可以拿到 state 的值，那么区别是什么？

1. 使用 this.$store.state.xxx 可以直接修改 vuex 的 state 数据
2. 使用辅助函数的形式，是不可以修改的

### 3.3 Vuex 的 getters 值修改

面试官可能会这样问：组件使用了 getters 中的内容，组件使用采用 v-model 的形式会发生什么？

```
getters是不可以修改的
```

### 3.4 Vuex 的 mutations 和 actions 区别

```
相同点：mutations和actions都是来存放全局方法的，这个全局方法return的值拿不到
```

```
区别：
	mutations ==》 同步
	actions   ==》 返回的是一个Promise对象，他可以执行相关异步操作

mutations是来修改state的值的，actions的作用是来提交mutations
```

### 3.5 Vuex 持久化存储 ：在页面使用了 state 值：1，然后把 1 修改成 2，然后刷新页面又回到了 1 为什么？

```
Vuex本身不是持久化存储的数据。Vuex是一个状态管理仓库（state：全局属性）==》就是存放全局属性的地方。
```

```
实现持久化存储：1. 自己写localStorage  2. 使用vuex-persistedstate插件
```

```
插件使用方式：https://www.xuexiluxian.cn/blog/detail/dae4073b07144d3c9abb3e2cc8495922
```

## 4. 路由

### 4.1 路由的模式和区别

```
路由的模式：history、hash
```

```
区别：
1. 关于找不到当前页面发送请求的问题
	history会给后端发送一次请求而hash不会
2. 关于项目打包前端自测问题
	hash是可以看到内容的
	history默认情况是看不到内容的
3. 关于表象不同
	hash:#
	history:/
```

### 4.2 子路由和动态路由

### 4.3 路由传值

### 4.4 导航故障

```
官网说明：https://v3.router.vuejs.org/zh/guide/advanced/navigation-failures.html#%E6%A3%80%E6%B5%8B%E5%AF%BC%E8%88%AA%E6%95%85%E9%9A%9C
```

解决：

```
import VueRouter from 'vue-router'
const routerPush = VueRouter.prototype.push
VueRouter.prototype.push = function (location) {
  return routerPush.call(this, location).catch(error => error)
}
```

### 4.5 $router和$route 区别

- $router 不仅包含当前路由还包含整个路由的属性和方法
- $route 包含当前路由对象

### 4.6 导航守卫

1. 全局守卫

- beforeEach 路由进入之前
  - afterEach 路由进入之后

2. 路由独享守卫

- beforeEnter 路由进入之前

3. 组件内守卫

- beforeRouteEnter 路由进入之前
  - beforeRouteUpdate 路由更新之前
  - beforeRouteLeave 路由离开之前

## 5. API

### 5.1 $set

```
面试官：你有没有碰到过，数据更新视图没有更新的问题==》$set
```

```
this.$set(target,key,修改后的值)
```

### 5.2 $nextTick

```
$nextTick返回的参数[函数]，是一个异步的。功能：获取更新后的dom

源码|原理：
$nextTick( callback ){
		return Promise.resolve().then(()=>{
			callback();
		})
}
```

### 5.3 常用 API

| API       | 作用                                     |
| --------- | ---------------------------------------- |
| $refs     | 获取 DOM                                 |
| $el       | 获取当前组件的根节点                     |
| $data     | 获取当前组件 data 数据                   |
| $children | 获取到当前组件的所有子组件               |
| $parent   | 获取当前组件的父组件，如果找不到返回自身 |
| $root     | 获取根组件                               |

### 5.4 数据定义在 data 的 return 内和 return 外的区别

- return 外：单纯修改这个数据是不可以修改的，因为没有被 get/set
- reutnr 内：是可以修改的

### 5.5 computed 计算属性

- computed 计算属性的结果值，可以修改吗？可以，需要通过 get/set 写法
- 当前组件 v-model 绑定的值是 computed 来的，那么可以修改吗？可以的，需要通过 get/set 写法

### 5.6 watch

```
watch:{
  obj:{
    handler(newVal,oldVal){
      console.log( 'obj',newVal , oldVal )
    },
    immediate:true,
    deep:true
  },
}
```

### 5.7 methods 和 computed 区别

```
computed是有缓存机制的，methods是没有缓存机制的（调用几次执行几次）
```

## 6. 指令

### 6.1 如何自定义指令

```
全局：
Vue.directive('demo', {
  inserted: function (a,b,c) {
    console.log( a,b,c );
  }
})
```

```
局部：
<script>
export default {
  directives: {
    demo: {
      bind: function (el) {
        console.log( 1 )
      }
    }
  }
}
</script>
```

### 6.2 vue 单项绑定

单项绑定：v-bind，双向绑定：v-model

### 6.3 v-if 和 v-for 优先级

- vue2 中：v-for > v-if
- vue3 中：v-if > v-for

## 7. 原理

### 7.1 $nextTick 原理

```
$nextTick功能：获取更新后的dom
```

```
$nextTick( callback ){

		return Promise.resolve().then(()=>{
			callback();
		})

}
```

### 7.2 双向绑定原理

## 8. axios 二次封装

# Vue3

## 1. vue2 和 vue3 的区别

- 双向绑定的原理不同
  - Vue2 使用`Object.defineProperty()`，后添加的属性劫持不到
  - Vue3 使用`Proxy`，后添加的属性也可以劫持到，不需要循环
- Vue3 中没有`$set`，因为`Proxy`不需要
- 代码写法不同
  - Vue2 是选项式 API
  - Vue3 可以向下兼容（选项式 API），也可以组合式 API 或者 setup 语法糖形式
- v-if 和 v-for 的优先级不同
  - vue2 中：v-for > v-if
  - vue3 中：v-if > v-for
- $ref和$children 不同

## 2. Vue3 用 setup 语法糖形式怎么组织代码

说明：hooks（就是函数式），主要让功能模块细分（提升项目的维护性）
解决问题：<script setup>
//代码==》比较乱
</script>
面试题：你们 vue3 写代码的方式 ==〉setup 形式
解决：hooks

## 3. Vue 用 setup 语法糖形式写代码如何获取类似于 Vue2 中的 this

```js
import { getCurrentInstance } from "vue";
let app = getCurrentInstance();
console.log(app.appContext.app.config.globalProperties.$loading);
```

## 4. Vue3 常用 API

1. createApp 创建一个应用实例

- 等于 Vue2 中的`new Vue()`
  - 使用场景：写插件，封装全局组件时会使用

2. provide/inject 依赖注入

- 传值，用于祖孙组件间通信
  - 使用场景：跨级组件间通信（使用 props 逐级传递比较麻烦）
  - 缺点：不好维护和查询数据来源

3. directive 自定义指令

- 使用场景：后台管理系统中的按钮权限控制（一个用户拥有某些权限，但是只能查看和修改，不能删除）

4. mixin 全局混入 局部

- 使用场景：可以添加生命周期
  - 缺点：不好维护和查询数据来源

5. app.config.globalProperties

- 作用：获取 Vue 这个全局对象的属性和方法
  - 使用场景：自己封装插件的时候需要把方法添加到对象中

6. nextTick 等待下一次 DOM 更新

- 原理：nextTick 返回一个 Promise，回调函数放在 Promise 中，异步执行
  - 场景：就是把 DOM 要更新，因为 Vue 是数据驱动 DOM，所以数据的赋值要在 nextTick 进行

7. ref/reactive 定义响应式数据
8. computed 计算属性，有缓存
9. watch 监听（Vue3 不需要深度监听）
10. markRaw 不被`Proxy`代理，说白了就是静态的数据
11. defineProps 父组件传递的值，子组件使用 setup 的形式时需要用 defineProps 接收
12. defineEmits 当前组件使用 setup 形式时自定义事件需要用 defineEmits
13. slot 匿名插槽、具名插槽、作用域插槽

- 使用场景：后台管理系统，左侧是固定菜单，右侧是不固定内容，那么右侧就是 slot

## 5. Vue3 常用的响应式数据类型

- ref 基本类型
- reactive 复杂类型
- toRef 解构某一个值
- toRefs 解构多个值

## 6. Teleport 组件及其使用场景

- Teleport 组件是一个传送门
- 假如自己写弹出框，需要在页面中居中位置显示，不受当前组件的限制，可以把盒子传送到 body 中
