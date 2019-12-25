React https://segmentfault.com/a/1190000016885832?utm_source=tag-newest
===

(1)React组件生命周期
---

    1、getDefaultProps  设置默认的props，也可以用dufaultProps设置组件的默认属性.
    2、getInitialState  在使用es6的class语法时是没有这个钩子函数的，可以直接在constructor中定义this.state。此时可以访问this.props
    3、componentWillMount  组件初始化时只调用，以后组件更新不调用，整个生命周期只调用一次，此时可以修改state。
    4、render  react最重要的步骤，创建虚拟dom，进行diff算法，更新dom树都在此进行。此时就不能更改state了。
    5、componentDidMount  组件渲染之后调用，只调用一次。
    6、componentWillReceiveProps(nextProps)  组件初始化时不调用，组件接受新的props时调用。
    7、shouldComponentUpdate(nextProps, nextState)  react性能优化非常重要的一环。组件接受新的state或者props时调用，我们可以设置在此对比前后两个props和state是否相同，如果相同则返回false阻止更新，因为相同的属性状态一定会生成相同的dom树，这样就不需要创造新的dom树和旧的dom树进行diff算法对比，节省大量性能，尤其是在dom结构复杂的时候，这里是不能调用setState的，因为会导致死循环。
    8、componentWillUpdate(nextProps, nextState)  组件初始化时不调用，只有在组件将要更新时才调用，此时可以修改state
    9、componentDidUpdate()  组件初始化时不调用，组件更新完成后调用，此时可以获取dom节点。
    10、componentWillUnmount()  组件将要卸载时调用，一些事件监听和定时器需要在此时清除。
    
(2)React整体思想
---
    UI = f(data)

(3)PureComponent https://segmentfault.com/a/1190000014979065
---
    提供一个shouldComponentUpdate
    在无状态组件开发中，可以使用React.memo来代替

(4)高阶组件
---
    它接受至少一个 React 组件为参数，并且能够返回一个全新的 React 组件作为结果,
    最巧妙的就是可以进行链式调用
    const SuperX = withThree(withTwo(withOne(X)));

(5)调用setState之后发生了什么？
---
    在代码中调用 setState 函数之后，React 会将传入的参数对象与组件当前的状态合并，然后触发所谓的调和过程（Reconciliation）。经过调和过程，React 会以相对高效的方式根据新的状态构建 React 元素树并且着手重新渲染整个 UI 界面。在 React 得到元素树之后，React 会自动计算出新的树与老树的节点差异，然后根据差异对界面进行最小化重渲染。在差异计算算法中，React 能够相对精确地知道哪些位置发生了改变以及应该如何改变，这就保证了按需更新，而不是全部重新渲染。
(6)为什么虚拟 dom 会提高性能?
---
    虚拟 dom 相当于在 js 和真实 dom 中间加了一个缓存，利用 dom diff 算法避免了没有必要的 dom 操作，从而提高性能。

    用 JavaScript 对象结构表示 DOM 树的结构；然后用这个树构建一个真正的 DOM 树，插到文档当中当状态变更的时候，重新构造一棵新的对象树。然后用新的树和旧的树进行比较，记录两棵树差异把 2 所记录的差异应用到步骤 1 所构建的真正的 DOM 树上，视图就更新了
(7)react-diff原理？
---
    把树形结构按照层级分解，只比较同级元素。
    给列表结构的每个单元添加唯一的 key 属性，方便比较。
    React 只会匹配相同 class 的 component（这里面的 class 指的是组件的名字）
    合并操作，调用 component 的 setState 方法的时候, React 将其标记为 dirty.到每一个事件循环结束, React 检查所有标记 dirty 的 component 重新绘制.
    选择性子树渲染。开发人员可以重写 shouldComponentUpdate 提高 diff 的性能。
(8)state和props有什么不同之处？
---
    State 是一种数据结构，用于组件挂载时所需数据的默认值。State 可能会随着时间的推移而发生突变，但多数时候是作为用户事件行为的结果。
    Props(properties 的简写)则是组件的配置。props 由父组件传递给子组件，并且就子组件而言，props 是不可变的(immutable)。组件不能改变自身的 props，但是可以把其子组件的 props 放在一起(统一管理)。Props 也不仅仅是数据--回调函数也可以通过 props 传递。