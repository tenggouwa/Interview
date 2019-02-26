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

(7)Vue生命周期
---

	beforeCreate（创建前） 在数据观测和初始化事件还未开始
	created（创建后） 完成数据观测，属性和方法的运算，初始化事件，$el属性还没有显示出来
	beforeMount（载入前） 在挂载开始之前被调用，相关的render函数首次被调用。实例已完成以下的配置：编译模板，把data里面的数据和模板生成html。注意此时还没有挂载html到页面上。
	mounted（载入后） 在el 被新创建的 vm.$el 替换，并挂载到实例上去之后调用。实例已完成以下的配置：用上面编译好的html内容替换el属性指向的DOM对象。完成模板中的html渲染到html页面中。此过程中进行ajax交互。
	beforeUpdate（更新前） 在数据更新之前调用，发生在虚拟DOM重新渲染和打补丁之前。可以在该钩子中进一步地更改状态，不会触发附加的重渲染过程。
	updated（更新后） 在由于数据更改导致的虚拟DOM重新渲染和打补丁之后调用。调用时，组件DOM已经更新，所以可以执行依赖于DOM的操作。然而在大多数情况下，应该避免在此期间更改状态，因为这可能会导致更新无限循环。该钩子在服务器端渲染期间不被调用。
	beforeDestroy（销毁前） 在实例销毁之前调用。实例仍然完全可用。
	destroyed（销毁后） 在实例销毁之后调用。调用后，所有的事件监听器会被移除，所有的子实例也会被销毁。该钩子在服务器端渲染期间不被调用。

(8)VUE双向绑定原理
---

	vue实现数据双向绑定主要是：采用数据劫持结合发布者-订阅者模式的方式，通过Object.defineProperty（）来劫持各个属性的setter，getter，在数据变动时发布消息给订阅者，触发相应监听回调。当把一个普通 Javascript 对象传给 Vue 实例来作为	它的 data 选项时，Vue 将遍历它的属性，用 Object.defineProperty 将它们转为 getter/setter。用户看不到 getter/setter，但是在内部它们让 Vue 追踪依赖，在属性被访问和修改时通知变化。

	vue的数据双向绑定 将MVVM作为数据绑定的入口，整合Observer，Compile和Watcher三者，通过Observer来监听自己的model的数据变化，通过Compile来解析编译模板指令（vue中是用来解析 {{}}），最终利用watcher搭起observer和Compile之间	的通信桥梁，达到数据变化 —>视图更新；视图交互变化（input）—>数据model变更双向绑定效果。

(9)什么是vue的计算属性？
---


	在模板中放入太多的逻辑会让模板过重且难以维护，在需要对数据进行复杂处理，且可能多次使用的情况下，尽量采取计算属性的方式。好处：①使得数据处理结构清晰；②依赖于数据，数据更新，处理结果自动更新；③计算属性内部this指向vm实例；	④在template调用时，直接写计算属性名即可；⑤常用的是getter方法，获取数据，也可以使用set方法改变数据；⑥相较于methods，不管依赖的数据变不变，methods都会重新计算，但是依赖数据不变的时候computed从缓存中获取，不会重新计算。

(10)单页面应用优缺点
---

	优点：Vue 的目标是通过尽可能简单的 API 实现响应的数据绑定和组合的视图组件，核心是一个响应的数据绑定系统。MVVM、数据驱动、组件化、轻量、简洁、高效、快速、模块友好。 	缺点：不支持低版本的浏览器，最低只支持到IE9；不利于SEO的优化（如果要支持SEO，建议通过服务端来进行渲染组件）；第一次加载首页耗时相对长一些

































