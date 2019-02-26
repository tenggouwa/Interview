框架整理
===

(1) MVC   Model、View、Controller   后两者耦合性强  
---

	MVC允许在不改变视图的情况下改变视图对用户输入的响应方式，用户对View的操作交给了Controller处理，在Controller中响应View的事件调用Model的接口对数据进行操作，一旦Model发生变化便通知相关视图进行更新。

(2) MVVM  Model、View、ViewModel
---

	这里的html部分相当于View层，可以看到这里的View通过通过模板语法来声明式的将数据渲染进DOM元素，当ViewModel对Model进行更新时，通过数据绑定更新到View。

(3)MVVM与MVC最大的区别就是
---

	MVVM实现了View和Model的自动同步，也就是当Model的属性改变时，我们不用再自己手动操作Dom元素，来改变View的显示，而是改变属性后该属性对应View层显示会自动改变。非常的神奇~

(4)双向数据绑定 (VUE ，Angular,  KnockoutJS)
---

	VUE:              数据劫持        对Model进行劫持，当数据发生变化的时候，触发劫持时绑定的方法，对视图View进行更新    使用的是 —— 数据劫持(Object.defineProperty,proxy) + 发布订阅
	Angular:        脏值检查        当发生了某种事件，检查新的数据结构和之前的是否变动，来判断是否要更新View
	KnockoutJS: 发布订阅模式  数据上绑定订阅器，View上绑定发布器，

(5)单向数据流
---

	state：驱动应用的数据源。view：以声明方式将 state 映射到视图 。 actions：响应在 view 上的用户输入导致的状态变化

(6)双向数据流
---

	双向数据绑定==带来双向数据流。数据（state）和视图（View）之间的双向绑定。
	ng 里的 ng-model 和 vue 里的 v-model。
	说到底就是 （value 的单向绑定 + onChange 事件侦听）的一个语法糖，你如果不想用 v-model，像 React 那样处理也是完全可以的。

(7)单页面应用优缺点
---

	优点：Vue 的目标是通过尽可能简单的 API 实现响应的数据绑定和组合的视图组件，核心是一个响应的数据绑定系统。MVVM、数据驱动、组件化、轻量、简洁、高效、快速、模块友好。 	缺点：不支持低版本的浏览器，最低只支持到IE9；不利于SEO的优化（如果要支持SEO，建议通过服务端来进行渲染组件）；第一次加载首页耗时相对长一些

































