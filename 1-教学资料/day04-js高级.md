# day04 

## 反馈

1.	啊，好舍不得董老师，555，你讲的太好了。今天请务必讲一下冒泡排序
1.	①老师,我是班里数一数二的差生,我是不是也可以多背背面试题去尝试面试,不通过再回来复读呀? ②或者万一真碰到狗shi运进去了,但是自己啥都不会(学习也很慢)那也不要主动辞职,等负责人实在受不了了再来炒我呀? ③老师拜拜 多谢老师的谆谆教诲 我卢某人感激不尽!
   1.	面试过程
      1.	不懂的知识点,你一定会立马搞懂
      1.	面试能力
   1.	试用期头一个月
      1.	成长也是最大的
1.	老师能讲下cookie与session区别，以及在什么时候需要使用到它们，一直对这块比较模糊
   1.	sessionId:用户的id(内存中之类)
   1.	cookie:用户id,
   1.	token:用户生成一个加密串
1.	碰到周林林老师和董老师，是来黑马最值得的事情。如果没有老师这么细致，细心的的去讲原理，很多只是使用的话， 估计很快就会忘记了。老师真的很棒很有耐心，希望你能坚持下去。很遗憾只带了我们这么几天，哎，如果能一直跟着老师学就好了，真的讲的通俗易懂又不厌其烦的重复。天下无不散的宴席，老师再见，等我找到一份好工作，我就把你带出黑马
1.	感觉好多东西好像懂了又好像没懂的样子,说概念说不上来,写倒是能写两句,脑壳疼
   1.	多写.
1.	我廖睿爱您，今天想坐您腿上听课，可以吗？飞 这辈子最大的遗憾就是跟周林林、董浩飞say goodbye
1.	老师觉得培训到现在，我们（平均水准线附近的同学）相当于在职员工的什么水平
   1.	知识面:高级水平
   1.	逻辑处理能力
      1.	初级与初级以上
   1.	10k-16k
      1.	中级开发(2-3年开发经验)
      1.	高级开发
1.	老师有时间的话能带我们过一下git和git冲突解决吗？
   1.	git冲突
      1.	怎么产生的冲突
         1.	不是在最新的代码基础上修改的
            1.	master | merging
         1.	git pull
            1.	git fetch
            1.	git merge
         1.	git merge
      1.	怎么解决
         1.	找到相应文件
         1.	修改代码
         1.	git add .
         1.	git commit -m"注释"
         1.	git push
         1.	有可能出现 一个新的界面(:wq)







## 回顾

- 计算属性传参

  - ~~~js
    computed:{
      xxx(){
         return (参数)=>{
         return 值
         }
      }
        xxx:{
       get(){
        return (参数)=>{
        	 return 值
           }    
         },
       set(value){
         做一些相应处理  
       }
        // this.xxx=123 
        }
    }
    {{xxx(实参)}}
    ~~~

  - watch:

    - ~~~
      某个值的change事件
      props的值能不能watch
      watch:{
      "$route.path"(){},
        方法名(newVal,oldVal){
        	方法名:this.值,去掉this,加上引号
        }
        方法名:{
        deep:true(尝试监听,引用值的修改只有修改了它的引用它才能识别),
        immediate:true(初次赋值也会触发)
        handler(newVal,oldVal){
        
        }
        }
      }
      ~~~

  - 组件v-model

    - v-model是props与emit的简写(语法糖)

      - ~~~
        xxx子
           props:["value"],
           model:{
               prop:"value",
               event:"input"
           },
           this.$emit("input",456)
        app父
          xxx标签 :value="appValue" @input="inputEvent"
            appValue:123
            function inputEvent(num){
            this.appValue=num
            }
           xxx标签  v-model="appValue" 
        ~~~

  - .sync修饰符

    - ~~~
      xxx 子组件 
         props:['value']
         this.$emit("update:value",456)
      app 父组件
         xxx标签 :value.sync="appValue"
         appValue:123
         
      ~~~

  - mixin混入

    - 全局混入

      - ~~~
        Vue.mixin({
        data(){
        return {
          xxx:1
        }
        },
        created(){
          console.log("mixin",this.xxx)  // 2
        }
        })
        
        App.vue
          data(){
          return {
            xxx:2
          }
          },
          created(){
             console.log("app",this.xxx)  // 2
          }
        ~~~

      - 特点:全局混入,所有的组件都会与混入的组件合体

        - 组件有的值取组件的,组件没有的取混入组件的
        - 生命周期:先执行混入组件的,再执行当前组件的

    - 局部混入

      - ~~~
        mixins:[{
        data(){
        return {
        xxx:123
        }
        }
        }]
        ~~~

      - 



## 冒泡排序

从下往上相邻的元素相比较,按规则换位置

~~~js
      let arr = [2, 5, 3, 0]
      for (let i = 0; i < arr.length - 1; i++) {
        for (let j = 0; j < arr.length - 1 - i; j++) {
          if (arr[j] > arr[j + 1]) {
            ;[arr[j], arr[j + 1]] = [arr[j + 1], arr[j]]
            // let temp = arr[j]
            // arr[j] = arr[j + 1]
            // arr[j + 1] = temp
          }
        }
      }
      window.console.log(arr)
~~~



## 补充 - 双向绑定的原理



基本概念：

+ 当视图上的数据发生改变时， data 中的数据也发生改变
+ 当 data 中的数据发生改变时，视图中的数据也发生改变

原理：

+ 主流使用的版本 2.x：

  + 关键字：`Object.defineProperty`

    ```js
    var data = {}
    document.querySelector('#ipt').oninput = function(e) {
    	data.name = e.target.value
    }
    Object.defineProperty(data, 'name', {
    	set: function(value) {
    		this._name = value
    		document.querySelector('#box').innerHTML = value
            document.querySelector('#ipt').value = value
    	},
    	get: function() {
    		return this._name
    	}
    })
    ```

+ 最新的版本 3.x

  + 关键字： `Proxy`

  + 用法

    + ~~~js
      返回值(proxy实例对象)=new Proxy(对象,{
      get(target,key){
      	return target[key]
      },
      set(target,key,value){
      	target[key=value]	
      }
      })
      ~~~

    + 

+ 注意点：

  + 我们这里讲的实现原理是实现的方法，其实在 vue 底层实现这玩意儿的时候用到一种模式：观察者模式。



## mockjs

>  生成随机数据，拦截 Ajax 请求 

官网地址:[http://mockjs.com/](http://mockjs.com/)

**使用场景**:前后端分离开发,后端 没有给出接口,只给出相应的基本数据格式情况下,自己可以使用mock模拟后端接口数据

**基本使用**

1. 安装   `npm i mockjs -D`

2. 引入`Mock`配制需要拦截的`ajax`请求

   ~~~js
   import Mock from 'mockjs'
   Mock.mock('需要拦截的接口地址', {'// 拦截后的数据格式'})
   //如:
   import Mock from 'mockjs'
   // 这里random是mock提供的一个随机处理机制
   let rendomMock = Mock.Random
   Mock.mock(process.env.VUE_APP_URL + '/articles/share/15', {
     code: 200,
     message: 'success',
     data: {
       id: 16,
       title: rendomMock.title(),  // 生成随机标题
       content: rendomMock.cparagraph(),  // 生成随机文章内容
       contentText: rendomMock.cparagraph(),
       'read|1-100': 1, // "参数名|min-max":值的示例,能生成一些特别随机值
       created_at: '2020-06-29T03:18:29.000Z',
       updated_at: rendomMock.date(),// 生成随机时间
       'star|1-1000': 1,// 生成一到1000有随机数
       collect: 2,
       author: {
         nickname: rendomMock.name(),// 生成随机名字
         avatar: '/uploads/avatar09_4b071982f9.jpeg'
       },
       share: '15'
     }
   })
   ~~~
   
3. 在`main.js`中应用`mock`

   ~~~js
   require('上一步mock.js的路径')
   如:require('@/api/mock.js')
   ~~~

   









## Vue.extend方法

> 如果要实现通过方法调用的弹框组件需要怎么做呢?咱们先来看看如何动态的渲染组件到页面上

[Vue.extend](https://cn.vuejs.org/v2/api/#Vue-extend)

[vm.$mount](https://cn.vuejs.org/v2/api/#vm-mount)

[vm.$el](https://cn.vuejs.org/v2/api/#vm-el)



1. `Vue.extend(组件)`
   1. 返回的是一个构造函数
   2. 不能直接使用,还需要实例化
   3. 实例化出来的就是包含传入的组件特性的实例化对象
2. `$mount`
   1. `$mount(选择器)`
      1. 直接找到对应的dom元素并把组件添加进去
      2. 但是`html,body`会有异常提示
   2. `$mount()`
      1. 基于组件的`template`生成对应的结构`dom`
      2. `$el`可以获取到
3. 直接添加到希望添加的位置即可



## 需求 - message组件

> 简短的提示我们可以用`message`组件来实现,该组件的使用是通过方法哦

[Element - message](https://element.eleme.cn/#/zh-CN/component/message)



**参数:**

| 参数     | 参数说明          | 类型   | 可选值 | 默认值 |
| -------- | ----------------- | ------ | ------ | ------ |
| title    | 标题              | string | -      | 标题   |
| duration | 多久之后消失,毫秒 | number | -      | 1000   |

**需求:**

1. 可以在任意的`vue实例`上通过`$message`调用
2. 消失之后直接从`dom`树中移除
3. 参数的传递用对象的形式`this.$message({title:"标题",duration:3000})`





**基本结构:**

```vue
<template>
  <div class="my-message my-message--info">
    <i class="my-message__icon iconfont icon-info"></i>
    <p class="my-message__content">标题</p>
  </div>
</template>

<script>
export default {}
</script>

<style lang="less">
.my-message {
  min-width: 380px;
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
  border-width: 1px;
  border-style: solid;
  border-color: #ebeef5;
  position: fixed;
  z-index: 9999;
  left: 50%;
  top: 20px;
  transform: translateX(-50%);
  background-color: #edf2fc;
  padding: 15px 15px 15px 20px;
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-align: center;
  -ms-flex-align: center;
  align-items: center;
  // 根据类型设置不同的外观
  &.my-message--info {
    color: #909399;
  }
  // success
  &.my-message--success {
    background-color: #f0f9eb;
    border-color: #e1f3d8;
    .my-message__icon {
      color: #67c23a;
    }
    .my-message__content {
      color: #67c23a;
    }
  }
  // warning
  &.my-message--warning {
    background-color: #fdf6ec;
    border-color: #faecd8;
    .my-message__icon {
      color: #e6a23c;
    }
    .my-message__content {
      color: #e6a23c;
    }
  }
  // error
  &.my-message--error {
    background-color: #fef0f0;
    border-color: #fde2e2;
    .my-message__icon {
      color: #f56c6c;
    }
    .my-message__content {
      color: #f56c6c;
    }
  }
  .my-message__icon {
    margin-right: 10px;
  }
  .my-message__content {
    padding: 0;
    font-size: 14px;
    line-height: 1;
    margin: 0;
  }
}
</style>

```





## 实现 - message组件

> 结合上面分析的这几个方法,咱们来实现一下`message`组件

**message.vue**

~~~vue
<template>
  <transition name="xxx">
    <div class="my-message" v-show="isShow" :class="'my-message--' + type">
      <i class="my-message__icon iconfont" :class="'icon-' + type"></i>
      <p class="my-message__content">{{ title }}</p>
    </div>
  </transition>
</template>
<script>
export default {
  data () {
    return {
      type: 'info',
      title: '',
      duration: 1000,
      isShow: false
    }
  },
  created () {},
  methods: {
    show () {
      this.isShow = true
      setTimeout(() => {
        this.isShow = false
        setTimeout(() => {
          document.body.removeChild(this.$el)
        }, 500)
      }, this.duration)
    }
  }
}
</script>
<style lang="less" scoped>
.my-message {
  min-width: 380px;
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
  border-width: 1px;
  border-style: solid;
  border-color: #ebeef5;
  position: fixed;
  z-index: 9999;
  left: 50%;
  top: 20px;
  transform: translateX(-50%);
  background-color: #edf2fc;
  padding: 15px 15px 15px 20px;
  display: -webkit-box;
  display: -ms-flexbox;
  display: flex;
  -webkit-box-align: center;
  -ms-flex-align: center;
  align-items: center;
  // 根据类型设置不同的外观
  &.my-message--info {
    color: #909399;
  }
  // success
  &.my-message--success {
    background-color: #f0f9eb;
    border-color: #e1f3d8;
    .my-message__icon {
      color: #67c23a;
    }
    .my-message__content {
      color: #67c23a;
    }
  }
  // warning
  &.my-message--warning {
    background-color: #fdf6ec;
    border-color: #faecd8;
    .my-message__icon {
      color: #e6a23c;
    }
    .my-message__content {
      color: #e6a23c;
    }
  }
  // error
  &.my-message--error {
    background-color: #fef0f0;
    border-color: #fde2e2;
    .my-message__icon {
      color: #f56c6c;
    }
    .my-message__content {
      color: #f56c6c;
    }
  }
  .my-message__icon {
    margin-right: 10px;
  }
  .my-message__content {
    padding: 0;
    font-size: 14px;
    line-height: 1;
    margin: 0;
  }
}
.xxx-enter-active,
.xxx-leave-active {
  transition: all 0.5s;
}
.xxx-enter {
  opacity: 0;
}
.xxx-leave-to {
  opacity: 0;
}
</style>

~~~

main.js中处理全局$message

~~~js
import message from '@/components/message'

Vue.prototype.$message = function ({ type, title, duration }) {
  const messageFn = Vue.extend(message)
  const messageObj = new messageFn()
  messageObj.type = type
  messageObj.title = title
  messageObj.duration = duration
  messageObj.$mount()
  document.body.appendChild(messageObj.$el)
  messageObj.show()
}
~~~

**调用**

~~~js
      this.$message({
        type: 'success',
        duration: 5000,
        title: '我是新来的' + Date.now()
      })
~~~

## 路由总结

~~~js
vue-router
1:下载  npm i vue-router
2:导入  import VueRouter from 'vue-router'
3:注册 Vue.use(VueRouter)
4:实例化  
   const router=new VueRouter({
       routes:[
         {
           path:"/",
           component:"导入的组件"
         }
       ]
    })
5:暴露出去
   export default router
6:main.js注入到new Vue({router})
7:路由出口
   router-view
路由对应勾子
  全局勾子
    前置守卫
    router.beforeEach((to,from,next)=>{
      next()
    })
    后置守卫
    router.afterEach((to,from)=>{      
    })
  路由所对应组件的勾子
    进入前,当前对应组件还没有完成实例化,还不能访问data与methods,它在beforeCreate执行前执行
    beforeRouteEnter(to,from,next){
      next()
    }
    更新时:路由没有跳转(还是在当前路由,但是路由参数改变之类),它就会触发更新
    beforeRouteUpdate(to,from,next){
      next()
    }
    离开时,它在beforeDestroy之前执行
    beforeRouteLeave(to,from,next){
      next()
    }
  路由配制内的勾子
     beforeEnter(to,from,next){
       next()
     }

  路由勾子执行先后:beforeEach----beforeEnter----beforeRouteEnter-----afterEach----beforeRouteUpdate----beforeRouteLeave
~~~



# js 高级

## 防抖与节流

防抖

- 过一段时间执行一次代码,但是这段时间内调用相应代码,重新进行倒计时(清理掉以前倒计时)执行相应代码

- ~~~js
      function fnXXX (fn, time) {
        var _time = null
        return function () {
          let _arg = arguments
          let _this = this
          if (_time) {
            clearTimeout(_time)
          }
          _time = setTimeout(() => {
            fn.apply(_this, _arg)
            // fn()
          }, time)
        }
      }
    //  window.addEventListener('scroll', fnXXX(scrollFn, 500))
  ~~~

- 节流

  - 过一段时间执行一次相应代码,如果这段时间内你想调用相应代码,它是不执行的

  - ~~~js
        function fnXXX2 (fn, time) {
          var isLoading = false
          return function () {
            let _arg = arguments
            if (!isLoading) {
              isLoading = true
              let _this = this
              setTimeout(() => {
                //   fn()
                fn.apply(_this, _arg)
                isLoading = false
              }, time)
            }
          }
        }
    ~~~

  - 





## var 关键字 

### var - 声明赋值

**作用**：

+ 声明变量

**对比 let & const**

+ const：

  + 一旦定义无法修改

    ```js
    const a = 'haha'
    a = 'abc' // 报错，const 修改的变量无法修改
    ```

+ let：

  + 定义的变量存在作用域，超出作用域就无法再次访问

    ```js
    if (5 === 5){
    	let a = 'xjj'
    	console.log(a) // xjj
    }
    console.log(a) // 报错：无法访问到 a
    ```

    

### var - 作用域

**全局作用域**

+ 说明：var 在全局作用域下声明变量，在任何位置都能访问到

  ```js
  var name = 'xxx'
  // 在全局作用域中访问
  console.log(name)
  // 在局部作用域中访问
  if (5 === 5) {
  	console.log(name)
  }
  ```

  

**局部作用域**

+ 说明：var 在局部作用域下声明变量,在任何位置也能访问到

  ```js
  if (5 === 5) {
  	var name = 'xxx'
  	console.log(name) // xxx
  }
  console.log(name) // xxx
  ```


+ 注意点：

  + 普通的大括号不会影响 var 定义的变量，但是函数会
  + 在函数中使用 var 定义的变量不是全局变量，只是局部变量 

  

**作用域访问规则**

+ 说明：var 定义的变量，在被使用时，会优先在当前作用域下面找对应的属性，如果找到直接使用，如果找不到，则去父级作用下找对应的变量

  ```js
  // 案例一：
  var name = 'xxx1'
  function fn () {
  	var name = 'xxx2'
  	console.log(name)
  }
  
  
  // 案例二：
  var name = 'xxx'
  function fn () {
  	console.log(name)
  }
  ```

  



### var - 预解析

**变量预解析**

+ 说明：如果给 var 声明的变量赋值，声明会被提升到当前作用域的最前面

  ```js
  // 原代码
  console.log(a) 
  var a = 123
  
  
  // 预解析后的代码（只有声明被提前赋值依旧没有被提前）
  var a
  console.log(a)
  a = 123
  ```

  

**函数预解析**

+ 说明：如果定义一个函数，函数也会被提升到当前作用域的最前面

  ```js
  // 原代码
  sayHi()
  function sayHi () {
  	console.log('hello')
  }
  
  
  // 预解析后的代码
  function sayHi () {
  	console.log('hello')
  }
  sayHi()
  ```

+ 注意点：

  + 如果将函数赋值给一个var定义的变量, 那么函数不会被预解析, 只有变量会被预解析

    ```js
    // 源代码
    sayHi()
    var sayHi = function () {
    	console.log('hello')
    }
    
    
    // 预解析后的代码
    var sayHi
    sayHi()
    sayHi = function () {
    	console.log('hello')
    }
    
    ```

    

### var - 面试题

```js
    	//案例1
        // {
        //     var num = 5;
        // }
        // console.log(num);


        //案例2
        // var num = 5;
        // if (num > 3) {
        //     var sum = 7;
        // }
        // console.log(sum);

        //案例3
        // for (var i = 0; i < 10; i++) {
        // }
        // console.log(i);


        //案例4 全局变量
        // var name = "zs";
        // function f() {
        //      name = "ww";
        // }
        // f();
        // console.log(name);//ww

        //案例5
        // function f() {
        //     var name1 = "zs";
        // }
        // f();
        // console.log(name1);


```

~~~ 
var a=10
//window.a=?
b=20
console.log(b)
function test(){
var a=b=20
}
test()
console.log(a)   ?
console.log(b)   ?
~~~

## 预编译

>预编译发生在代码执行的前一刻

**预编译过程:**

1. 创建了一个对象
2. 把形参与变量声明作为对象的属性名,值为undefined
3. 将实参值与形参值统一
4. 在函数体里面找函数申明,值赋予函数体(函数的名字作为第一步创建的名字,把值赋上来)

注意:函数表达式与函数申明 区别

~~~js
var xxx=function(){}  这叫函数表达式
function xxx(){}    这叫函数申明 
~~~



~~~js
      function test(a) {
            window.console.log(a);
            var a = 1;
            window.console.log(a);
            function a() {}
            window.console.log(b);
            var b = function () {};
            window.console.log(b);
      }
      test(1);
~~~

~~~js
      window.console.log(a)
      var a = 10
      function a () {
        window.console.log(a)
      }
      a()
~~~

~~~js
      window.console.log(c)
      c = 10
      var c
      window.console.log(c)
~~~

~~~js
      function xxx (a, b) {
        window.console.log(a) 
        c = 0
        var c
        window.console.log(c) 
        a = 3
        b = 2
        window.console.log(b) 
        function b () {}
        window.console.log(b) 
      }
      xxx(1)
~~~









## in 关键字

### in - forin遍历对象&数组

+ 说明：forin可以用来遍历对象

  ```js
  // 遍历对象
  var obj = {
  	name: 'xjj',
  	age: 19,
  	gender: '男'
  }
  for(item in obj) {
  	console.log(item, obj[item])
  }
  
  
  // 遍历数组
  var arr = [
      { id: 1, name: '追命' },
      { id: 2, name: '铁手' },
      { id: 3, name: '无情' }
  ]
  for(item in arr) {
  	console.log(item, arr[item])
  }
  ```

  

### in - 判断对象中是否包含属性

+ 说明：使用 in 关键字，可以判断一个对象是否存在某个属性

  ```js
  var obj = {
  	name: 'xjj',
  	age: 19,
  	gender: '男'
  }
  // 判断是否存在 name 属性
  var bool = 'name' in obj
  console.log(bool)
  ```





## delete - 关键字

### delete - 基本使用

+ 说明：

  + 作用一：delete关键字可以删除没有用var,let const等关键字声明的变量

  ```js
      aa = '123'
      console.log(aa) // 123
      delete aa
      console.log(aa) // 报错
  ```

  + 作用二：delete关键字可以删除对象的属性

    ```js
        var obj = {
          a: 'xxx'
        }
        console.log(obj.a) // `xxx`
        delete obj.a
        console.log(obj.a) // undefined
    ```









## websocket

> 它的最大特点就是，服务器可以主动向客户端推送信息，客户端也可以主动向服务器发送信息 ,它不同于http请求,它建立 的是一个tcp连接.
>
> https://www.runoob.com/html/html5-websocket.html

**服务器基本使用**(基于node)

1. 安装依赖 

   ~~~
   npm i ws
   ~~~

2. 创建一个index.js文件

   ~~~js
   var WebSocketServer = require('ws').Server
   // node服务器开启websocket
   wss = new WebSocketServer({ port: 1234 })
   // 与客户端建立连接
   wss.on('connection', ws => {
     console.log('Connecting...')
     ws.on('message', msg => {
       if (msg.includes('md')) {
         // 发送信息
         ws.send('警告:不允许说md')
       } else {
         ws.send(msg)
       }
     })
   })
   ~~~

3. 通过node,运行index.js

   ~~~
   node index.js
   ~~~

**客户端基本使用**

​          **创建一个基本的index.html,运行html,就可以在控制台打印区域看到信息**

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8" />
  </head>
  <body>
    <input id="text" type="text" />
    <button type="button" onclick="sendMsg()">send</button>
    <script> 
        // 客户端连接服务端
      var ws = new WebSocket('ws://localhost:1234')
      // 客户端连接服务端成功后反选
      ws.onopen = function (e) {
        console.log('连接成功')
      }
     // 客户端接收服务端信息
      ws.onmessage = function (e) {
        console.log(e.data)
      }
     // 客户端向服务端发送信息
      function sendMsg () {
        const _input = document.querySelector('#text')
        ws.send(_input.value)
      }
    </script>
  </body>
</html>
```



## vue缺点:

   单页面应用:首页打开慢,不利于seo

seo:搜索排名:抓取的html

- vue nuxt.js   服务端渲染ssr  
- 服务端也要有一些相应处理
- seo
  - vue页面(nuxt.js)
  - jquery页面
- 管理系统 (不要seo)

