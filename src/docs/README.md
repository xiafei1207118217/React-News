<!-- 开发前的准备 -->
 1.安装Node.js
 安装完成后在命令行中输入node -v 和npm -v 看是否安装完成。

 2.配置npm国内镜像源
 npm install -g cnpm --registry=https://registry.npm.taobao.org。

 3.新建一个项目
 创建一个项目文件目录
 npm init 对项目进行初始化按照提示创建，创建成功后会在项目中生成一个package.json文件。

 4.安装react相关的包
 npm install --save react react-dom babelify babel-preset-react 
 npm babel-preset-es2015 --save                                       如果使用es5还需要安装es2015的支持 

 5.webpack相关配置
 npm install -g webpack                              全局安装webpack
 npm install -g webpack-dev-server                   全局安装webpack服务器
 npm install webpack --save                          项目中安装webpack
 npm install webpack-dev-server --save               项目中安装webpack服务器
 webpack                                             将项目中所用到的包打包成浏览器认识的js文件
 webpack --watch                                     开启监视，每次源码有变动都会重新编译
 webpack-dev-server                                  在开发服务器上
 webpack-dev-server --contentbase src --inline --hot 只针对src目录下的

 webpack.config.js文件中进行配置。

<!-- -------------------------------------->
 <!-- react的知识梳理 -->
<!-- -------------------------------------->

 <!-- react虚拟DOM的概念 -->
 1.什么是虚拟DOM：虚拟DOM是在DOM的基础上建立了一个抽象层，对数据和状态所做的任何改动，都会被自动且高效的同步到虚拟DOM，经过虚拟DOM的高效的diff算法之后再批量同步到DOM中。

 2.虚拟DOM的原理：React会在内存中维护一个虚拟DOM树，当数据发生变化时，React会自动更新虚拟DOM然后将新的虚拟DOM与旧的进行对比，得到一个Diff然后将Diff放到一个队列里面，最终批量更新这些Diff到DOM中。

 3.虚拟DOM的优缺点
 优点：更新速度非常快。
 缺点：在首次渲染DOM的时候由于多了一层虚拟DOM的计算，所以比一般的慢。

 <!-- React的组件 -->
 1.使用ES6的语法定义一个React的组件
   class 组件名 extends React.Component {
     render() {
       return (

       );
     }
   }
 注：组件名称必须以大写字母开头。
  
 2.渲染组件
 ReactDOM.render(
   组件名称,
   document.getElementById('id名称')
 );

 3.组件定义别名
  项目中有时候会对组件进行一些判断这时候可以给组件定义一个别名。
  const Component = <Welcome />   //定义
  <div>
    {Component}
  </div>

 <!-- React的生命周期 -->
  react的生命 周期主要分为初始化，更新和卸载3个部分
 0~5为初始化，
 0.constructor  构造函数
  constructor函数包含两个默认的参数props和context，父组件可以通过这个构造函数传递给子组件。需要传入super对象，否则会发生this指向错误。

 1.getDefaultProps 设置默认的props可以使用defaultProps设置组件的默认属性

 2.getInitialState  使用es6的语法时是没有这个钩子函数的
 
 3.componentWillMount  组件将要挂载
  该状态表示：组件刚经历过constructor初始完数据，组件还未渲染完成，还没有进入render，DOM还未渲染，整个生命周期中只调用一次。
  componentWillMount一般使用的比较少，更多的是用在服务端渲染，一般ajax请求不写在这个状态里面，因为如果请求过来的数据是空会影响页面的渲染，可能看到的就是空白。

 4.render() 
  render函数会插入jsx生成的dom结构，react会生成一份虚拟的dom树。在每一次组件更新的时候此时react会通过diff算法来比较更新前后的新旧DOM树，比较之后找到最小的有差异的DOM节点，并重新渲染。
 
 5.componentDidMount  组件渲染完成
  组件第一次渲染完成，此时DOM节点已经生成，可以在这里调用ajax请求，返回数据setState后组件会重新渲染，只调用一次。

 6.componentWillReceiveProps(nextProps)
  组件在接收新的props时调用，将nextProps与this.Props对比，将nextProps setState为当前组件的state，从而重新渲染组件。
  
 7.shouldComponentUpdate(nextProps,nextState)
  用于组件重新渲染的生命周期，在react中setState后，state发生变化，组件会重新开始渲染，由于父组件的重新渲染会导致所有子组件的重新渲染，这个时候是不需要在所有的子组件中进行重新渲染的，因此需要在子组件中进行判断。如果不需要进行重新渲染那么return false即可。

 8.componentWillUpdate(nextProps,nextState)
  组件在进行重新渲染之后在这里拿到nextProps和nextState

 9.render函数
  渲染。

 10.componentDidUpdate(prevProps,PrevState)
  

 11.componentWillUnmount()

