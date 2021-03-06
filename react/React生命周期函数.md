## 总结

* 当props或者state被修改时，就会引发组件的更新过程
* 只有render和shouldComponentUpdate需要返回结果
* 不建议在 getDefaultProps、getInitialState、shouldComponentUpdate、componentWillUpdate、render 和 componentWillUnmount 中调用 setState，特别注意：不能在 shouldComponentUpdate 和 componentWillUpdate中调用 setState，会导致循环调用。
* setState 会先进行 _pendingState 更新队列的合并操作，不会立刻 reRender，因此是异步操作，且通过判断状态（MOUNTING、RECEIVE_PROPS）来控制 reRender 的时机



## getDefaultProps

* object getDefaultProps()
* 执行过一次后，被创建的类会有缓存，映射的值会存在this.props,前提是这个prop不是父组件指定的
* 这个方法在对象被创建之前执行，因此不能在方法内调用this.props
* 注意任何getDefaultProps()返回的对象在实例中共享，不是复制

## getInitialState

* object getInitialState()
* 控件加载之前执行，返回值会被用于state的初始化值

## componentWillMount

* void componentWillMount()
* 执行一次，在初始化render之前执行
* 在这个方法内调用setState，render()知道state发生变化，并且只执行一次

## render

* ReactElement render()
* 决定了组件该渲染什么
* 调用render()
* 调用render()方法时，首先检查this.props和this.state返回一个子元素，子元素可以是DOM组件或者其他自定义复合控件的虚拟实现
* 如果不想渲染可以返回null或者false，这种场景下，react渲染一个`<noscript>`标签
* 当返回null或者false时，ReactDOM.findDOMNode(this)返回null
* 不要在这个方法里初始化组件的state，每次执行时返回相同的值
* 这个方法不会读写DOM或者与服务器交互，如果必须如服务器交互，在componentDidMount()方法中实现或者其他生命周期的方法中实现，保持render()方法纯净使得服务器更准确，组件更简单

## componentDidMount

* void componentDidMount()
* 在初始化render之后只执行一次
* 从这个函数开始，可以访问任何组件，可以和 js 其他框架交互，可以设置计时 setTimeout 或者 setInterval，或者发起网络请求
* componentDidMount()方法中的子组件在父组件之前执行

## componentWillReceiveProps

从这个生命周期开始触发组件的更新过程

* void componentWillReceiveProps(object nextProps)
* 一个组件要从父组件接受参数，只要父组件的render函数被重新调用，在render函数里面渲染的子组件就会经历更新过程，不管父传给子的props有没有改变
* 这个函数适合根据新的props值（也就是参数nextProps）来计算出是不是要更新内部状态state
* 这个生命周期有必要把传入的参数nextProps和this.props作必要的对比，只有两者有变化时才有必要通过调用this.setState()来更新组件的状态
* 旧的属性还是可以通过this.props来获取,
* 这里调用更新状态是安全的，并不会触发额外的render调用

## shouldComponentUpdate

* boolean shouldComponentUpdate(object nextProps, object nextState）
* 决定了一个组件什么时候不需要渲染
* 在第二个render之前执行
* 父组件render和this.setState()都会经过的生命周期函数
    * nextProps: 父组件render时是否渲染
    * nextState：调用this.setState()时是否渲染
* 当组件比较多时，使用这个方法能有效提高应用性能
    * 返回true, 则会执行render()方法
    * 返回false, 不会执行render()方法，componentWillUpdate和componentDidUpdate方法也不会被调用
* 默认情况下，shouldComponentUpdate方法返回true防止state快速变化时的问题，
* 但是如果·state不变，props只读，可以直接覆盖shouldComponentUpdate用于比较props和state的变化，决定UI是否更新

## componentWillUpdate（删除）

* void componentWillUpdate(object nextProps, object nextState)
* 当props和state发生变化时执行
* 在这个函数里面，就不能使用this.setState来修改状态
* 这个函数调用之后，就会把nextProps和nextState分别设置到this.props和this.state中。紧接着这个函数，就会调用render()来更新界面了

## componentDidUpdate

* void componentDidUpdate(object prevProps, object prevState)
* 组件更新结束之后执行，在初始化render时不执行

## componentWillUnmount

* void componentWillUnmount()
* 当组件要被从界面上移除时调用
* 在这个函数中，可以做一些组件相关的清理工作，例如取消计时器、网络请求等

## componentDidCatch（err, info)

* 组件内的异常有可能会影响到 React 的内部状态，进而导致下一轮渲染时出现未知错误。
* 这些组件内的异常往往也是由应用代码本身抛出，在之前版本的 React 更多的是交托给了开发者处理，而没有提供较好地组件内优雅处理这些异常的方式。
* 在 React 16.x 版本中，引入了所谓 Error Boundary 的概念，从而保证了发生在 UI 层的错误不会连锁导致整个应用程序崩溃；未被任何异常边界捕获的异常可能会导致整个 React 组件树被卸载。
* 所谓的异常边界即指某个能够捕获它的子元素（包括嵌套子元素等）抛出的异常，并且根据用户配置进行优雅降级地显示而不是导致整个组件树崩溃。
* 异常边界能够捕获渲染函数、生命周期回调以及整个组件树的构造函数中抛出的异常。


## 生命周期阶段

- 首次渲染
	- willMount
	- render
	- didMount
- props更新时
	- receiveProps
	- shouldUpdate
	- willUpdate
	- render
	- didUpdate
- state更新时
	- shouldUpdate
	- willUpdate
	- render
	- didUpdate
- 卸载
	- willUnmount

## V16.3 最新变化

1. 去掉了3个方法
	* componentWillMount
	* componentWillReceiveProps
	* componentWillUpdate

2. 增加了2个方法
	* static getDerivedStateFromProps(nextProps, prevState)
	* getSnapshotBeforeUpdate(prevProps, prevState)

3. 更改了1个方法，增加了第3个参数
	* componentDidUpdate(prevProps, prevState, snapshot)

## V17 

渲染机制变成Async Render：
在dom真正render之前，React中的调度机制可能会不定期的去查看有没有更高优先级的任务，
如果有，就打断当前的周期执行函数(哪怕已经执行了一半)，等高优先级任务完成，再回来重新执行之前被打断的周期函数。

### 新增

1. UNSAFE_componentWillMount
2. UNSAFE_componentWillReceiveProps 
3. UNSAFE_componentWillUpdate





























