---
layout: post
title: "vue组件"
subtitle: "vue组件也不懂用过多少回了,这里来看看能不能抠点细节"
date: 2020-05-31 01:20:32
author: "Aurora"
tag:
  - javascript
  - vue
---

## component

### 基础

可以将组件进行任意次数的复用

#### data

组件中 data 必须是一个函数

#### prop

通过 Prop 向子组件传递数据

HTML 中的 attribute 名是大小写不敏感的，所以浏览器会把所有大写字符解释为小写字符。这意味着当你使用 DOM 中的模板时，camelCase (驼峰命名法) 的 prop 名需要使用其等价的 kebab-case (短横线分隔命名) 命名

可以以对象形式列出 prop，这些 property 的名称和值分别是 prop 各自的名称和类型

**Number**:通过 v-bind 可以告诉特性这是一个 JavaScript 表达式而不是一个字符串
**Boolean**: 包含该 prop 没有值的情况在内，都意味着 `true`,即便 `false` 是静态的，我们仍然需要 `v-bind` 来告诉 Vue
**Array**: 即便数组是静态的，我们仍然需要 `v-bind` 来告诉 Vue
**Object**: 即便对象是静态的，我们仍然需要 `v-bind` 来告诉 Vue

如果你想要将一个对象的所有 property 都作为 prop 传入，你可以使用不带参数的 v-bind (取代 v-bind:prop-name)

##### 单向数据流

所有的 prop 都使得其父子 prop 之间形成了一个单向下行绑定：父级 prop 的更新会向下流动到子组件中，但是反过来则不行。每次父级组件发生变更时，子组件中所有的 prop 都将会刷新为最新的值。这意味着你不应该在一个子组件内部改变 prop。

有两种常见的试图变更一个 prop 的情形：

1. 这个 prop 用来传递一个初始值；这个子组件接下来希望将其作为一个本地的 prop 数据来使用。在这种情况下，最好定义一个本地的 data property 并将这个 prop 用作其初始值
2. 这个 prop 以一种原始的值传入且需要进行转换。在这种情况下，最好使用这个 prop 的值来定义一个计算属性

##### 验证

可以为组件的 prop 指定验证要求

type 可以是下列原生构造函数中的一个：String、Number、Boolean、Array、Object、Date、Function、Symbol,额外的，type 还可以是一个自定义的构造函数，并且通过 instanceof 来进行检查确认。

##### 非 Prop 的 Attribute

一个非 prop 的 attribute 是指传向一个组件，但是该组件并没有相应 prop 定义的 attribute

组件可以接受一个未定义 prop 的特性，会自动添加到组件的根元素上。

对于绝大多数 attribute 来说，从外部提供给组件的值会替换掉组件内部设置好的值。所以如果传入 type="text" 就会替换掉 type="date" 并把它破坏！庆幸的是，class 和 style attribute 会稍微智能一些，即两边的值会被合并起来，从而得到最终的值

如果你不希望组件的根元素继承 attribute，你可以在组件的选项中设置 inheritAttrs: false

> 注意 inheritAttrs: false 选项不会影响 style 和 class 的绑定。

##### vm.\$attrs

\$attrs: { [key: string]: string }

包含了父作用域中不作为 prop 被识别 (且获取) 的 attribute 绑定 (class 和 style 除外)。当一个组件没有声明任何 prop 时，这里会包含所有父作用域的绑定 (class 和 style 除外)，并且可以通过 v-bind="\$attrs" 传入内部组件——在创建高级别的组件时非常有用。

\$attrs property ，该 property 包含了传递给一个组件的 attribute 名和 attribute 值

### 事件

父级组件可以像处理 native DOM 事件一样通过 v-on 监听子组件实例的任意事件,同时子组件可以通过调用内建的 \$emit 方法并传入事件名称来触发一个事件

有的时候用一个事件来抛出一个特定的值是非常有用的,这时可以使用 \$emit 的第二个参数来提供这个值

##### 命名

推荐始终使用 kebab-case 的事件名

##### v-model

自定义事件也可以用于创建支持 v-model 的自定义输入组件

一个组件上的 v-model 默认会利用名为 value 的 prop 和名为 input 的事件

可以通过设置 model 来处理一些比较特殊的双向绑定:

```javascript
Vue.component("base-checkbox", {
  model: {
    prop: "checked",
    event: "change",
  },
  props: {
    checked: Boolean,
  },
  template: `
    <input
      type="checkbox"
      v-bind:checked="checked"
      v-on:change="$emit('change', $event.target.checked)"
    >
  `,
});
```

可能想要在一个组件的根元素上直接监听一个原生事件。这时，你可以使用 v-on 的 .native 修饰符,
但组件可能做了重构,根元素不是想要的元素,这时，父级的 .native 监听器将静默失败

为了解决这个问题，Vue 提供了一个 \$listeners property，它是一个对象，里面包含了作用在这个组件上的所有监听器。

##### vm.\$listeners

\$listeners: { [key: string]: Function | Array\<Function> }

包含了父作用域中的 (不含 .native 修饰器的) v-on 事件监听器。它可以通过 v-on="\$listeners" 传入内部组件——在创建更高层次的组件时非常有用。

##### 双向绑定

在有些情况下，我们可能需要对一个 prop 进行“双向绑定”,推荐在子组件中以 update:myPropName 的模式触发事件取而代之。父组件可以监听那个事件,以方法的形式更新数据

除事件外父组件可以用 .sync 修饰一个用来绑定的字段,来实现双向绑定

> 注意带有 .sync 修饰符的 v-bind 不能和表达式一起使用 (例如 v-bind:title.sync=”doc.title + ‘!’” 是无效的)。取而代之的是，你只能提供你想要绑定的 property 名，类似 v-model。

当我们用一个对象同时设置多个 prop 的时候，也可以将这个 .sync 修饰符和整个 v-bind 配合使用

#### 插槽

通过插槽分发内容

> slot 和 slot-scope 这两个目前已被废弃但未被移除

##### 作用域

父级模板里的所有内容都是在父级作用域中编译的；子模板里的所有内容都是在子作用域中编译的。

##### 具名插槽

有时我们需要多个插槽,对于这样的情况，\<slot> 元素有一个特殊的 attribute：name。这个 attribute 可以用来定义额外的插槽

在向具名插槽提供内容的时候，我们可以在一个 \<template> 元素上使用 v-slot 指令，并以 v-slot 的参数的形式提供其名称

#### is

可以通过 Vue 的 \<component> 元素加一个特殊的 is attribute 来实现

```javascript
<component v-bind:is="currentTabComponent"></component>
```

在上述示例中，currentTabComponent 可以包括

- 已注册组件的名字，或
- 一个组件的选项对象

这个 attribute 可以用于常规 HTML 元素，但这些元素将被视为组件，这意味着所有的 attribute 都会作为 DOM attribute 被绑定。对于像 value 这样的 property，若想让其如预期般工作，你需要使用 .prop 修饰器。

有些元素，诸如 \<li>、\<tr> 和 \<option>，只能出现在其它某些特定的元素内部。这个特殊的 is attribute 给了我们一个变通的办法

需要注意的是如果我们从以下来源使用模板的话，这条限制是不存在的：

- 字符串 (例如：template: '...')
- 单文件组件 (.vue)
- \<script type="text/x-template">

### next

#### 全局注册

`Vue.component('my-component-name', { /* ... */ })`

你给予组件的名字可能依赖于你打算拿它来做什么。当直接在 DOM 中使用一个组件 (而不是在字符串模板或单文件组件) 的时候，我们强烈推荐遵循 W3C 规范中的自定义组件名 (字母全小写且必须包含一个连字符)。这会帮助你避免和当前以及未来的 HTML 元素相冲突。

全局注册的行为必须在根 Vue 实例 (通过 new Vue) 创建之前发生

#### 局部注册

components: object

`components` 选项中定义你想要使用的组件

> 局部注册的组件在其子组件中不可用
