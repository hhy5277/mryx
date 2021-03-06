#### 项目描述
&nbsp;&nbsp;&nbsp;&nbsp;一个基于优鲜食物的移动端购物网站（大部分功能模块已实现，适合有一定Vue基础的人学习，项目已经上传到我的[GitHub](https://github.com/WJCHumble/mryx)，项目实施需要的资源已经放在素材文件夹下，包括接口文档、图片资源等）

#### 技术栈
&nbsp;&nbsp;&nbsp;&nbsp;Vue CLI + Vue Router + Vuex + Less + Mint UI + axios + Swiper + Animate + Better Scroll + Mock + Vue Touch

### 项目展示(此处只列举部分)

1. 首页

<div align=center> <img src="https://img-blog.csdnimg.cn/20190629191039811.png" width = "300" height = "500"  /> </div>


2.  城市选择

<div align=center> <img src="https://img-blog.csdnimg.cn/20190629154417256.png" width = "300" height = "500"  /> </div>


3.  购物车

<div align=center> <img src="https://img-blog.csdnimg.cn/20190629154517729.png" width = "300" height = "500"  />  </div>


4.  商品详情

<div align=center> <img src="https://img-blog.csdnimg.cn/20190629154600756.png" width = "300" height = "500"  /> </div>

5. 个人中心


<div align=center> <img src="https://img-blog.csdnimg.cn/20190629154637568.png" width = "300" height = "500"  /> </div>


6.  收获地址

<div align=center> <img src="https://img-blog.csdnimg.cn/20190629154710992.png" width = "300" height = "500"  /> </div>

<div align=left> 
  
### 基本使用

#### 使用less
	
```javascript
	cnpm install less less-loader -S-D
```

#### 使用swiper

```javascript
	cnpm install swiper -S-D
	//在组件中引入
	//引用swiper
	import Swiper from 'swiper' 
	//引入css文件
	import 'swiper/dist/css/swiper.min.css'
	
	//然后在挂载的时候初始化swiper
	mounted() {
		    this.nextTick(() => {
		    	this.scroll = new Swiper('.swiper-container', {
			    autoplay: true,
			    // 如果需要分页器
		        pagination: {
		          el: '.swiper-pagination',
		        },
		    })
		    })
	}
```

#### 使用mint-ui

```javascript
	cnpm install mint-ui -S
	cnpm install babel-plugin-component -S-D
```
&nbsp;&nbsp;&nbsp;&nbsp;打开.babelrc进行配置，在plugin插入一项配置，例如：

```javascript
	"plugins": ["transform-vue-jsx", "transform-runtime", ["component", [
		  {
		    "libraryName" : "mint-ui",
		    "style": true
		  }
		  ]]]
	//此处是插入了component这个
```
&nbsp;&nbsp;&nbsp;&nbsp;使用：

```javascript
	main.js中import 'mint-ui/lib/style.css'
    import {Navbar, TabItem} from 'mint-ui'
```

### 使用vuex

```javascript
	cnpm install vuex -S
```

&nbsp;&nbsp;&nbsp;&nbsp;创建 store 文件夹
```javascript
	- index.js
	- state.js
	- getters.js
	- mutation-types.js
	- actions.js
	- mutations.js
```
&nbsp;&nbsp;&nbsp;&nbsp;需要注意：每个.js文件写的时候都需要注意导出 export default{} 或 export const ....
&nbsp;&nbsp;&nbsp;&nbsp;并且state getters actions mutations都是有多个  每个间要用,号隔开，在index.js 中分别引入(import)state.js getters.js actions.js mutations.js vue vuex
&nbsp;&nbsp;&nbsp;&nbsp;使用vuex	   Vue.use(vuex)，创建vuex   

```javascript
	export default Vuex.Store({
					state,
					getters,
					actions,
					mutations,	
				})
```
&nbsp;&nbsp;&nbsp;&nbsp;在main.js中为vue实例挂载vuex，引入store/index.js，在实例中挂载。
### 使用animate.css

```javascript
	cnpm install animate.css
```
&nbsp;&nbsp;&nbsp;&nbsp;在 main.js 中引入

```handlebars
 	import animate from 'animate.css'		
```

&nbsp;&nbsp;&nbsp;&nbsp;在页面中使用

```javascript
	<transition enter-active-class="animated fadeIn"></transition>
```

### 使用better-scroll

&nbsp;&nbsp;&nbsp;&nbsp;使用better-scroll实现各种滚动效果

```handlebars
	npm install better-scroll -S
```
&nbsp;&nbsp;&nbsp;&nbsp;具体使用看[官方文档](https://ustbhuangyi.github.io/better-scroll/doc/zh-hans/installation.html#npm)

```handlebars
	this.$nextTick(() => {
		if(!this.scroll) {
			this.scroll = new BScroll(this.$refs.wrapper, {
				click: true
			})
		} else {
			this.scroll.refresh()
		}
	})
```
&nbsp;&nbsp;&nbsp;&nbsp;需要注意的是子元素的高度一定要大于父元素的高度，子元素设置超出隐藏
### 跨域访问接口

&nbsp;&nbsp;&nbsp;&nbsp;正常情况下，要实现跨域，是通过后台进行配置响应的响应头的参数。
&nbsp;&nbsp;&nbsp;&nbsp;vue-cli 则跨域通过 node.js 代理服务器实现跨域请求。
&nbsp;&nbsp;&nbsp;&nbsp;文件路径 config/index.js

```handlebars
	proxyTable: {
	   '/api': { // 匹配所有以 '/api'开头的请求路径  即匹配的是axios中传入的url参数，/api/user  这种形式才会匹配
	     target: 'http://d.apicloud.com/mcm/api', // 代理目标的基础路径
	     changeOrigin: true, // 支持跨域
	     pathRewrite: {// 重写路径: 去掉路径中开头的'/api'  当真正的接口不需要api时重写
	       '^/api': ''  //去掉匹配到的路径的/api  如果不去掉就删除pathRewrite
	     }
	   } 
	}
	//最后得到的路径就是 target+url
	//假设请求的url为 /api/user
	//经过node.js代理后  真正请求的是 http://d.apicloud.com/mcm/api/user
	//需要注意的是F12显示的仍然是localhost:8080/api/usesr  但实际上发送的地址是经过node.js代理服务器实现的跨域请求

请求头
	const instance = axios.create({
	  baseURL: '/api',
	  timeout: 1000,
	  headers: {
	  	'X-APICloud-AppId': 'A6914327011091',
	  	'X-APICloud-AppKey': '8ac17d22e49cb7982d82796097cec52a6c7cd01d.1475375422841'
	  }
	})
	//get请求
	promise = instance.get(url)
	//post请求
	promise = instance.post(url)
```

### 关于浮点数计算的问题

```javascript
	state.totalPrice = parseFloat((state.totalPrice + food.price).toFixed(2))
```
	
&nbsp;&nbsp;&nbsp;&nbsp;需要注意：不能直接(state.totalPrice + food.price).toFixed(2)，因为toFixed() 返回一个数值的字符串表现形式。
### 首页左右滑动效果

&nbsp;&nbsp;&nbsp;&nbsp;组件用的是mint-ui提供的当时 存在一个问题  它只提供了滑动效果 不会和tab动态的关联起来，所以借助了vue-touch。
&nbsp;&nbsp;&nbsp;&nbsp;vue-touch使用: 

```javascript
	cnpm install vue-touch@text
```
&nbsp;&nbsp;&nbsp;&nbsp;main.js绑定vue

```javascript
	import VueTouch from 'vue-touch'
	Vue.use(VueTouch, {name: 'v-touch'})
```

&nbsp;&nbsp;&nbsp;&nbsp;FoodList中使用

```javascript
	<v-touch @swipeLeft=""></v-touch>  //从左往右滑动
	<v-touch @swipeRight=""></v-touch> //从右往左滑
    绑定事件，使用this.$emit('v-swipeLeft')  //自定义事件
```
	    
&nbsp;&nbsp;&nbsp;&nbsp;Home中使用

```javascript
	<FoodList @v-swipeLeft=""/>
```
		
&nbsp;&nbsp;&nbsp;&nbsp;绑定事件

```javascript
	触发nav的updateSelectedIndex事件
	通过this.$refs.nav.updateSelectedIndex(更改的下标) //要先给nav绑定ref="nav"
```
&nbsp;&nbsp;&nbsp;&nbsp;优化建议：是否可以通过watch监听navBar的下标变化，如果变化了，在this.$nextTick中执行初始化方法。

### mockjs图片资源
	
&nbsp;&nbsp;&nbsp;&nbsp;安装：

```javascript
	cnpm install mockjs -S
```

&nbsp;&nbsp;&nbsp;&nbsp;在 mock 文件目录下新建 data.js ，格式： Json数据类型。
		
```javascript
   // mockServer.js
   import Mock from 'mockjs'
   import data from './data.json'

   // 返回水果的接口
   Mock.mock('/fruits', {code:0, data: data.fruits})
   // 返回食材的接口
   Mock.mock('/ingredients', {code:0, data: data.ingredients})
   // 返回零食的接口
   Mock.mock('/snacks', {code:0, data: data.snacks})
   //返回牛奶的接口
   Mock.mock('/milks', {code:0, data: data.milks})
   //返回蔬菜的接口
   Mock.mock('/vegetables', {code:0, data: data.vegetables})
```
&nbsp;&nbsp;&nbsp;&nbsp;在main.js中引入 

```javascript
	import './mock/mockServer.js'
```
