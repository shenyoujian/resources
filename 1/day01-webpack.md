# wday01-webpack

## 反馈









## 回顾

- 第一天

  - vue create 名字

  - npm run serve

  - rem

    - 设置html下的font-size:屏幕宽度的/10

      - amf-fleible.js

    - 使用:

      - pxtorem

      - ~~~
        800px   365px  rem  365/80rem
        ~~~

  - vant

    - vant设计稿  375  基值37.5

  - 全局使用less,以前脚手架没安装 要安装什么

    - npm i less less-loader  -D

  - 插槽

    - 默认

      - 定义

        - ~~~
          xxx
          <div>
          <slot></slot>
          </div>
          ~~~

      - 使用

        - ~~~
          <xxx>
          <p></p>
          <template #default>
          </template>
          </xxx>
          ~~~

        - 

    - 具名

      - 定义

        - ~~~
          xxx
          <div>
          <slot name='abc'></slot>
          </div>
          ~~~

      - 使用

        - ~~~
          <xxx>
          <template #abc>
          </template>
          </xxx>
          ~~~

        - 

    - 作用域

      - 定义

        - ~~~
          xxx
          <div>
          <slot :ooo="123" name="abc"></slot>
          </div>
          ~~~

      - 使用

        - ~~~
          默认插槽
          <xxx>
          <template v-slot="scope">
          {{scope.ooo}}
          </template>
          </xxx>
          具名插槽
          <xxx>
          #   v-slot:
          <template #abc="scope">
          {{scope.ooo}}
          </template>
          </xxx>
          ~~~

      - 导航栏

        - ~~~
          van-nav-bar
            title:中间标题
            left-text:左边文本
            right-text:右边文本
            left-arrow:左边小箭头
            slot="left/right/title"
          ~~~

      - 输入框

        - ~~~
          van-field
             v-model:双向绑定
             label:左边标题
             left-icon:前面小图标
             type:类型  number
             slot="left-icon/label/button"
          ~~~

      - 表单

        - 表单验证

          - 基本表单验证

            - ~~~
              van-form 
                 van-field :rules="rulesa"
                 van-field :rules="rulesb"
                 rulesb:[
                 {required:true,message:错误信息,trigger:"onChange/onBlur"},
                 {
                 validator:(value,rule)=>{
                 return boolean值
                   true:验证通过
                   false:验证不通过
                 },message:错误信息,trigger:"onChange/onBlur"
                 }
                 ]
              ~~~

          - 全局表单验证

            - van-form加入ref=form

            - ~~~
              this.$refs.form.validate().then(()=>{
              // 验证通过
              }).catch(()=>{
              // 验证失败
              })
              ~~~

          - 局部表单验证

            - van-filed  name=xxx

            - ~~~
              this.$refs.form.validate('name的值').then(()=>{
              // 验证通过
              }).catch(()=>{
              // 验证失败
              })
              ~~~

          - toast

            - ~~~
              this.$toast.loading({
              duration:0
              })
              this.$toast.clear()
              this.$toast.success("消息替换")
              ~~~

    - 第二天

      - vuex

      - ~~~js
        vuex:状态管理(共享数据管理)
        基本使用
           1:安装  npm i vuex
           2:导入(store/index.js)
              import Vuex from 'vuex'
           3:注册
              import Vue from 'vue'
              Vue.use(Vuex)
           4:实例化
              const store=new Vuex.Store({
                state:{
                   userInfo:""
                },
                mutations:{
                  setUserInfo(state,value){
                    state.userInfo=value
                  }
                  //  使用  this.$store.commit("mutations方法名",值)
                },
                actions:{
                   refreshUserInfo(store){
                   setTimeout(()=>{
                   store.commit("setUserInfo",值)
                   },1000)
                   }
                },
                // this.$store.dispatch("actions方法名",值)
                getters:{
                // 计算属性使用场景:依赖一个或者多个值产生一个新的值
                // 特点:它产生的值会缓存起来,依赖的值改变了它会立马改变,可以当属性使用
                    getUserInfo(state){
                        return state.userInfo
                    }
                    // this.$store.getters.getUserInfo
                
                }
              })
             5:暴露出去
             export default store
             6:在main.js中注入
                import store from '@/store'
                 new Vue({
                     store
                 })
        
        
        
        
        ~~~

      - mapState

        - ~~~
          import {mapState} from 'vuex'
          computed:{
          ...mapState(["userInfo"])
          }
          
          ~~~

    - git

      - ~~~
        git init
        git clone 地址
        git checkout -b 分支名  origin/分支名
        git add .
        git commit -m"注释"
        git remote add origin 地址
        git remote remove origin
        git push -u origin master
        git branch 分支名
        git branch -a
        git branch -d 分支名
        git branch -D 分支名
        git push origin :分支名
        git checkout master
        git merge login
        git push
        产生冲突
            git pull(git fetch   git merge)
            (master | merging)
            git add .
            git commit -m'注释'
            git push
        ~~~

      - scoped:控制css使用范围

        - 加scoped:只能控制当前组件与子组件的最外层
          - 看得到的就能控制,看不到的就不能控制
        - 不加scoped样式就是全局使用

      - api

        - ~~~js
          request.js
            1:安装axios
               npm i axios
            2:导入
            import axios from 'axios'
            3:创建副本
              const _fetch=axios.create({
              baseURL:process.env.VUE_APP_名字
              })
            4:拦截器
              请求拦截
              _fetch.interceptors.request.use(function(config){
              return config
              },
              function(error){
              return Promise.reject(error)
              }
              )
              _fetch.interceptors.response.use(function(res){
              return res
              },
              function(error){
              return Promise.reject(error)
              }
              )
            5:暴露出去
              export default _fetch
            6:使用
              import _fetch from './request'
           export  function 方法名(){
                return   _fetch({
                      url:"/xxx"
                  })
              }
           export { 方法名} 
          ~~~

    - 第三天

      - 工具型方法src/utils

      - ~~~
        export function saveLocal(key,value){
        window.localStorage.setItem(key,value)
        }
        export function getLocal(key){
        return window.localStorage.getItem(key)
        }
        export function removeLocal(key){
        window.localStorage.removeItem(key)
        }
        ~~~

      - 统一异常处理

        - ~~~js
           请求拦截
              _fetch.interceptors.request.use(function(config){
              return config
              },
              function(error){
              return Promise.reject(error)
              }
              )
          响应拦截
          import {Toast} from 'vant'
          import {removeLocal} from '@/utils/local'
          import store from '@/store'
          import router from '@/router'
              _fetch.interceptors.response.use(function(res){
               if(res.data.code===200){
                  return res 
               }
              //  203/204 token错误
                else if(res.data.code===203 || res.data.code===204){
                    1:提示一下
                    Toast.fail("错误信息")
                    2:删除token
                    removeLocal("token")
                    3:修改登陆状态
                 store.commit("修改登陆状态的方法名",false)
                    4:跳转到登陆页
                    router.push("/login")
                   5:中止.then执行,执行.catch 
                    return Promise.reject(new Error("错误信息"))    
                }
              //  205/206...其它错误
                  else{
                     1:提示一下
                      Toast.fail("错误信息")
                     2:中止.then执行,执行.catch 
                   return Promise.reject(new Error("错误信息"))
                  }
              },
              function(error){
              return Promise.reject(error)
              }
              )
          ~~~

        - tabbar

          - ~~~
            van-tabbar
               v-model:选择某一项的索引
               active-color:选中某项后的颜色 
               inactive-color:没选中时的颜色
               placeholder:生成一个等高的占位符
               route:路由模式
               van-tabbar-item to="路由地址"
                  slot="default/icon"
            ~~~

        - cell

          - ~~~
            van-cell
               title:左边文本
               value:右边文本
               is-link:右边小箭头
               center:居中
               slot="icon/title/default"
            ~~~

        - 导航守卫 

          - 前置守卫 

            - ~~~js
              router.beforeEach((to,from,next)=>{
                to:要去的路由信息
                from:从哪来的路由信息
                next:是否允许 通过
                正常通过next()
                跳转至其它地方next(path地址)   
              })
              ~~~

          - 后置守卫

            - ~~~
              router.afterEach((to,from)=>{
              
              })
              ~~~

        - async await 

          - 将异步的代码以同步方式编写

          - 

            ~~~js
            async function xxx(){
            console.log(1)
            try{
            const res=await a1()
            }catch(error){
            console.log(2)
            }
            const res2=await a2()
            console.log(3)
            //  a1,a2同时执行 Promise.all([a1(),a2()]).then.catch
            const resArr=await Promise.all([a1(),a2()])
            }
            ~~~

      - 第四天

        - 统一token处理

          - ~~~js
            _fetch.interceptors.reuqest(function(config){
                // 需要token就加
                if(config.needToken){
                  config.headers.名字=值
                }
            return config
            },function(error){
            return Promise.reject(error)
            })
            function xxx(){
                return _fetch({
                    url:"/xxxx",
                    needToken:true
                })
            }
            ~~~

        - 登陆回跳到前面的地址

          - ~~~js
            // 2个地方
            1:响应拦截
            window.location.href.split("#")[1]
            router.push('/login?redirect=当前要去的路由地址')
            2:前置守卫
            router.beforeEach((to,from,next)=>{
            next()
            next("/login?redirect="+to.fullPath)
            })
            登陆完成处理
            const _redirect=this.$route.query.redirect
            if(_redirect){
                this.$router.push(_redirect)
            }else{
                this.$router.push("/home")
            }
            ~~~

        - Vue.use

          - ~~~js
            Vue.use(js,参数)
            js可以是一个对象也可以是一个函数
            对象
             export default {
                install(Vue){
                  // 全局组件注册
                    // Vue原型加入属性
                    // 全局过滤器
                    Vue.prototype.$num=123
                }
             }
            函数 
            export default function(Vue,options){
                Vue.prototype.$num=123
            }
            ~~~

        - 第五天

          - dialog

            - ~~~js
              this.$dialog.confirm({
              title:标题
              message:内容
              }).then(()=>{
              // 确定点击
              }).catch(()=>{
              // 取消点击
              })
              
              
              ~~~

          - popup

            - ~~~
              van-popup
                 v-model:是否显示弹框
                 position:位置控制top/bottom/left/right/center
              ~~~

          - picker选择器

            - ~~~
              van-picker
                title:中间标题
                show-toolbar:是否显示工具拦
                columns:数据
                default-index:默认选中哪一项的索引
                @confirm=function(value,index){
                value选中项的值
                index选中项的索引
                }
                @cancel
              ~~~

          - area地区选择

            - ~~~
              van-area
                 title:中间标题
                 area-list:地区选择数据
                 value:默认选中某一项的code值
                 columns-num:1:省2:省市3:省市区
                 @confirm=function(value,index){
                  value选中项的值
                   index选中项的索引
                 }
                @cancel
              ~~~

        - van-uploader

          - ~~~
            van-uploader
                v-model:双向绑定上传的数据
                [{url:图像地址}]
                before-read:读取前function(file){
                // 限制上传文件的类型与大小
                file.type文件类型
                file.size:文件大小(字节)
                return boolean
                true:正常上传
                false:中止上传
                }
                after-read:function(res){
                res.content:文件的base64数据格式
                res.file:文件对象
                // 上传文件到服务器
                }
                max-count:1
                @delete:删除的回调事件
                
                
            ~~~

        - props传值

          - ~~~
            父传子(属性)
                传:子组件标签上定义一个属性  属性名=值
                收:
                   props:["属性名"]
                   props:{
                   属性名:{
                      type:Number,
                      default:默认值(原始值直接定义,引用值函数return 引用值)
                   }
                   }
            子传父(子触发父方法)
               定义
                  子组件标签上绑定一个方法
                  <xxx @子组件方法名=父组件方法名 />
               触发:
                 this.$emit('子组件方法名',参数)
            父传子属性
               原始值:不可修改
               引用值:只要不修改它的引用,它的值是可以随便修改
               堆随便修改,栈不可修改
               <xxx :obj="objFather" />
               objFather:{
               a:123
               }
               xxx
               props:["obj"]
               修改obj
               this.obj.a=456
            ~~~

    - 第六天

      - 过滤器

        - 基本使用

          - ~~~
            定义:filters:{
               方法名(参数,参数2){
                return 参数加工后的值
               }
            }
            使用:只能用于{{实参 | 方法名(参数2) }}  v-bind
            ~~~

        - 全局使用

          - ~~~
            Vue.filter(方法名,function(参数){
             return 参数加工后的值
            })
            ~~~

      - 时间处理

        - ~~~
          moment
          基本使用
          moment(时间格式).format("YYYY/MM/DD HH(hh):mm:ss")
          比较时间
          差值=momentA.diff(monentb,'h')
          momentA-monentb的小时差
          
          
          ~~~

    - 缓存组件

      - keep-alive
        - 缓存组件对应的路由出口包一层keep-alive
        - 在对应组件加上name值  keep-alive include="name的值" exclude="name值"
      - beforeCreate  created  beforeMount  mounted  beforeDestroy destroyed
      - activated:显示时,mounted后面执行
      - deactivated:隐藏时,善后处理

    - 下拉 刷新

      - ~~~
        van-pull-refresh
           v-model:是否处于刷新中 下拉 放手后它会自动变成true
           @refresh:刷新方法,刷新完成,修改v-model的值为false
           
        ~~~

    - 上拉加载

      - ~~~
        van-list
           v-model:是否处于加载中,默认:false,滚动条距离底部小于300它会自动变成true
           finished:是否全部加载完成 默认值false
           finished-text:加载完成后的文本显示
           @load=function(){
              // 加载完成
              1:修改v-model的值为false
              2:判断是否全部加载完成,如果全部加载完成修改finished的值为true
           }
        重新激活list组件,
        还原它的所有参数值,静默刷新
        静默刷新
        1:值修改了页面没渲染
          数组:里面的值修改了,vue只能识别它的长度变化
          对象:原本存在的值可以识别,但是新增属性不能识别
        2:组件还原到初始状态
        div v-if="bol"
        bol:true
        this.$nextTick(()=>{
          this.bol=true
        })
        this.bol=false
        
        ~~~

    - 第七天

      - 数组去重

        - ~~~
          [...new Set(数组名)]
          var a={xx:1}
          var b=a
          [a,b]
          ~~~

        - filter

          - ~~~js
            let arr=[1,2,3,2,6,3]
            去重后的数组=arr.filter((item,index,arrtemp)=>{
               return arrtemp.indexOf(item)===index
            })
            ~~~

      - 颜色处理

        - ~~~
          str="abc"  [a,c]  a<span style='color:red'>b</span>c
          str.split("b").join("<span style='color:red'>b</span>")
          ~~~

    - 第八天

      - 路由传参

        - 常规路由传参

          - 传

            - ~~~js
              this.$router.push("/path?参数名=值")
              this.$router.push({
                  path:"/path",
                  query:{
                  参数名:值
                  }
              })
              ~~~

            - 

          - 收

            - ~~~js
              this.$route.query.参数名=值
              ~~~

        - 动态路由匹配

          - 设置路由

            - ~~~
              {
              path:"/xxx/:id?"
              }
              ~~~

          - 传

            - ~~~
              this.$router.push("/xxx/123")
              ~~~

          - 收

            - ~~~
              this.$route.params.id===123
              ~~~

        - name传参

          - 设置路由

            - ~~~
              {
              path:"/xxx",
              component:xxx,
              name:xxx
              }
              ~~~

          - 传

            - ~~~js
              this.$router.push({
              name:"xxx",
              query:{
              参数名:值
              },
              params:{
              参数名:值
              }
              })
              ~~~

          - 收

            - query
              - this.$route.query.参数名
            - params
              - this.$route.params.参数名

        - 跨域

          - 同源

          - 代理(服务器间访问是不会有跨域的)

            - ~~~js
              vue.config.js
              module.exports={
              devServer:{
                 proxy:{
                    "/abc":{
                    target:"http://127.0.0.1/xxx",
                    pathReqrite:{
                    "^/xxx":""
                    }
                    }
                 }
              }
              
              }
              ~~~

    - 第九天

      - 滚动条处理

        - ~~~
          router.afterEach(()=>{
          window.scrollTo(0,0)
          })
          ~~~

      - 滚动条优化

        - 组件缓存起来

        - 记录滚动条位置

          - ~~~
            router.beforeEach((to,from,next)=>{
            from.meta.scrollTop=document.documentElement.scrollTop || window.pageYOffset || document.body.scrollTop
            next()
            })
            ~~~

        - 缓存组件还原滚动条位置

          - ~~~
            activated(){
            window.scrollTo(0,this.$route.meta.scrollTop)
            }
            ~~~

      - van-dropdown-menu

        - ~~~
          van-dropdown-menu
             van-dropdown-item
                  v-model:选中项的value值
                  options:[{
                  text:显示的文本,
                  value:选中该项后的值
                  }]
                  slot="title/default"
          ~~~

      - 索引栏

        - ~~~
          van-index-bar  index-list=[A-Z]
             van-index-anchor index="对应索引栏的锚点值"
          ~~~

      - van-circle

        - ~~~
          van-circle
             v-model:当前值
             rate:目标值(100)
             speed:速度多少rate/秒
             color:进度条颜色 
             layer-color:轨道颜色 
          ~~~

    - 第十天

      - mapGetters

        - 导入   import {mapGetters} from 'vuex'

        - 定义

          - ~~~
            computed:{
            ...mapGetters(["getters方法名"])
            }
            ~~~

          

## 打包

- vue.config.js修改配制

  -  ~~~
    module.exports = {
       publicPath:"./"
    }
    ~~~

- 执行打包命令

  -   npm run build

- 将dist目录下的文件压缩发给相应人员放到服务器

### 前瞻

webpack：

+ 基本概念
+ 基本使用
+ 三项：
  + 配置项
  + loader
  + plugin

## webpack 基本概念

### webpack 基本概念 - 三个问题：

为什么要学习 webpack

+ 1.0 webpack 在工作其实用的不多，但是在面试中出的次数特别多。
+ 2.0 webpack 它是 vue-cli 的底层实现原理，学习了它，可以更加方便的去使用 vue-cli

- 3.0 webpack 的作用
  - 就是 vue-cli 实现的底层的原理
  - vue-cli 搭建的项目有哪些功能：
    + 可以运行为一个服务器
    + 可以进行实时更新
    + 可以解析 css 文件 
    + ....
  - 上述的这些功能，其实都是 webpack 来实现的



### webpack 基本概念 - 准备工作：

> 整个 webpack  的学习我们会以一个例作为主线来完成。

案例：

+ 有一个输入框,我们输入了一些信息,刷新的时候输入框中信息还存在

### webpack 基本概念 - 概念

+ 官网：
  + [中文](https://www.webpackjs.com/)
  + [英文](https://webpack.js.org/)
+ 作用：用来打包资源
  + 表
  + 样式
  + 脚本
  + 图片
  + 资源
+ 打包流程
  + 模块化的项目，以一个 `js` 文件为入口，分别导入其它的文件（.js，图片， 样式.....）形成了一个模块化的项目。webpack 可以将这个模块化的模块进行打包，将 js & 样式 & 图片进行打包，打包之后可以直接运行在浏览器上。

## webpack 的使用

> webpack 我们需要使用它来将我们的项目进行打包，运行到浏览器中

###  webpack 的使用 - 步骤

[传送门](https://www.webpackjs.com/guides/installation/#%E6%9C%AC%E5%9C%B0%E5%AE%89%E8%A3%85)

步骤：

+ 0.0 初始化项目（生成 `package.json` 文件）

  ```bash
  npm init -y
  ```

+ 1.0 安装 webpack

  ```bash
  npm install --save-dev webpack // 安装 webpack  
  npm install --save-dev webpack-cli@3.3.11 // 安装 webpack 的 cli
  // --save-dev  -D less 只用于开发环境
  // --save      -S      即用于开发也用于生产
  ```

+ 2.0 配置 `package.json`

  ```json
  {
  	"scripts": {
  		"build": "webpack ./要打包的文件路径"
  	}
  }
  ```

+ 3.0 打包

  ```bash
  npm run build
  ```

注意点：

+ 1.0 一旦运行 `npm run build` 会将 `src` 目录下所有的内容打包到 `dist` 目录中
+ 2.0 在`index.html` 中不再导入 `src` 目录下的文件，而是导入 `dist` 目录下的内容
+ 3.0 `src` 下的文件依旧是模块化的项目， `dist` 下的是通过 `webpack` 打包之后的结构，不再是模块化的结构了（浏览器可以直接运行。）

### webpack 的使用 - 使用配置文件

> 由于将来在项目中可以修改的参数非常多，如果分散在不同的地方，要修改就太麻烦了。为了解决这样的问题，可以使用 webpack 中的配置文件来管理管理这些需要修改的参数

[传送门](https://www.webpackjs.com/guides/getting-started/#%E4%BD%BF%E7%94%A8%E4%B8%80%E4%B8%AA%E9%85%8D%E7%BD%AE%E6%96%87%E4%BB%B6)

步骤：

+ 1.0 在项目的根目录下创建一个文件名为： `webpack.config.js`

+ 2.0 在配置文件中添加代码

  ```js
  const path = require('path');
  
  module.exports = {
    entry: './src/main.js',
  };
  ```

+ 3.0 配置`package.json` 文件

  ```bash
  {
  	"scripts": {
  		"build": "webpack --config webpack.config.js",		
  	}
  }
  ```

+ 4.0 重新打包

  ```bash
  npm run build
  ```

注意点：

+ 1.0 `npm run build`：

  + `npm run` 要运行 `package.json` 中 `scripts` 下面的指令
  + `start`：找到 `package.json` 中的 `scripts` 下面的 `start` 对应的指令，并且执行

+ 2.0  `webpack --config webpack.config.js`

  ![1585711653944](.\img\1585711653944.png)

## 配置项

> 要 webpack 中配置项有很多，我们不会全部讲完，中会将一些比较常用的配置项列出来

### 配置文件 - 入口

> 设置项目的入口文件(入口的js)

![1585712442911](\img\1585712442911.png)

### 配置文件 - 出口

>  设置项目打包后生成的文件名

![1585712776695](\img\1585712776695.png)

### 配置文件 - 项目的模式

> 项目模式的区分：
>
> > 开发模式：
> >
> > > 概念：程序员在这个过程中进行代码的开发
> > >
> > > 特点：
> > >
> > > > 保证代码的完整性，以方便程序进行代码的修改
> >
> > 生产模式：
> >
> > > 概念：程序员的代码已经开发完成，项目已经发布上线了，已经投入生产使用
> > >
> > > 特点：
> > >
> > > > 代码运行稳定，代码体积尽可能的小（删除空格换行缩进）

mode：（项目的模式）

+  development：开发模式
+  production：生成模式（默认值）

![1585713378978](\img\1585713378978.png)

### 配置文件 - 解析

resolve：

+ alias： 别名

  >  @ ：表示的是 src 目录 ,它就是用 alias 来配置的

  ![1585740816920](\img\1585740816920.png)

+ extensions：可省略的后缀名

  > 在导入文件时，每个文件都有自己的后缀，可通过它来配置可省略的后缀
  >
  > 默认情况下 js 后缀可以省略（除了 js 之外其它的都不能省略）

  ![1585741152012](\img\1585741152012.png)

### 配置文件 - 源码映射

> 打包后的项目报错信息是不准确的，可以使用源码映射来解决这个问题

开启源码映射：

![1585741913812](img\1585741913812.png)

特点：

+ 1.0 一旦项目开启源代码映射，会将原本的代码原本信息也保存一份到打包的目录下。
  + 问题：在加载资源时， main.js 太大了，有一部分没有意义，会消耗性能。
  + 解决方案：
    + 将源码生成到别的文件中： `devtool: 'source-map'`

注意点：

+ 项目的配置文件其实是基于 `nodejs` 的
+ 我们说 `webpack`是基于 `nodejs` 的

总结：

+ webpack 中的配置项其实有很多： [传送门](https://www.webpackjs.com/configuration/)
+ 我们只是挑选了其中用的比较多的来进行讲解，如果后续我们遇到其它的配置可以通过传送门去查看

## loader

> 由于现在写的项目只有 js 文件，webpack 默认是可以打包 js 文件的。但是 webpack 默认仅仅只能打包 js 文件，无法打包     其它文件（图片，样式，字体 ...）.如果想要打包其它的文件，可以借助 webpack 中的 loader 来进行打包。

### loader - 作用

作用：

+ webpack 默认只能打包 js 文件，无法打包其它文件（样式，字体，图片）。如果想要打包其它的文件，可以借助 webpack 中的 loader 来进行打包。

特点：

+ 所有的 loader 都是第三方包，可以帮助 webpack 打包其它资源

### loader - style-loader&css-loader

> 可以用来帮助 webpack 打包  .css 文件

步骤：

+ 1.0 安装打包 css 的 loader

  ```bash
  npm install --save-dev style-loader css-loader
  ```

+ 2.0 配置 Loader (webpack.config.js)

  ```js
  module.exports = {
  	entry: '',
  	output: {},
  	mode: '',
      resolve:{},
  	module: {
  		rules: [
  			{ 
  				test: /\.css$/,
  				use: [
  					'style-loader', // 将样式使用到页面中
  					'css-loader' // 将样式打包到 dist 目录下
  				]
              }
  		]
  	}
  }
  ```

+ 3.0 重新打包 `npm run build`

注意点：

+ 1.0 大部分的 loader 在使用时步骤都是三步： a. 下载 loader  b.配置 loader  c.重新打包
+ 2.0 打包样式时用到了 style-loader & css-loader：
  + css-loader：将 css 中的样式打包到了 `dist` 目录下的文件中了
  + style-loader：将打包后的 css 文件在运行时，添加到页面的头部中以 style 标签进行包裹
+ 3.0 style-loader 与 css-loader 的书写顺序不能改变

### loader - less-loader

> 在写项目时，一般会使用 less 语法来书写样式。less 如果需要打包要借助第三方包： less-loader

使用 less

+ 在 `style` 中创建一个 less.less
+ 添加 less 的样式
+ 在 `src/index.js` 中导入这个 less

打包 less 的步骤：

+ 1.0 安装第三方包

  ```bash
  npm install --save-dev less-loader less
  ```

+ 2.0 配置 loader (webpack.config.js 中完成的)

  ```bash
  module.export = {
  	module: {
  		rules: [{
  			test: /\.less$/,
  			use: [
  				'style-loader',
  				'css-loader',
  				'less-loader'
  			]
  		}]
  	}
  }
  ```

+ 3.0 重新打包

### loader - sass-loader

> 用来打包 sass 文件的

使用 sass 文件：

+ 创建一个 sass 文件（注意点：所有的 sass 文件为了防止跟其它文件冲突，后缀名统一写为 `.scss` ）
+ 完成 sass 的代码
+ 在 `index.js` 中使用

打包 sass 的步骤：

+ 1.0 下载第三方包

  + ~~~node
    npm i node-sass sass-loader -D
    ~~~

+ 2.0  配置第三方包

  + ~~~js
    module.export = {
    	module: {
    		rules: [{
    			test: /\.scss$/,
    			use: [
    				'style-loader',
    				'css-loader',
    				'sass-loader'
    			]
    		}]
    	}
    }
    ~~~

  + 

+ 3.0 重新打包

### loader - file-loader

> 可以用来打包图片

打包图片：

+ 使用图片
  + 在 html 中添加一个容器
  + 给容器设置样式：设置一个背景图片
+ 打包图片：
  + 1.0 下载第三方包
  
    + ~~~
      npm i file-loader -D
      ~~~
  
  + 2.0 配置第三方包
  
    - ~~~
            {
              test: /\.(png|jpg|gif)$/,
              use: [
                {
                  loader: 'file-loader',
                  options: {
                  //配制输出图片的目录
                    outputPath: './assets/img'
                  }
                }
              ]
            },
      ~~~
  
    - 
  
  + 3.0 重新打包
  
  

### loader - babel-loader

> 将高版本js语法打包为低版本语法

打包 es6 为 es5

+ 1.0 下载第三方包

  ```bash
  npm install babel-loader@8.0.0-beta.0 @babel/core @babel/preset-env --save-dev
  ```

+ 2.0 配置第三方包

  ```js
  module: {
    rules: [
      {
        test: /\.js$/, // 将后缀名为 js 的文件进行高版本js转换成低版本js
        exclude: /node_modules/, // 处理的目录不包括 node_modules
        use: {
          loader: 'babel-loader', // 使用 babel-loader 来处理
          options: {
            presets: ['@babel/preset-env'] // 固定写法
          }
        }
      }
    ]
  }
  ```

+ 3.0 重新打包

### loader - vue-loader

> 默认情况下 webpack 无法打包后缀名为 .vue 的文件、如果要打包需要借助第三方包： vue-loader

使用 .vue 文件：

+ 1.0 下载第三方包： vue
+ 2.0 创建一个 `App.vue` 文件
+ 3.0 完成 App.vue 文件的内容
  + template & style & script
+ 4.0 在 main.js 中
  + 导入 Vue
  + 导入 App.vue 
  + 创建一个 vue 实例
  + 将  App.vue 挂载到 vue 实例中

打包 .vue 的过程：

+ 1.0 安装第三方包

  ```bash
  npm install -D vue-loader vue-template-compiler
  ```

+ 2.0 配置 Loader （webpack.config.js）

  ```js
  // 导入 Loader
  const VueLoaderPlugin = require('vue-loader/lib/plugin')
  
  module.exports = {
    module: {
      rules: [
        // 配置 loader
        {
          test: /\.vue$/,
          use: ['vue-loader']
        }
      ]
    },
    plugins: [
      // 将 vue-loader 作为插件来使用
      new VueLoaderPlugin()
    ]
  }
  ```

+ 3.0 重新打包 `npm run start`

注意点：

+ 1.0 vue-loader 的说明文档不在 webpack 中，因为 vue-loader 是属于 vue 的全家桶系列。如果要找去 vue 的官网中去找

总结：

+ loader 与配置项一样，也有很多不同的 loader， 我们只是学习了一些常用的 loader，其它的可以参考 [传送门](https://www.webpackjs.com/loaders/)
+ webpack：
  + 配置项：可以用来配置项目的相关信息
  + loader：可以用帮助 webpack 打包额外的资源

## 插件

> 给 webpack 提供额外的功能

### 插件 - HtmlWebpackPlugin

> 修改内容之后，重新打包好 dist 目录下的内容之后，还需要将 index.html 从根目录下拷贝到 dist 目录下，太麻烦了。
>
> 问题：我不希望每次重新打包 dist 目录之后再将 index.html 拷贝到 dist 目录下。
>
> 解决方案：可以使用 HtmlWebpackPlugin

作用：可以在 dist 目录中自动生成一个 html 文件

使用步骤：

+ 1.0 下载插件

  ```bash
  npm install --save-dev html-webpack-plugin
  ```

+ 2.0 配置插件（webpack.config.js 中完成的）

  ```js
  // 导入插件
  const HtmlWebpackPlugin = require('html-webpack-plugin')
  // 配置插件
  module.exports = {
      plugins: [
          new HtmlWebpackPlugin({           
              template: 'html模版文件路径' // 以谁为模板生成的静态页面
          })
      ]
  }
  ```
  
+ 3.0 重新打包: `npm run build`

注意点：

+ 如果不设置其它属性，默认会生成一个 html 文件
  + 这个文件中没有结构 & 样式
  + 它默认导入了生成的 js 文件

### 插件 - clean-webpack-plugin

> 每次重新打包项目时一定要删除 dist 目录
>
> 问题：每次都删除，太麻烦了。解决这个问题可以使用：clean-webpack-plugin

作用：用来清除 dist 目录

步骤：

+ 1.0 下载插件

  ```bash
  npm install clean-webpack-plugin --save-dev
  ```

+ 2.0 配置插件

  ```js
  // 导入插件
  const { CleanWebpackPlugin } = require('clean-webpack-plugin');
  // 配置插件
  module.exports = {
   	plugins:[
          new CleanWebpackPlugin()
      ]
  }
  ```

+ 3.0 重新打包

注意点：

+ 1.0 插件会帮助自动清除 dist 目录
+ 2.0 以后如果有能力看文档时，尽量用英文文档

### 插件 - webpack-dev-server

> 可以开启一个服务器，具有实时更新的功能

作用：可以开启一个服务器，具有实时更新的功能

步骤：

+ 1.0 下载插件

  ```bash
  npm install --save-dev webpack-dev-server
  ```

+ 2.0 配置插件（webpack.config.js）

  ```js
  module.exports = {
  	devServer: {
      	contentBase: './dist'
  	},
  }
  ```

+ 3.0 配置指令：(package.json)

  ```json
  {
  	"scripts": {
  		"build": "webpack --config webpack.config.js",
  		"serve": "webpack-dev-server --config webpack.config.js --open"
  	}
  }
  ```

+ 4.0 开启服务器：`npm run serve`

注意点：

+ 开启服务器之后，修改完代码之后是不需要自己重新打包， 手动刷新页面的（服务器可以做到时实更新）

### 插件 - 模块的热替换

> 修改 css 之后，可以让页面不 刷新直接更新修改的样式

```js
module.exports = {
	devServer: {
    	contentBase: './dist',
    	hot: true, // 开启模块的热替换
	}
}
```

注意点：

+ 配置文件中的配置项发生修改之后需要重启服务才能生效

总结：

+ 插件的作用是给 webpack 提供额外的功能
+ 插件的种类不单单只有以上几种还有很多，详情请见： [传送门](https://www.webpackjs.com/plugins/)
+ webpack
  + 配置项：配置项目中的相关信息
  + loader：配置打包信息
  + plugin：配置额外功能









