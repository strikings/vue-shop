## 1.项目概述

> ### 1.1电商项目基本业务概述

根据不同的应用场景，电商系统一般都提供了 PC 端、移动APP、移动Web、微信小程序等多种终端访问方式。

> ### 1.2电商后台管理的功能

电商后台管理系统用于管理用户账号、商品分类、商品信息、订单、数据统计等业务功能。

> ### 1.3电商后台管理的开发模式

电商后台管理系统整体采用**前后端分离**的开发模式，其中前端项目是基于**Vue 技术栈的 SPA 项目**

> ### 1.4电商后台管理系统的技术选型

#### 1.前端项目技术栈

* Vue
* Vue-router
* Element-UI
* Axios
* Echarts

#### 2.后端项目技术栈（了解）

* Node.js
* Express
* Jwt
* Mysql
* Sequelize

## 2.项目初始化

> ### 2.1前端项目初始化步骤

①安装Vue脚手架 npm install -g @vue/cli（**全局安装一次就好**）

②通过Vue脚手架创建项目(**推荐使用：vue  ui** )，点击右边的修改按钮，弹出输入框   输入f:  回车，就可以选择其他盘创建项目文件夹！

③配置Vue路由(**直接在vue ui 里面完成**)

④配置Element-UI 组件库(**在项目页面安装插件**)

⑤配置axios库（**在项目页面:选择依赖搜索axios**,选择运行依赖）（开发依赖：less-loader和less）

⑥初始化git远程仓库

⑦将本地项目托管到Github（**国外服务器**）或 码云 （**国内服务器**）中

```tex
使用window+R,输入cmd命令，开启终端；输入vue ui 开启可视化面板
创建新项目--功能：选择这四项（1.Babel  2.Router 3.Linter/Formatter 4.使用配置文件）
创建新项目--配置：选择  ESLint+standard config ;其他选择默认
然后创建项目即可，项目创建完成后！

....................安装element-ui插件.....................
在可视化面板--选择插件--添加插件：Element-ui(搜索：vue-cli-plugin-element);
然后配置插件(选择按需导入：import on demand)
.....................配置axios库.....................
在可视化面板-选择依赖--添加依赖：选择运行依赖（搜索：axios）


.....................................................
建议：在项目根目录，运行
	1.npm install -g @vue/cli（全局安装一次就好）
	2.vue ui (创建本地仓库)
		插件：element-ui
		依赖-运行依赖：axios
		依赖-开发依赖：less-loader和less



1.添加公钥步骤：
在git任意窗口，运行：
	ssh-keygen -t rsa -C "qianduanwd@163.com"  回车
	如果提示：.ssh/id_rsa already exists.  选择y
	按照提示完成三次回车，即可生成 ssh key。通过查看 ~/.ssh/id_rsa.pub 文件内容，全部复制
登录玛云账号--点击账号头像--设置--安全设置--SSH公钥--粘贴到这个位置

2.然后验证公钥是否可用：
  在git窗口，运行：
	ssh -T git@gitee.com
	提示：Hi 吴东! You've successfully authenticated  表示公钥可用！！！

3.登录玛云账号--创建仓库
选择左侧+，新建仓库：填写仓库名称（取消勾选使用Readme文件初始化这个仓库），其他保持默认。
然后选中git任意窗口，依次运行：
	git config --global user.name "吴东"
	git config --global user.email "qianduanwd@163.com"
	
4.在项目根目录打开窗口，运行：
	注意：这些git操作只是在本地操作git仓库
	git status
	git add . 把文件添加到暂存区
	git commit -m "add files"
	git status   此时应运行在master主分支

5.将本地仓库上传到玛云中，需要以下操作：
  在项目根目录，安装页面提示的代码依次运行：(类似下面的代码)
	git remote add origin https://gitee.com/wd_qianduan/vue_shop.git
	git push -u origin master  （关联本地仓库与云端仓库）
	
6.在玛云中查看创建的库，如果看到第一次的提示信息：add files，表示本地仓库成功上传玛云仓库！！！
  今后每做完一个功能，都需要上传玛云！！！
```

> ### 2.2后台项目的环境安装配置

①安装 MySQL 数据库

```tex
1.安装phpstudy服务器，只打开mysql即可。
	**其他选项菜单--服务管理器--Apache--停止
2.导入数据库保证API接口正常运行：
	找到这个文件：vue-api-server/db/mydb.sql
3.通过phpstudy执行mydb.sql文件：
	**选择MySQL管理器--Mysql导入导出：
	  密码：root
	  选择要还原的文件：选择这个文件路径 mydb.sql
	  还原数据库名：mydb
4.黑框关闭之后证明数据库导入完成，如何验证呢？
	其他选项菜单--MySQL工具--打开数据库目录--mydb文件夹:有内容，就证明数据库还原完成。
5.在vue-api-server文件夹下，窗口运行：
	npm install  安装依赖包
	node app.js  运行api接口
6.启动postman，进行测试：http://127.0.0.1:8888/api/private/v1/login
	请求方式：post
	接着传入两个参数：username:admin   password:123456  (注意打钩：√)
```



②安装 Node.js 环境

③配置项目相关信息

④**启动项目，运行npm run serve**

⑤使用 Postman 测试后台项目接口是否正常

## 3.登录/退出功能

> ### 3.1登录概述

#### 3.1-1.登录业务流程

①在登录页面输入用户名和密码

②调用后台接口进行验证

③通过验证之后，根据后台的响应状态跳转到项目主页

#### 3.1-2.登录业务的相关技术点

* http 是无状态的(需要记录用户的登录状态)	
  * 通过 cookie 在客户端记录状态
  * 通过 session 在服务器端记录状态
  * 通过 token 方式维持状态

> ### 3.2登录--token原理分析

```tex
1.如果前端和后台接口之间不存在跨域问题，推荐使用Cookie或者session记录登录状态。
2.如果前端和后台接口存在跨域问题，则使用token。
分析：token原理
	现在有客户端和服务器
	服务器：专门提供API接口。如登录接口
	客户端：需要通过ajax请求，访问服务器上的数据
	目前：客户端与服务器之间存在跨域问题
token原理：
1.客户端在登录页面输入用户名和密码，把这次请求提交到服务器。
2.服务器根据用户的这次请求验证用户是否存在。
  如果登录成功之后，服务器向客户端返回一个唯一的token值。
3.客户端需要把服务器返回的token值，记录到客户端本地。
4.今后如果客户端要请求服务器的API接口，必须携带token才能够正常的进行操作。
  如果客户端在发起下一次请求的时候，携带了token。
5.服务器接收到token之后，验证token是否存在：如果存在证明用户已登录
  然后会根据携带的token验证是哪个用户，从而根据用户的操作返回不同的结果。

注意事项：
1.token值是由服务器生成，而且每个不同的用户生成的token值也是不一样的。
2.token值记录了用户的登录状态
3.token：客户端与服务器端进行身份校验

```

> ### 3.3登录功能实现

#### 1.登录页面的布局

通过Element--UI组件实现布局

* el-form
* el-form-item
* el-input
* el-button
* 字体图标

```tex
找到自己的项目 vue_shop
打开vscode,在项目根目录vue_shop运行：git status
```

注意：在开发中只有开发新功能了，尽量把功能放在新的分支上进行开发；分支开发完成以后再把这个分支合并到master分支上

​	1.创建分支命令：git  checkout  -b  分支名

​	2.在项目根目录，运行：git  checkout  -b  login

​	3.查看所有分支，运行：git branch    分支前存在*     表示当前处于这个分支    *login

> #### 梳理vue项目的结构，删除不必要的内容

* 1.App.vue根组件

```js
<template>
  <div id="app">
    APP根组件
  </div>
</template>

<script>
export default {
  name: 'app'
}
</script>

<style>
</style>
```

* 2.路由  router.js

```js
import Vue from 'vue'              指的是引入vue.js文件
import Router from 'vue-router'
Vue.use(Router)                    Vue.use() 明确地安装路由功能

export default new Router({
    routes: [

    ]
})
```

* 3.删除views文件夹	 
* 4.删除components/HelloWorld.vue文件 

#### 功能：创建登录组件，通过路由的形式渲染到App根组件，添加路由重定向redirect

* 1.在components/新建登录组件：Login.vue

```js
<template>
    <div>
        登录组件
    </div>
</template>

<script>
export default {
    
}
</script>

<style lang="less" scoped>

</style>

注意：
1.lang="less"  支持less语法格式
2.scoped是vue的指令。控制组件样式生效的区间
	如果加上scoped，样式只在当前组件内生效
	如果去掉scoped，样式会全局生效

一个组件它的样式是来美化自己组件结构的，不应该影响其他的组件
所以：只要定义的是单文件组件，一定为style标签加上scoped指令
	  避免组件之间的样式冲突
```

* 2.在路由  router.js  导入路由--添加路由规则

```js
import Vue from 'vue'
import Router from 'vue-router'
import Login from './components/Login.vue'

Vue.use(Router)

export default new Router({
    routes: [{
        path: '/',
        redirect: '/login'
    }, {
        path: '/login',
        component: Login
    }]
})
```

* 3.在根组件 App.vue，添加路由占位符

```vue
<template>
  <div id="app">
    <!-- 路由占位符 -->
    <router-view></router-view>
  </div>
</template>
```

#### 功能：完成登录组件的基本页面布局:全屏背景色--登录的盒子

> 实现全屏背景色

* 1.在src/assets/新建css文件夹/新建global.css

```css
html,
body,
#app {
    height: 100%;
    margin: 0;
    padding: 0;
}
```

* 2.在入口文件main.js中导入全局样式表：import './assets/css/global.css'
* 3.在Login.vue中，为style标签添加  height: 100%;

```vue
<style lang="less" scoped>
   .login_container{
       height: 100%;
       background-color: #2b4b6b;
   }
</style>
```

> 登录的盒子 login_box

在Login.vue文件中：

```vue
<template>
    <div class="login_container">
        <div class="login_box">

        </div>
    </div>
</template>

<script>
export default {
    
}
</script>

<style lang="less" scoped>
   .login_container{
       height: 100%;
       background-color: #2b4b6b;
   }
   .login_box{
       width: 450px;
       height: 300px;
       background-color: #fff;
       border-radius: 3px;
       position: absolute;
       top: 50%;
       left: 50%;
       transform: translate(-50%,-50%)
   }
</style>

```

#### 功能：绘制图像区域  avatar_box

```vue
<template>
    <div class="login_container">
        <div class="login_box">
            <div class="avatar_box">
                <img src="../assets/logo.png" alt="">
            </div>
        </div>
    </div>
</template>

<script>
export default {
    
}
</script>

<style lang="less" scoped>
   .login_container{
       height: 100%;
       background-color: #2b4b6b;
   }
   .login_box{
       width: 450px;
       height: 300px;
       background-color: #fff;
       border-radius: 3px;
       position: absolute;
       top: 50%;
       left: 50%;
       transform: translate(-50%,-50%);

       .avatar_box{
           height: 130px;
           width: 130px;
           border: 1px solid #eee;
           border-radius: 50%;
           padding: 10px;
           box-shadow: 0 0 10px #ddd;
           position: absolute;
           left: 50%;
           transform: translate(-50%,-50%);
           background-color: #fff;
           img{
               width: 100%;
               height: 100%;
               border-radius: 50%;
               background-color: #eee;
           }
       }
   }
</style>
```

#### 功能：登录的表单区域

打开Element-UI官网，粘贴对应的html结构

因为我们的组件是按需导入的，所以如果用到form表单、input输入框等

* 1.需要先在src/plugins/element.js，引入相关的组件

```js
// 按需导入
import { Button } from 'element-ui'
import { Form, FormItem } from 'element-ui'
import { Input } from 'element-ui'

// 注册全局组件
Vue.use(Button)
Vue.use(Form)
Vue.use(FormItemon)
Vue.use(Input)
```

* 2.在Login.vue文件中： Form表单--Button按钮--Input输入框

```vue
<template>
    <div class="login_container">
        <div class="login_box">
            <!-- 头像区域 -->
            <div class="avatar_box">
                <img src="../assets/logo.png" alt="">
            </div>
            <!--登录表单区域 -->
            <el-form class="login_form">
                <!-- 用户名区域 -->
                <el-form-item>
                    <el-input></el-input>
                </el-form-item>
                <!-- 密码区域 -->
                 <el-form-item>
                    <el-input></el-input>
                </el-form-item>
                <!-- 按钮区域 -->
                <el-form-item class="btns">
                    <el-button type="primary">登录</el-button>
                    <el-button type="info">重置</el-button>
                </el-form-item>
            </el-form>
        </div>
    </div>
</template>

<script>
export default {
    
}
</script>

<style lang="less" scoped>
   .login_container{
       height: 100%;
       background-color: #2b4b6b;
   }
   .login_box{
       width: 450px;
       height: 300px;
       background-color: #fff;
       border-radius: 3px;
       position: absolute;
       top: 50%;
       left: 50%;
       transform: translate(-50%,-50%);

       .avatar_box{
           height: 130px;
           width: 130px;
           border: 1px solid #eee;
           border-radius: 50%;
           padding: 10px;
           box-shadow: 0 0 10px #ddd;
           position: absolute;
           left: 50%;
           transform: translate(-50%,-50%);
           background-color: #fff;
           img{
               width: 100%;
               height: 100%;
               border-radius: 50%;
               background-color: #eee;
           }
       }
   }
   .login_form{
       position: absolute;
       bottom: 0;
       width: 100%;
       padding: 0 20px;
       box-sizing: border-box;
   }
   .btns{
       display: flex;
       justify-content: flex-end;
   }
</style>
```

#### 功能：绘制密码和小图标

* 1.在Element-UI官网查找：输入框--带 icon 的输入框

```vue
 <el-input  prefix-icon="el-icon-search"></el-input>    el-icon-search 需要被替换为 iconfont icon-user
```

因为Element-UI官网找不到需要的图标，所以借助第三方图标库。

下载好之后，将字体图标文件fonts,放在assets文件夹里面      assets/fonts

* 2.然后在main.js导入

```js
// 导入字体图标
import './assets/fonts/iconfont.css'
```

* 3.在Login.vue中，iconfont  图标名

```vue
 <el-input prefix-icon="iconfont icon-user"></el-input>       用户头像
 <el-input prefix-icon="iconfont icon-3702mima"></el-input>   用户密码锁
```

#### 功能：实现表单的数据绑定(element文档提供的做法)

* 1.为el-form标签添加model 属性绑定到数据对象form     ：model = 'form'
* 2.为每一个表单项，通过v-model绑定到数据对象上的属性中

```VUE
<template>
    <div class="login_container">
        <div class="login_box">
            <!-- 头像区域 -->
            <div class="avatar_box">
                <img src="../assets/logo.png" alt="">
            </div>
            <!--登录表单区域 -->
            <el-form :model="loginForm" class="login_form">
                <!-- 用户名区域 -->
                <el-form-item>
                    <el-input v-model="loginForm.username" prefix-icon="iconfont icon-user">

                    </el-input>
                </el-form-item>
                <!-- 密码区域 -->
                 <el-form-item>
                    <el-input v-model="loginForm.password" prefix-icon="iconfont icon-3702mima" type="password">

                    </el-input>
                </el-form-item>
                <!-- 按钮区域 -->
                <el-form-item class="btns">
                    <el-button type="primary">登录</el-button>
                    <el-button type="info">重置</el-button>
                </el-form-item>
            </el-form>
        </div>
    </div>
</template>

<script>
export default {
    data(){
        return {
            // 这是登录表单的数据绑定对象
            loginForm: {
            username: 'wuddong',
            password: '123'
        }
        }
    }
}
</script>
```

#### 功能：表单的数据验证(这是element官网文档提供的做法)

* 为el-form标签通过绑定rules属性，指定校验对象(自定义)    :rules="loginFormRules"
* 在data数据中定义校验对象，其中每一个属性就是一个验证规则（数组）
* 为不同的表单el-form-item项,通过prop指定不同的验证规则进行表单验证

在Login.vue文件中：

```vue
第一步：<el-form :model="loginForm" :rules="loginFormRules" class="login_form"></el-form>

第二步：在data数据中

			// 这是表单的验证规则对象
			（required: true  表示必填项；trigger: 'blur' 表示鼠标离开进行验证）

            loginFormRules:{
                // 验证用户名是否合法
                username: [
                    { required: true, message: '请输入用户名', trigger: 'blur' },
                    { min: 3, max: 5, message: '长度在 3 到 5 个字符', trigger: 'blur' }
                ],
                // 验证密码是否合法
                password: [
                    { required: true, message: '请输入密码', trigger: 'blur' },
                    { min: 6, max: 15, message: '长度在 6 到 15 个字符', trigger: 'blur' }
                ]
            }

第三步：
用户名区域  <el-form-item prop="username"></el-form-item>
密码区域    <el-form-item prop="password"></el-form-item>
```

#### 功能：表单的重置---点击重置按钮，重置表单的效验--resetFields

```tex
Vue直接操作DOM

	1.通过ref标注DOM元素
    // 在DOM元素上通过ref属性标注，属性名称自定义  <div ref="info">hello</div>
    
    2.通过$refs获取DOM元素
    	// 通过Vue实例的$refs获取标记ref属性的元素
    	let info = this.$refs.info.innerHTML
    	console.log(info) // hello
```



方法：查询官方文档form--Form Methods   拿到表单的实例对象Form，调用resetFields函数。

* 为表单el-form添加ref引用，ref引用指定的值就是表单的引用对象loginFormRef

* 为重置按钮添加事件 @click="resetLoginForm"，触发resetLoginForm事件处理函数

* 在resetLoginForm事件处理函数中，通过this.$refs.表单的引用对象.resetFields()

  **在Login.vue文件中**

```vue

第一步：登录表单区域  <el-form ref="loginFormRef"> </el-form>
第二步：<el-button type="info" @click="resetLoginForm">重置</el-button>
第三步：在script标签定义methods方法
 methods:{
        // 点击重置按钮，重置登录表单
        resetLoginForm(){
            console.log(this); 
			//结果是组件的实例对象,里面有个属性$refs
            this.$refs.loginFormRef.resetFields();
        }
    }
```

#### 功能：实现登录前表单数据的预验证--validate

方法：查询官方文档form--Form Methods   拿到表单的引用对象，调用validate函数。

* 获取表单的引用对象loginFormRef

* 拿着引用对象loginFormRef，调用validate函数进行表单预校验；

  在validate中它接收一个回调函数，第一个形参是验证的结果：布尔值

  ```vue
  第一步：为登录按钮添加点击事件  <el-button type="primary" @click="login">登录</el-button>
  第二步：在script标签的methods方法中
   login(){
              this.$refs.loginFormRef.validate(valid=>{
                  console.log(valid);
  				
              })
          }
```
  
  

#### 功能：配置axios发起登录请求

1.如果要请求服务器：

- 启动MySql服务器(Phpstudy服务器)
- 找到素材/vue-api-server/app.js，在窗口启动：node  app.js

2.在main.js中：配置axios

```js
// 导入axios包
import axios from 'axios'
// 配置请求的根路径
axios.defaults.baseURL = 'http://127.0.0.1:8888/api/private/v1/'
// 把axios包挂载到vue原型对象上：这样每一个vue组件都可以通过this直接访问到$http，从而去发起ajax请求
Vue.prototype.$http = axios
```

3.根据验证的结果valid，判断是否发起登录请求

如果请求成功，Login.vue

* 请求方式：post
* 请求地址：login
* 请求参数：this.loginForm

```vue
  login(){
            this.$refs.loginFormRef.validate(async valid=>{
                console.log(valid); 
				//valid是布尔值：true 或者 false
				//******************内容如下：
                if(!valid) return;   不发起请求
                const {data: res} = await this.$http.post("login",this.loginForm);
                console.log(res);
                // {data: null, meta: {…}}
                if(res.meta.status !== 200) return console.log('登录失败');
                console.log('登录成功');
            })
        }
    }

因为post请求的结果是promise实例对象，所以在函数使用 await async
这样结果是:服务器返回的数据是一个对象：{data: {…}, status: 200, statusText: "OK", headers: {…}, config: {…}, …}
		  **es6语法：取对象里面的属性值**
	      我们只需要里面的data对象，所以结构复制出data属性重命名为res对象{data: res}  res就是data对应的属性值
然后根据res的meta属性，判断是否登录成功  res.meta.status !== 200
```

#### 功能：配置Message全局弹框组件

##### 需求：登录成功或者失败，给用户友好提示

配置方法：

* 从element-ui中导入弹框组件            import { Message } from 'element-ui'
* 把弹框组件挂载到vue的原型对象上  Vue.prototype.$message = Message  
* 调用$message提供的方法             

查看官方文档：Message消息提示

在plugins/element.js中,导入弹框提示组件：

```js
// 导入弹框提示组件
import { Message } from 'element-ui'
Vue.prototype.$message = Message  

注意：
1.$message是自定义属性
2.Vue.prototype.$message = Message  
  表示把弹框组件挂载到vue的原型对象上，这样每一个组件都可以通过this访问到$message
  然后就可以弹框提示了
  同时$message身上提供了一些弹框方法error('失败')、success('成功')
  我们只需要调用这些方法，提示需要的信息就可以了。
  
```

在Login.vue中，调用这些方法：

```vue
  登录成功：this.$message.error('登录失败')
  登录失败：this.$message.success('登录成功')
```

#### 2.实现登录

​	①通过 axios 调用登录验证接口

​	②登录成功之后保持用户 token 信息

​	③跳转到项目主页

在Login.vue中：

```vue
 this.$message.success('登录成功')
                // 1.将登录成功之后的token，保存到客户端的sessionStorage中
                //   localstorage   是持久化的存储机制
                //   sessionStorage 是会话期间的存储机制
                //      1.1 项目中除了登录之外的其他API接口，必须在登录之后才能访问
                //      1.2 token只应在当前网站打开期间生效，所以将token保存在sessionStorage中
        第一步： window.sessionStorage.setItem("token",res.data.token);
                // 2.通过编程式导航跳转到后台主页，路由地址是 /home
        第二步： this.$router.push('/home');
```

然后在components文件夹下，新建Home.vue

```vue
<template>
    <div>
        Home 组件
    </div>
</template>

<script>
export default {

}
</script>

<style lang="less" scoped>

</style>
```

接着在router.js导入home组件，添加路由规则

```js
// 导入home组件
import Home from './components/Home.vue'
// 添加路由规则
{ path: '/home',component: Home }
```

#### 3.路由导航守卫控制访问权限

需求：/home页面属于有权限的页面

1. 只有用户在登录的情况下才允许访问，如果是未登录状态是不允许看到home页面的
2. 如果用户没有登录，希望用户从home路径直接跳转到登录页

如果用户没有登录，但是直接通过URL访问特定页面，需要重新导航到登录页面

**在router.js中，添加路由导航守卫 router.beforeEach **

```js
 // 为路由对象，添加 beforeEach 函数(导航守卫) 
   to表示将要访问的页面路径；
   from表示从哪个路径跳转到哪个路径
   next表示放行的函数
   
 const router = new Router({})
 router.beforeEach((to, from, next) => {
   
   // 如果用户访问的登录页，直接放行允许访问登录页
   if (to.path === '/login') return next()
   // 如果访问的不是登录页，判断sessionStorage 中是否存在 token 值
   const tokenStr = window.sessionStorage.getItem('token')
   // 没有token，证明你没有登录，强制跳转到登录页
   
   if (!tokenStr) return next('/login')
   // 经过判断用户有token值，直接放行
   next()
 })
 
 export default router
 
 **通过用户访问的地址以及用户是否有token值，来决定用户具体访问的是哪个页面。**
```

### 退出功能实现原理

基于 token 的方式实现退出比较简单，只需要销毁本地的 token ,利用编程式导航--重新返回登录页面。

这样，后续的请求就不会携带 token ，必须重新登录生成一个新的 token 之后才可以访问页面。

在Home.vue组件中：

```tex
<template>
    <div>
       第一步：<el-button type="info" @click="logout">退出</el-button>
    </div>
</template>

<script>
	export default {
第二步：methods:{
        	logout(){
            	window.sessionStorage.clear();
            	this.$router.push("/login");
        	}
    	}
	}
</script>

<style lang="less" scoped>

</style>

```

#### 语法处理-处理项目中的ESLint语法报错问题

* 1.在项目根目录下，创建格式化文件  .prettierrc

```
{
    "semi": false,
    "singleQuote": true
}

说明：
	1. "semi": false        移除分号
	2. "singleQuote": true  用单引号表示字符串
```

* 2.依次在Login.vue/Home.vue文档中，点击右键--选择格式化文档
* 3.在.eslintrc.js中，添加一条规则

```js
'space-before-function-paren': 0   表示方法的()之前有一个空格
```

* 4.在UI页面：任务--重新运行--打开app

#### 语法处理--优化element--ui组件的按需导入形式

**element.js**

```js
将下面这些代码替换为一句代码
import { Button } from 'element-ui'
import { Form, FormItem } from 'element-ui'
import { Input } from 'element-ui'
// 导入弹框提示组件
import { Message } from 'element-ui'

合并为一句代码：
import { Button, Form, FormItem, Input, Message } from 'element-ui'
```

#### 登录退出--将本地代码提交到玛云

```tex
将本地的源代码先提交到云端仓储中进行保存
同时将本地的login分支也保存到了云端仓储中
今后只要是咱们写的源代码测试之后发现没问题，一定要先合并到主分支
然后再将主分支推送到云端仓储中，同时将子分支也推送到云端仓储中
```



在项目根目录运行，下面命令：

* git   status   查看状态
* git   add .     将所有内容放在暂存区
* git   commit -m "完成了登录"
* git   status   再次查看状态
* git  branch  查到当前处于哪个分支（如果当前处于login分支）
* git  checkout  master   切换到master分支
* git   branch   再次查看分支（是否处于master分支，确定切换到master分支后，进行合并操作）
* git   merge  login    将login分支合并到master分支，这样master分支里面也是最新的内容了
* git   push    将本地代码上传到玛云服务器
* git   branch
* git  checkout  login
* git  branch
* git  push  -u  origin  login   将本地的login子分支推送到云端origin仓储里面叫做login子分支进行保存

### 4.主页布局

#### 4.1实现基本的主页布局：先上下划分，再左右划分

首先在element.js中，导入组件 Container, Header, Aside, Main

```js
import { Container, Header, Aside, Main } from 'element-ui'
Vue.use(Container)
Vue.use(Header)
Vue.use(Aside)
Vue.use(Main)
```

在Home.vue中：

```vue
第一步：从element官方文档--Container布局容器--引入所需html结构
<template>
    <el-container class="home_container">
        <!-- 头部区域 -->
        <el-header>
            <el-button type="info" @click="logout">退出</el-button>
        </el-header>
        <!-- 页面主页区域 -->
        <el-container>
            <!-- 侧边栏 -->
            <el-aside width="200px">Aside</el-aside>
            <!-- 右侧内容主体 -->
            <el-main>Main</el-main>
        </el-container>
    </el-container>
</template>

<script>
export default {
  methods: {
    logout() {
      window.sessionStorage.clear()
      this.$router.push('/login')
    }
  }
}
</script>

第二步：设置相关样式
注意：element-UI中提供的组件，组件名称就是类名
     例如： .el-header{}  

<style lang="less" scoped>
	.home_container{
    	height: 100%;
	}
	.el-header{
    	background-color: #373d41;
	}
	.el-aside{
    	background-color: #333744;
	}
	.el-main{
    	background-color: #eaedf1;
	}
</style>

```

#### 4.2美化主页的header区域

在Home.vue中：

```vue
template部分：
 <el-header>
   第一步：添加div内容
   <div>
      <img src="../assets/heima.png" alt="">
      <span>黑马后台管理系统</span>
   </div>
   ...........................................................
   <el-button type="info" @click="logout">退出</el-button>
 </el-header>

第二步：为el-header标签添加样式
flex布局原理：通过给父盒子添加flex属性，来控制子盒子的位置和排列方式。
	1.fle-direction:设置主轴的方向
	2.justify-content：设置主轴上的子元素的排列方式
	3.align-items:设置侧轴上的子元素的排列方式（单行）
	4.align-content:设置侧轴上子元素的排列方式（多行）
......................................................................
.el-header{
    display: flex;                
    justify-content: space-between;  先两边贴边再平分剩余空间（默认x轴）
    padding-left: 0;
    align-items: center;  居中显示，垂直居中（默认y轴）
    color: #fff;
    font-size: 20px;
    div {
        display: flex;
        align-items: center;  居中显示，垂直居中（默认y轴）
        span {
            margin-left: 15px;
        }
    }
}

```

#### 实现导航菜单的基本结构:菜单分为二级，可以折叠

1. 在element.js导入组件：Menu,    MenuItem,   Submenu

```js
 import {
    Menu,
    MenuItem,
    Submenu
} from 'element-ui'

Vue.use(Menu)
Vue.use(MenuItem)
Vue.use(Submenu)
```

查询element官方文档--NavMenu导航菜单

2. 在Home.vue中：引入侧边栏的html结构

```vue
<!-- 侧边栏 -->
            <el-aside width="200px">
                <!-- 侧边栏内容区域 -->
                <el-menu
                    background-color="#333744"
                    text-color="#fff"
                    active-text-color="#ffd04b">
                        <!-- 一级菜单 -->
                        <el-submenu index="1">
                            <!-- 一级菜单的模板区域 -->
                            <template slot="title">
                                <!-- 一级图标 -->
                                <i class="el-icon-location"></i>
                                <!-- 一级文本 -->
                                <span>导航一</span>
                            </template>
                            <!-- 二级菜单 -->
                             <el-menu-item index="4">
                                <template slot="title">
                                    <!-- 一级图标 -->
                                    <i class="el-icon-location"></i>
                                    <!-- 一级文本 -->
                                    <span>导航一</span>
                                </template>
                            </el-menu-item>                          
                        </el-submenu>
                    </el-menu>
            </el-aside>
```

#### 4.3通过接口获取菜单数据

####      通过axios请求拦截器添加token,保证拥有获取数据的权限

API接口文档要求：需要授权的 API ，必须在请求头中使用 `Authorization` 字段提供 `token` 令牌

意思是：除了登录接口之外，其他所有接口必须授权才能正常调用，怎么授权呢？

​		调用登录接口--服务器端会返回登录成功的token令牌，这个令牌就是我们权限认证的字段

​         	在每一个请求头中添加`Authorization` 字段提供 `token` 令牌，想到了请求拦截器!!!

在main.js中：

```vue
只要通过axios向服务器端发送请求，必然会在发送请求期间优先调用use回调函数，会这次请求进行预处理
这次请求经过处理之后，才会发送到服务器进行真正的处理
// axios请求拦截   config是请求对象
  axios.interceptors.request.use(config => {
    // 为请求头对象，添加 Token 验证的 Authorization 字段
    config.headers.Authorization = window.sessionStorage.getItem('token')
    return config  表示对这次请求做了预处理
  })
........................................以上内容，放下下面代码的前面
// 把axios包挂载到vue实例对象的属性上
Vue.prototype.$http = axios

登录成功之后，查看network-login，查看请求头 Authorization：null 
原因：因为发起的是登录请求，你在登录期间服务器肯定没给你颁发令牌，默认是null
如果登录之后，调用其他接口，再去监听请求就会发现Authorization的值就是token值
这样服务器接收到这次请求，它会先判断Authorization是否符合要求，它才会给你响应。
如果不符合要求或者Authorization：null,服务器会驳回这次请求

```

#### 发起请求获取左侧菜单数据

在Home.vue中：

在页面刚被加载的时候，应该立即获取左侧菜单。所以调用生命周期函数created(){ }

```vue
<script>
export default {
    data(){
        return {
            // 左侧菜单数据
            menulist: []
        }
    },
    created(){
        this.getMenuList()
    },
  methods: {
    async getMenuList(){
        const {data: res} = await this.$http.get('menus')
        console.log(res); // {data: Array(5), meta: {…}}; 其中meta:{msg: "获取菜单列表成功", status: 200}
        if(res.meta.status!==200) return this.$message.error(res.meta.msg)
        this.menulist = res.data
    }
  }
}
</script>

```

#### 通过双重for循环渲染左侧菜单

实现思路：所有的一级菜单放在data数组中，也就是 menulist: [ ]。这个menulist数组中的每一项都是一个一级菜单

​		   每个一级菜单中通过children属性嵌套了所有的二级菜单。

​       		   所以如果要绘制左侧菜单，需要双重for循环：

​			外层for循环--渲染一级菜单

​			内层for循环--渲染二级菜单

#### 4.4动态渲染菜单数据并进行路由控制

* 通过 v-for 双层循环分别进行一级菜单和二级菜单的渲染
* 通过路由相关属性启用菜单的路由功能

```vue
 注意事项：
	1.数值和字符串拼接，得到的还是字符串。item.id + ''

<el-menu router>
  // 一级菜单
  <el-submenu :index="item.id + ''" v-for=“item in menulist" :key="item.id">
	// 一级菜单模板区域                                                                        
    <template slot="title">
	// 一级菜单文本                          
      <span>{{item.authName}}</span>
    </template>
	// 二级菜单                         
    <el-menu-item :index="subItem.id + '' " v-for="subItem in item.children"       
       :key="subItem.id" >
		// 二级菜单文本                        
       <span slot="title">{{subItem.authName}}</span>
    </el-menu-item>
  </el-submenu>
 </el-menu>
```

#### 为选中项设置字体颜色并添加分类图标

第一步：修改el-menu标签携带的颜色     active-text-color="#409Eff"

第二步：修改二级菜单的图标   <i class="el-icon-menu"></i>   （查看element官方文档--icon图标--所需图标名：el-icon-menu）

第三步：所有的一级菜单图标都不一样，需要借助第三方图标库!!!

​		每个一级菜单都是通过for循环动态生成，如何在动态生成一级菜单时，自动生成对应的图标呢？ 

​		* 解决方法：在data中先定义字体图标对象iconsObj:{ },以一级菜单的id作为键、id对应的图标作为值

```vue
1.在data数据中，添加iconsObj属性
iconsobj: {
                '125':'iconfont icon-user',
                '103':'iconfont icon-tijikongjian',
                '101':'iconfont icon-shangpin',
                '102':'iconfont icon-danju',
                '145':'iconfont icon-baobiao'
            }
2.每循环一次生成一个一级图标，然后绑定生成的id，从而显示对象的图标。
 <!-- 一级图标 -->
 <i :class="iconsobj[item.id]"></i>

3.图标与文本之间有一定的间距，每个图标都有一个类 iconfont
  在style标签中：
	.iconfont {
    	margin-right: 10px;
	}
```

#### 每次只能打开一个菜单项并解决边框问题

查看element文档--NavMenu导航菜单--Menu Attribute(菜单属性)--unique-opened(是否只保持一个子菜单的展开)

```vue
第一步：为el-menu标签添加属性绑定  :unique-opened="true" 或者 unique-opened
第二步：解决侧边栏右侧的边线对不齐的问题
.el-aside{
    background-color: #333744;
	.....................................解决方法如下：
    .el-menu{
        border-right: none;
    }
}
```

实现侧边栏的折叠和展开效果

在Home.vue中：

```vue
第一步：在侧边栏结构上面添加折叠与展开按钮  <div class="toggle_button">|||</div>
第二步：添加样式
.toggle_button{
    background-color: #4a5064;
    font-size: 10px;
    line-height: 24px;
    color: #fff;
    text-align: center;
    letter-spacing: 0.2em;
    cursor: pointer;
}
第三步：在data中定义
  	isCollapse:false   是否折叠
第四步：为el-menu标签，添加属性
  	:collapse="isCollapse"        动态控制展开和折叠效果  collapse默认为false
  	:collapse-transition="false"  取消折叠动画
第五步：为按钮绑定事件
	<div class="toggle_button" @click="toggleCollapse">|||</div>
	在methods方法中，定义事件：
	toggleCollapse(){
        this.isCollapse = !this.isCollapse
    }
第六步：动态控制侧边栏的展开范围
 	<el-aside :width="isCollapse?'64px':'200px'"></el-aside>
```

#### 实现首页路由的重定向

1. 定义Welcome.vue
2. 在Home.vue的Main的位置，放置路由占位符
3. 将welcome这个路由设置为home路由的子路由规则；这样在home页面中嵌套显示了welcome的子组件

```vue
第一步：在components下，新建组件 Welcome.vue
第二步：在Home.vue的Main的位置，放置路由占位符  <router-view></router-view>
第三步：在router.js导入 import Welcome from './components/Welcome.vue' 
	   添加路由规则
 		{
        	path: '/home',
        	component: Home,
        	redirect: '/welcome',       访问/home重定向到/welcome
			............................在home路由里面嵌套welcome路由规则，子路由规则用children：[{ }]
        	children: [{
            	path: '/welcome',
            	component: Welcome
        	}]
    	}
```

#### 实现侧边栏路由连接的改造

查询element官网--菜单属性--router(是否使用 vue-router 的模式，启用该模式会在激活导航时以 index 作为 path 进行路由跳转)

router默认值为false

```vue
在Home.vue文件中：
第一步：为el-menu标签开启路由模式 <el-menu :router="true"></el-menu>

第二步：以index属性当做跳转地址，因为path没有以斜线开头，所以手动拼接了斜线
		// 二级菜单
 	   <el-menu-item :index="'/'+ subItem.path" ></el-menu-item>
```

#### 通过路由的形式展示用户列表组件

```vue
第一步：在components下，新建user文件夹/新建Users.vue
第二步：在router.js中
	1.导入组件 import Users from './components/user/Users.vue'
	2.创建路由规则
	{
        path: '/home',
        component: Home,
        redirect: '/welcome',
        children: [{
            path: '/welcome',
            component: Welcome
        }, {
            path: '/users',   .........创建路由规则
            component: Users
        }]
    }

```

#### 实现左侧菜单高亮效果状态保持！在sessionStorage中保存左侧菜单

1. 在点击二级菜单链接的时候，把对应的地址保存在sessionStorage中
2. 当我们刷新页面的时候，从sessionStorage中取出保存的链接地址，动态的赋值给el-menu属性default-active="链接地址"

```vue
在Home.vue文件中：
第一步：为二级菜单绑定事件  <el-menu-item  @click="saveNavState('/'+ subItem.path)"></el-menu-item>
第二步：在methods方法中：
 // 保存链接的激活状态
    saveNavState(activePath){
        window.sessionStorage.setItem('activePath',activePath)  将链接地址保存在sessionStorage中
        this.activePath = activePath   点击不同链接的时候重新为activePath赋值，才能实现高亮效果的动态切换
    }
第三步：在data数据中定义被激活的链接地址    activePath: '' 

第四步：<el-menu :default-active="activePath"></el-menu>  
       default-active(当前激活菜单的index可以赋值给 default-active),接收的值是string

第五步：在script标签中：（点击不同链接的时候，重新为activePath赋值，让当前链接保持高亮！）
 created(){
     this.activePath = window.sessionStorage.getItem('activePath')  当home页面刚被刷新创建出来的时候
 }

```

### 4.用户列表功能开发

####  绘制用户列表组件的基本布局结构

1. 绘制了用户列表组件中的面包屑导航区域

2. 使用卡片视图组件，实现栅格布局:

   el-row列与列之间的间隙用:gutter指定        <el-row :gutter="20"> 

   el-col列占的宽度用 :span 指定  <el-col :span="10">

Users.vue

```vue
<template>
    <div>
        <!-- 面包屑导航区域 -->
        <el-breadcrumb separator-class="el-icon-arrow-right">
            <el-breadcrumb-item :to="{ path: '/home' }">首页</el-breadcrumb-item>
            <el-breadcrumb-item>用户管理</el-breadcrumb-item>
            <el-breadcrumb-item>用户列表</el-breadcrumb-item>
        </el-breadcrumb>
        <!-- 卡片视图区域 -->
        <el-card>
            <el-row :gutter="20">
                <el-col :span="10">
                    <!-- 搜索与添加区域 -->
                    <el-input placeholder="请输入内容">
                        <el-button slot="append" icon="el-icon-search"></el-button>
                    </el-input>
                </el-col>
                <el-col :span="4">
                    <el-button type="primary">添加用户</el-button>
                </el-col>
            </el-row>
        </el-card>
    </div>
</template>
```

在element.js引入对应的组件模块

```js
import {
    Breadcrumb,
    BreadcrumbItem,
    Card,
    Row,
    Col

} from 'element-ui'

Vue.use(Breadcrumb)
Vue.use(BreadcrumbItem)
Vue.use(Card)
Vue.use(Row)
Vue.use(Col)
```

global.css

```css
.el-breadcrumb {
    margin-bottom: 15px;
    font-size: 12px;
}

.el-card {
    box-shadow: 0 1px 1px rgba(0, 0, 0, 0.15)!important;
}
```

获取用户列表数据

- 请求路径：users

- 请求方法：get

- 请求参数

  * query  查询参数--可以为空
  * pagenum  当前页码--不能为空
  * pagesize  每页显示条数--不能为空

  

```vue
<script>
export default {
    data(){
        return {
            // 获取用户列表的参数对象
            queryinfo: {
                query: '',
                pagenum: 1,
                pagesize: 2
            },
            userlist: [],
            total: 0
        }
    },
    created(){
        this.getUserList()
    },
    methods: {
        async getUserList(){
            const {data: res} = await this.$http.get('users',{params: this.queryinfo})       **get请求用params传递参数**
            if(res.meta.status!==200){
                return this.$message.error('获取用户列表失败！')
            }
            this.userlist = res.data.users
            this.total = res.data.total
            console.log(res); 
        }
    }
}
</script>
```

#### 使用el-table组件渲染用户列表数据



```vue
在el-row标签下面，添加el-table标签
  1. :data="userlist" 绑定数据源  border 添加边框线    stripe 隔行变色
  2. <el-table-column label="姓名" prop="username"></el-table-column> 模板列
	label="姓名"      标题
	prop="username"   标题对应的内容
<el-table :data="userlist" border stripe>
   <el-table-column type="index"></el-table-column>  为表格添加索引列
   <el-table-column label="姓名" prop="username"></el-table-column>
   <el-table-column label="邮箱" prop="email"></el-table-column>
   <el-table-column label="电话" prop="mobile"></el-table-column>
   <el-table-column label="角色" prop="role_name"></el-table-column>
   <el-table-column label="状态" prop="mg_state"></el-table-column>
   <el-table-column label="操作"></el-table-column>
</el-table>

在global.css添加样式
.el-table {
    margin-top: 15px;
    font-size: 12px;
}
```

#### 为表格添加状态列的显示效果---如何将布尔值按需渲染为开关效果

方法：使用作用域插槽---作用域插槽的内容必须以template开头和结尾 同时通过slot-scope接收传递的数据

分析：状态这一列属于一个单元格，肯定属于这一行；只要我们拿到这一行的数据  {{scope.row}}显示这一行的数据

​	    就可以点出来状态具体的值 scope.row.mg_state ，此时就可以按需渲染状态的效果了!

```vue
<el-table-column label="状态"> 
   作用域插槽的内容必须以template开头和结尾 同时通过slot-scope接收作用域插槽的数据scope(自定义名称)  slot-scope="scope"
   <template slot-scope="scope">
     <el-switch v-model="scope.row.mg_state"></el-switch>
   </template>
</el-table-column>
```

#### 通过作用域插槽渲染操作列 

** element--button按钮(size属性)--Tooltip文字提示(enterable属性) **

分析：操作列并不对应我们的数据结构，操作列渲染成什么样子--所以完全由程序员说了算！

而且操作列必须拿到对应的id才能进行：修改用户 或者 删除用户；只能使用作用域插槽进行操作列的渲染。

```vue
 <el-table-column label="操作" width="180px">
                    <template slot-scope="scope">
                        <!-- 修改按钮 -->
                        <el-button type="primary" icon="el-icon-edit" size="mini"></el-button>
                        <!-- 删除按钮 -->
                        <el-button type="danger" icon="el-icon-delete" size="mini"></el-button>
                        <!-- 分配角色按钮 -->
                        <el-tooltip effect="dark" content="分配角色" placement="top" :enterable="false">
                            <el-button type="warning" icon="el-icon-setting" size="mini"></el-button>
                        </el-tooltip>
                    </template>
                </el-table-column>
```

#### 实现分页显示效果--Users.vue

** element--Pagination 分页**

```vue
1.在element.js导入分页组件
	import Pagination from 'element-ui'
	Vue.use(Pagination)
2.在el-table标签下面，添加分页<el-pagination></el-pagination>
 			<el-pagination
            @size-change="handleSizeChange"
            @current-change="handleCurrentChange"
            :current-page="queryinfo.pagenum"
            :page-sizes="[1, 2, 5, 10]"
            :page-size="queryinfo.pagesize"
            layout="total, sizes, prev, pager, next, jumper"
            :total="total">
            </el-pagination>

3.在methods方法中：
 		// 监听 pagesize 改变的事件
        handleSizeChange(newSize){
            console.log(newSize);
            // 获取当前每页显示多少条数据
            this.queryinfo.pagesize = newSize
            // 重新发送请求渲染页面
            this.getUserList()         
        },
        // 监听 页码值 改变的事件
        handleCurrentChange(newPage){
            console.log(newPage);
            this.queryinfo.pagenum = newPage
            // 重新发起请求获取数据
            this.getUserList()
        }

4.在global.css添加样式：
	.el-pagination {
    	margin-top: 15px;
	}
```

#### 修改用户状态

- 请求路径：users/:uId/state/:type
- 请求方法：put
- 请求参数
  * uId      用户 ID      不能为空`携带在url中`
  * type    用户状态   不能为空`携带在url中`，值为 true 或者 false
- 响应数据

```tex
{
  "data": {
    "id": 566,
    "rid": 30,
    "username": "admin",
    "mobile": "123456",
    "email": "bb@itcast.com",
    "mg_state": 0
  },
  "meta": {
    "msg": "设置状态成功",
    "status": 200
  }
}
```



** element--switch开关(change事件)**

用户状态的更改同步保存到数据中

1. 监听到switch开关状态的改变，拿到最新的状态
2. 调用对应的API接口，将最新的状态保存到数据库中

```vue
第一步：绑定change事件
<el-table-column label="状态">
   <template slot-scope="scope">
       <el-switch  @change="userStateChange(scope.row)"></el-switch>
   </template>
</el-table-column>

第二步：在methods方法中：                  
		// 监听 switch 开关状态的改变
        async userStateChange(userinfo){
            console.log(userinfo);
            const {data: res} = await this.$http.put(`users/${userinfo.id}/state/:{userinfo.mg_state}`)
            if(res.meta.status!==200){
                userinfo.mg_state = !userinfo.mg_state
                return this.$message.error('更新用户状态失败！')
            }
            this.$message.success('更新用户状态成功！')
        }

注意：两种写法
	${userinfo.id}   el表达式
 	:{userinfo.id}
```

#### 实现搜索功能

** input输入框--可清空---Input Events(clear)**

当用户在文本框输入不同的名称之后，点击按钮可以根据指定的名称搜索不同的用户

1. 将文本框与data中的数据，进行双向数据绑定
2. 为搜索按钮绑定点击事件，调用获取用户列表函数---进行数据查询

```vue
第一步：将文本框与data中的数据，进行双向数据绑定
	   点击清空按钮：文本框重置--所有的用户立即查询出来  clearable  @clear="getUserList"
	<el-input placeholder="请输入内容" v-model="queryinfo.query" clearable @clear="getUserList"></el-input>

第二步：为搜索按钮绑定点击事件，调用获取用户列表函数---进行数据查询 
	<el-button @click="getUserList"></el-button>
```

#### 渲染添加用户的对话框

1. 按需导入对话框组件


2. 在element文档中找到对话框组件对应的结构，粘贴到项目中
3. 梳理基本代码机构
   * title="提示"                                                             标题提示信息
   * :visible.sync="addDialogVisible"                         实现对话框的显示和隐藏
   * 点击按钮时，将addDialogVisible设置为false。 实现隐藏对话框

*** *Dialog对话框****

```vue
第一步：在element.js导入组件  
	import Dialog from 'element-ui' 
	Vue.use(Dialog)
第二步：在el-card标签下面，添加对话框结构
 <!-- 对话框区域 -->
        <el-dialog
        title="提示"
        :visible.sync="addDialogVisible"
        width="50%">
            <!-- 内容主体区域 -->
            <span>这是一段信息</span>
            <!-- 底部区域 -->
            <span slot="footer" class="dialog-footer">
                <el-button @click="addDialogVisible = false">取 消</el-button>
                <el-button type="primary" @click="addDialogVisible = false">确 定</el-button>
            </span>
        </el-dialog>

第三步：为添加用户按钮绑定事件  <el-button  @click="addDialogVisible=true">添加用户</el-button>

```

#### 渲染添加用户的表单

* el-form
  * :model="addForm"          数据绑定对象
  * :rules="addFormrules"    验证规则对象
  * ref="ruleFormRef"            引用对象
  * label-width="80px"           文本所占宽度
* el-form-item
  * label="用户名"                  指定文本的标题
  * prop="username"           指定具体的校验规则
* el-input
  * v-model="addForm.username"   数据的双向绑定，绑定在addForm表单数据对象上。（输入的数据都会同步到addForm中）

** Form表单**

```vue
第一步：在对话框的内容主体区域添加表单结构
<el-form :model="addForm" :rules="addFormrules" ref="ruleFormRef" label-width="80px">
    <el-form-item label="用户名" prop="username">
        <el-input v-model="addForm.username"></el-input>
    </el-form-item>
    <el-form-item label="密码" prop="password">
        <el-input v-model="addForm.password"></el-input>
    </el-form-item>
    <el-form-item label="邮箱" prop="email">
        <el-input v-model="addForm.email"></el-input>
    </el-form-item>
    <el-form-item label="手机" prop="mobile">
        <el-input v-model="addForm.mobile"></el-input>
    </el-form-item>
</el-form>

第二步：在data数据中，添加下面内容：

			// 添加用户的表单数据
            addForm: {
                username: '',
                password: '',
                email: '',
                mobile: ''
            },
            // 添加表单的验证规则对象
            addFormrules: {
                username: [
                    { required: true, message: '请输入用户名', trigger: 'blur' },
                    { min: 3, max: 10, message: '长度在 3 到 10 个字符', trigger: 'blur' }
                ],
                 password: [
                    { required: true, message: '请输入密码', trigger: 'blur' },
                    { min: 6, max: 15, message: '长度在 6 到 15 个字符', trigger: 'blur' }
                ],
                 email: [
                    { required: true, message: '请输入邮箱', trigger: 'blur' }
                   
                ], 
                mobile: [
                    { required: true, message: '请输入手机号', trigger: 'blur' }  
                ]
            }
```

#### 自定义邮箱和手机号的校验规则

1. 在data数据且return{ }前面，先定义一个箭头函数代表校验规则，为箭头函数起个名字！
2. 在具体的规则中，通过validator使用自定义的规则

** Form表单--自定义校验规则**

```vue
1.在data数据且return{ }前面，添加下面内容：		
		// 验证邮箱的规则
        var checkEmail = (rule, value, cb) => {
            // 验证邮箱的正则表达式
            const regEmail = /^([a-zA-Z0-9_-])+@([a-zA-Z0-9_-])+(\.[a-zA-Z0-9_-])+/

            if (regEmail.test(value)) {
                // 合法的邮箱
                return cb()
            }
            cb(new Error('请输入合法的邮箱'))
        }
        // 验证手机号的规则
        var checkMobile = (rule, value, cb) => {
            // 验证手机号的正则表达式
            const regMobile = /^(0|86|17951)?(13[0-9]|15[012356789]|17[678]|18[0-9]|14[57])[0-9]{8}$/

            if (regMobile.test(value)) {
                return cb()
            }
            cb(new Error('请输入合法的手机号'))
        }

2. 在校验规则对象中，添加
	email:[{ validator: checkEmail, trigger: 'blur'}]
	mobile:[{ validator: checkMobile, trigger: 'blur'}] 

```

#### 实现添加表单的重置操作

1. 监听对话框的关闭事件
2. 在关闭事件中，重置表单

```vue
第一步：为el-dialog标签添加close事件    <el-dialog @close="addDialogClosed"></el-dialog>

第二步：拿到表单的引用，调用resetfields方法

 		// 监听添加用户对话框的关闭事件
        addDialogClosed(){
            this.$refs.ruleFormRef.resetFields()
        }
```

#### 实现添加用户前的表单预校验

```vue
第一步：为确认按钮添加事件   <el-button @click="addUser">确 定</el-button>
第二步：在methods方法中
 addUser(){
            this.$refs.ruleFormRef.validate(valid=>{
				console.log(valid)
                if(!valid) return
                // 可以发起添加用户的网络请求
            })
        }

```

#### 调用接口完成添加用户的操作

- 请求路径：users
- 请求方法：post
- 请求参数
  * username   用户名称   不能为空
  * password    用户密码   不能为空
  * email            邮箱           可以为空
  * mobile         手机号        可以为空
- 响应数据

```vue
{
    "data": {
        "id": 28,
        "username": "tige1200",
        "mobile": "test",
        "type": 1,
        "openid": "",
        "email": "test@test.com",
        "create_time": "2017-11-10T03:47:13.533Z",
        "modify_time": null,
        "is_delete": false,
        "is_active": false
    },
    "meta": {
        "msg": "用户创建成功",
        "status": 201
    }
}
```

```vue
在methods方法中，添加下面代码内容：
addUser(){
            this.$refs.ruleFormRef.validate(async valid=>{
                console.log(valid);
                if(!valid) return
                // 可以发起添加用户的网络请求
                const {data: res} = await this.$http.post('users',this.addForm)
                if(res.meta.status!==201){
                    this.$message.error('添加用户失败！')
                }
                this.$message.success('添加用户成功！')
                // 隐藏获取用户列表数据
                this.getUserList()
                this.addDialogVisible=false
            })
        }
```

#### 展示修改用户的对话框

**Dialog对话框**

点击修改按钮弹出修改用户的对话框，在对话框中会预先把对话框的信息加载出来

用户名(只读)，邮箱、手机号，信息都会显示在弹出的对话框中，只允许用户修改邮箱和手机号

修改之后，如果通过了验证：点击确定按钮就会修改当前用户的信息

```vue
第一步：点击修改按钮添加点击事件，弹出修改的对话框  <el-button  @click="showEditDialog()"></el-button>
第二步：在methods方法中
		// 展示编辑用户的对话框
        showEditDialog(){
            this.editDialogVisible=true
        }
第三步：在添加用户对话框代码的下面，添加修改用户对话框
		<!-- 编辑用户对话框 -->
        <el-dialog
        title="修改用户"
        :visible.sync="editDialogVisible"    在data数据中定义 editDialogVisible=false
        width="50%"
        >
            <span>这是一段信息</span>
            <span slot="footer" class="dialog-footer">
                <el-button @click="editDialogVisible = false">取 消</el-button>
                <el-button type="primary" @click="editDialogVisible = false">确 定</el-button>
            </span>
        </el-dialog>
```

#### 根据ID查询对应的用户信息

- 请求路径：users/:id
- 请求方法：get
- 请求参数
  * id   用户 ID    不能为空`携带在url中`
- 响应数据

```vue
{
    "data": {
        "id": 503,
        "username": "admin3",
        "role_id": 0,
        "mobile": "00000",
        "email": "new@new.com"
    },
    "meta": {
        "msg": "查询成功",
        "status": 200
    }
}
```

```vue
第一步：传入id <el-button  @click="showEditDialog(scope.row.id)"></el-button>
第二步：根据id查询用户数据
 		// 展示编辑用户的对话框
        async showEditDialog(id){
            console.log(id);
            const {data: res} = await this.$http.get('users/'+id)
            if(res.meta.status!==200){
                return this.$message.error('查询用户信息失败！')
            }
            this.editForm = res.data          先在data数据中定义 editForm:{ }
            this.editDialogVisible=true
        }
```

#### 渲染修改用户的表单

** Form表单--表单验证**

```vue
1.在编辑用户内容的主体区域：
			<!-- 编辑用户的内容主体区域 -->
            <el-form :model="editForm" :rules="editFormRules" ref="editFormRef" label-width="70px">
                <el-form-item label="用户名">   用户名不需要验证规则，所以不需要prop属性
                    <el-input v-model="editForm.username" disabled></el-input>
                </el-form-item>
                 <el-form-item label="邮箱" prop="email">
                    <el-input v-model="editForm.email"></el-input>
                </el-form-item>
                 <el-form-item label="手机号" prop="mobile">
                    <el-input v-model="editForm.mobile"></el-input>
                </el-form-item>
            </el-form>

2.在data数据中：

			// 查询到的用户信息对象
            editForm: {
                username: '',
                email: '',
                password: ''
            },
            // 编辑用户的校验规则
            editFormRules: {
                email: [ 
                    { required: true, message: '请输入邮箱', trigger: 'blur' },
                    { validator: checkEmail, trigger: 'blur'}
                ],
                mobile: [
                    { required: true, message: '请输入手机号', trigger: 'blur' },
                    { validator: checkMobile, trigger: 'blur'} 
                ]
            }
```

#### 实现修改用户表单的重置操作

```vue
第一步：为编辑用户的对话框，添加close事件 <el-dialog @close="editDialogClosed"></el-dialog>
第二步：监听修改用户对话框的关闭事件
	editDialogClosed(){
         this.$refs.editFormRef.resetFields()
    }
```

#### 完成提交修改之前的表单预验证

点击确定按钮时，应该对用户输入的表单进行表单预验证，

验证通过之后才应该发起请求，进行真正的修改.

```vue
第一步：为确定按钮添加点击事件  <el-button  @click="editUserInfo">确 定</el-button>
第二步：在methods方法中
		// 修改用户信息并提交
        editUserInfo(){
            this.$refs.editFormRef.validate(valid=>{
                console.log(valid);
                if(!valid) return
                // 发起修改用户信息的数据请求
            })
        }

```

#### 提交表单完成用户信息的修改

- 请求路径：users/:id
- 请求方法：put
- 请求参数
  * id              用户 id     不能为空 `参数是url参数:id`
  * email        邮箱         可以为空
  * mobile      手机号     可以为空
- 响应数据

```vue
/* 200表示成功，500表示失败 */
{
    "data": {
        "id": 503,
        "username": "admin3",
        "role_id": 0,
        "mobile": "111",
        "email": "123@123.com"
    },
    "meta": {
        "msg": "更新成功",
        "status": 200
    }
}
```

```vue
		// 修改用户信息并提交
        editUserInfo(){
            this.$refs.editFormRef.validate(async valid=>{
                console.log(valid);
                if(!valid) return
                // 发起修改用户信息的数据请求
                const {data: res} = await this.$http.put('users/'+this.editForm.id,{
                    email: this.editForm.email,
                    mobile: this.editForm.mobile
                })
                if(res.meta.status!==200){
                    return this.$message.error('更新用户信息失败！')
                }
                // *1.关闭对话框
                this.editDialogVisible = false
                // *2.刷新数据列表
                this.getUserList()
                // *3.提示修改成功
                this.$message.success('更新用户信息成功！')
            })
        }
```

#### 删除数据--弹出对话框

** MessageBox弹框--确认消息--单独引用**

```vue
第一步：全局挂载MessageBox 
	import { MessageBox } from 'element-ui'
	Vue.prototype.$confirm = MessageBox.confirm  将MessageBox.confirm函数挂载到vue的原型对象上

第二步：根据id删除对应的用户信息
        async removeUserById(id){
            console.log(id);
            // 弹框询问用户是否删除数据..........单独引用内容如下：
            const confirmResult = await this.$confirm('此操作将永久删除该用户, 是否继续?', '提示', {
            confirmButtonText: '确定',
            cancelButtonText: '取消',
            type: 'warning'
            }).catch(err=>err)
            // 如果用户确认删除，则返回值为字符串  confirm
            // 如果用户取消删除，则返回值为字符串  cancel
            // console.log(confirmResult)
            if(confirmResult!=='confirm'){
                return this.$message.info('已取消删除')
            }
            console.log('确认了删除');
        }
```

#### 调用API完成删除用户的操作

- 请求路径：users/:id
- 请求方法：delete
- 请求参数
  * id     用户 id       不能为空`参数是url参数:id`
- 响应数据

```vue
{
    "data": null,
    "meta": {
        "msg": "删除成功",
        "status": 200
    }
}
```

```vue
 		将 console.log('确认了删除')  替换为下面的内容：

			const {data: res} = await this.$http.delete('users/'+ id)
            if(res.meta.status!==200){
                return this.$message.error('删除用户失败！')
            }
            this.$message.success('删除用户成功！')
            // 重新更新数据列表
            this.getUserList()
```

#### 提交代码--创建user子分支并把代码提交到玛云

```tex
在项目根目录运行：
	1. git branch  查看当前所在分支，发现在master分支！
	2. git checkout -b user  先创建子分支user，然后切换到user分支
	3. git branch  发现处于user分支，同时所有代码修改也切换到user子分支中
	4. git status
	5. git add .
	6. git status
	7. git commit -m "完成了用户列表功能的开发"
	8. git status
	9. git push -u origin user  将本地分支推送到origin仓储中，以user分支进行保存
	10.git branch
	11.git checkout master    先切换到master主分支             
	12.git merge user        将user里面所有的代码合并到master主分支,这样本地master里面的代码就是最新的
	13.git push 将本地的代码推送到玛云master分支，这样云端master里面的代码就是最新的

```

### 5.权限管理功能开发

#### 5.1创建rights子分支并推送到玛云

```tex
在项目根目录，运行：
	1. git branch   发现当前处于master,如果不是切换到master主分支
	2. git checkout -b rights  在master主分支下，创建rights子分支
	3. git branch   发现当前处于rights子分支
	4. git push -u origin rights  将rights分支推送到玛云中，让玛云也拥有rights子分支。
	                              这样接下来所有的功能都能下rights子分支下进行开发
	
```

#### 5.2权限列表-通过路由展示权限列表组件

```vue
第一步：在components文件夹下，新建power/新建Rights.vue

第二步：在router.js导入Rights组件  import Rights from './components/power/Rights.vue'
	
第三步：在home组件的children中，添加路由规则 { path: '/rights',component: Rights }
	
```

#### 5.3权限列表-绘制面包屑导航和卡片视图--Rights.vue组件

```vue
<template>
    <div>
        <!-- 面包屑导航区域 -->
        <el-breadcrumb separator-class="el-icon-arrow-right">
            <el-breadcrumb-item :to="{ path: '/home' }">首页</el-breadcrumb-item>
            <el-breadcrumb-item>用户管理</el-breadcrumb-item>
            <el-breadcrumb-item>用户列表</el-breadcrumb-item>
        </el-breadcrumb>
        <!-- 卡片视图 -->
        <el-card>123</el-card>
    </div>
</template>
```

#### 5.4权限列表-调用API接口获取权限列表数据--Rights.vue组件

- 请求路径：rights/:type
- 请求方法：get
- 请求参数
  * type     值 list 或 tree , list 列表显示权限, tree 树状显示权限,`参数是url参数:type`
- 响应参数
  * id    权限 ID
  * authName   权限说明
  * level      权限层级
  * pid       权限父 ID
  * path     对应访问路径
- 响应数据 type=list  (项目实际需要的是列表结构，所以 type=list)

```vue
data:{
    "data": [
        {
            "id": 101,
            "authName": "商品管理",
            "level": "0",
            "pid": 0,
            "path": null
        },
        {
            "id": 102,
            "authName": "订单管理",
            "level": "0",
            "pid": 0,
            "path": null
        }
    ],
    "meta": {
        "msg": "获取权限列表成功",
        "status": 200
    }
}
```

type=tree

```vue
  {
    data: [
      {
        id: 101,
        authName: '商品管理',
        path: null,
        pid: 0,
        children: [
          {
            id: 104,
            authName: '商品列表',
            path: null,
            pid: 101,
            children: [
              {
                id: 105,
                authName: '添加商品',
                path: null,
                pid: '104,101'
              }
            ]
          }
        ]
      }
    ],
    meta: {
      msg: '获取权限列表成功',
      status: 200
    }
  }
```

项目代码编写：

```vue
<script>
export default {
    data(){
        return {
            // 获取权限列表数据
            rightsList: []
        }
    },
    created(){
        // 发起请求获取列表数据
        this.getRightsList()
    },
    methods: {
        async getRightsList(){
            const {data: res} = await this.$http.get('rights/list')
            if(res.meta.status!==200){
                this.$message.error('请求列表数据失败！')
            }
            this.$message.success('请求列表成功！')
            this.rightsList = res.data 
        }
    }
}
</script>
```

#### 5.5权限列表-渲染权限列表UI结构

** Table表格--Tag标签**

```vue
第一步：在element.js中，导入Tag组件
	import Tag from 'element-ui'
	Vue.use(Tag)

第二步：添加表格结构
		<!-- 卡片视图 -->
        <el-card>
            <el-table
            :data="rightsList"
            border
            stripe>
                <el-table-column type="index"></el-table-column>
                <el-table-column prop="authName" label="商品管理"></el-table-column>
                <el-table-column prop="path"  label="路径"></el-table-column>
                <el-table-column prop="level" label="权限等级">
                  	....................................自定义权限等级这一列，所以通过作用域插槽自定义输出格式
                    <template slot-scope="scope">
                        <el-tag v-if = "scope.row.level==='0'">一级</el-tag>
                        <el-tag type="success" v-else-if = "scope.row.level==='1'">二级</el-tag>
                        <el-tag type="warning" v-else>三级</el-tag>
                    </template>
                </el-table-column>
            </el-table>
        </el-card>
```

### 6.角色功能开发

#### 6.1介绍用户-角色-权限 三者之间的关系

通过权限管理模块控制不同的用户可以进行哪些操作，具体可以通过角色的方式进行控制，

即每个用户分配一个特定的角色，角色包括不同的功能权限。

```tex
把用户绑定了不同的角色，角色下拥有不同的权限
只要用户拥有这个角色，就必然拥有这个角色下的权限
```

#### 6.2角色列表-通过路由展示角色列表组件--Roles.vue

```vue
第一步：在components/power下，新建Roles.vue组件

第二步：在router.js导入Roles.vue组件   import Roles from './components/power/Roles.vue'

第三步：在home的children中添加路由规则  { path: '/roles',component: Roles }

```

#### 6.3角色列表-绘制基本布局结构--Roles.vue

- 请求路径：roles

- 请求方法：get

- 响应数据说明

  - 第一层为角色信息


  - 第二层开始为权限说明，权限一共有 3 层权限
  - 最后一层权限，不包含 `children` 属性

- 响应数据

```vue
{
    "data": [
        {
            "id": 30,
            "roleName": "主管",
            "roleDesc": "技术负责人",
            "children": [
                {
                    "id": 101,
                    "authName": "商品管理",
                    "path": null,
                    "children": [
                        {
                            "id": 104,
                            "authName": "商品列表",
                            "path": null,
                            "children": [
                                {
                                    "id": 105,
                                    "authName": "添加商品",
                                    "path": null
                                }
                            ]
                        }
                    ]
                }
            ]
        }
    ],
    "meta": {
        "msg": "获取成功",
        "status": 200
    }
}
```

项目代码：

```vue
 		第一步：在template标签中
		<!-- 卡片视图 -->
        <el-card>
            <!-- 添加角色按钮区域 -->
            <el-row>
                <el-col>
                    <el-button type="primary">添加角色</el-button>
                </el-col>
            </el-row>
            <!-- 角色列表区域 -->
        </el-card>

第二步：在script标签中
<script>
export default {
    data(){
        return {
          // 角色列表数据
            rolesList: []
        }
    },
    created(){
        this.getRolesList()
    },
    methods: {
        // 获取所有角色的列表
        async getRolesList(){
            const {data: res} = await this.$http.get('roles')
            if(res.meta.status!==200){
                return this.$message.error('请求角色数据失败！')
            }
            this.rolesList = res.data
        }
    }
}
</script>

```

#### 6.4角色列表-渲染角色列表数据

** Button按钮--图标按钮**

```vue
			<!-- 角色列表区域 -->
            <el-table :data="rolesList" border stripe>
                <!-- 角色拓展 -->
                <el-table-column type="expand"></el-table-column>
                <!-- 角色索引 -->
                <el-table-column type="index"></el-table-column>
                <el-table-column label="角色名称" prop="roleName"></el-table-column>
                <el-table-column label="角色描述" prop="roleDesc"></el-table-column>
                <el-table-column label="操作" width="300px">
                    <template slot-scope="scope">
                        <el-button size="mini" type="primary" icon="el-icon-edit">编辑</el-button>
                        <el-button size="mini" type="danger" icon="el-icon-delete">删除</el-button>
                        <el-button size="mini" type="warning" icon="el-icon-setting">分配角色</el-button>
                    </template>
                </el-table-column>
            </el-table>
```

#### 6.5编辑和删除，自己做

#### 6.6角色列表-分析角色下权限渲染的实现思路

```tex
1.通过作用域插槽 scope.row拿到角色数据

2.通过.children拿到所有的一级权限，通过第一次for循环把一级权限渲染为tag标签
  让一级权限独占一行：左边5列(el-col)交给一级权限使用；右边剩余19列(el-col)交给二级和三级权限使用
  
3.在第一层for循环中嵌套第二层for循环，渲染所有的二级权限；同时也为二级权限添加el-row
  左边6列(el-col)交给二级权限使用，剩余的18列(el-col)渲染为三级权限
```



1. 通过scope.row拿到角色信息
2. 通过三层for循环：
   * 最外层for循环，渲染一级权限
   * 中间的for循环，渲染二级权限
   * 最后的for循环，渲染三级权限

#### 6.7角色列表-通过第一层for循环渲染一级权限；角色列表-美化一级权限的UI结构

** icon图标**

```vue
				<!-- 展开列 -->
                <el-table-column type="expand">
                    <template slot-scope="scope">
                        <el-row :class="['bdbottom',i1===0?'bdtop':'']"   ...........为el-row标签添加class类
                                v-for="(item1,i1) of scope.row.children" :key="item1.id">
                            <!-- 渲染一级权限 -->
                            <el-col :span="5">
                                <el-tag>{{item1.authName}}</el-tag>
                                <i class="el-icon-caret-right"></i>       ...................添加图标  
                            </el-col>
                            <!-- 渲染二级和三级权限 -->
                            <el-col :span="19"></el-col>
                        </el-row>
                        <pre>
                            {{scope.row}}
                        </pre>
                    </template>
                </el-table-column>

..............................................................美化样式
<style lang="less" scoped>
    .el-tag {
        margin: 7px;
    }
    .bdtop {
        border-top: 1px solid #eee;
    }
    .bdbottom {
        border-bottom: 1px solid #eee;
    }
</style>
```

#### 6.8角色列表-通过第二层for循环渲染二级权限

```vue
							<!-- 渲染二级和三级权限 -->
                            <el-col :span="19">
                                <!-- 通过for循环 嵌套渲染二级权限 -->
                                <el-row :class="[i2===0?'':'bdtop']" 
                                v-for="(item2,i2) of item1.children" :key="item2.id">
                                    <el-col>
                                        <el-tag type="success">{{item2.authName}}</el-tag>
                                        <i class="el-icon-caret-right"></i>
                                    </el-col>
                                    <el-col></el-col>
                                </el-row>
                            </el-col>
```

#### 6.9角色列表-通过第三层for循环渲染三级权限

```vue
							<!-- 渲染二级和三级权限 -->
                            <el-col :span="19">
                                <!-- 通过for循环 嵌套渲染二级权限 -->
                                <el-row :class="[i2===0?'':'bdtop']" 
                                v-for="(item2,i2) of item1.children" :key="item2.id">
                                    <el-col :span="6">
                                        <el-tag type="success">{{item2.authName}}</el-tag>
                                        <i class="el-icon-caret-right"></i>
                                    </el-col>
                                    <el-col :span="18">
                                        <!-- 通过for循环 渲染三级权限 -->
                                        <el-tag type="warning" 
                                        v-for="(item3,i3) of item2.children"
                                        :key="item3.id">{{item3.authName}}</el-tag>
                                    </el-col>
                                </el-row>
                            </el-col>
```

#### 6.10角色列表-美化角色下权限的UI结构

```vue
1.缩小页面视图，保持页面结构不乱！
  解决方法：给整个页面添加最小宽度，在global.css   #app{ min-width: 1366px }

2.让标签在页面垂直居中
  在Roles.vue中的style标签添加样式
   	.vcenter {
        display: flex;
        align-items: center;
    }

3.为el-row标签添加  vcenter类名

```

#### 6.11角色列表-点击删除权限按钮弹出确认提示框

** Tag标签--可移除标签--Events(close);MessageBox弹框--确认消息**

```vue
1.在通过for循环 渲染三级权限 el-tag标签添加：
	closable  每个标签后面有删除×标记
	@close="removeRightById()  添加删除事件

2.在methods方法中：
		// 根据id删除对应的权限
        async removeRightById(){
            // 弹框提示用户是否要删除
            const confirmResult = await this.$confirm('此操作将永久删除该文件, 是否继续?', '提示', {
            confirmButtonText: '确定',
            cancelButtonText: '取消',
            type: 'warning'
            }).catch(err=>err)
            if(confirmResult!=='confirm'){
                return this.$message.info('取消了删除')
            }
            console.log('确认了删除！');
            
        }
```

#### 6.12角色列表-完成删除角色下指定权限的功能

- 请求路径：roles/:roleId/rights/:rightId
- 请求方法：delete
- 请求参数
  * :roleId    角色 ID     不能为空`携带在url中`
  * :rightId   权限 ID     不能为空`携带在url中`
- 响应数据说明
  * 返回的data, 是当前角色下最新的权限数据
- 响应数据

```vue
{
    "data": [
        {
            "id": 101,
            "authName": "商品管理",
            "path": null,
            "children": [
                {
                    "id": 104,
                    "authName": "商品列表",
                    "path": null,
                    "children": [
                        {
                            "id": 105,
                            "authName": "添加商品",
                            "path": null
                        },
                        {
                            "id": 116,
                            "authName": "修改",
                            "path": null
                        }
                    ]
                }
            ]
        }
    ],
    "meta": {
        "msg": "取消权限成功",
        "status": 200
    }
}
```

项目代码内容：

```vue
1.在点击事件中传入参数  @close="removeRightById(scope.row,item3.id)"
2.将 console.log('确认了删除！') 替换为下面的代码内容：
			const {data: res} = await this.$http.delete(`roles/${role.id}/rights/${rightId}`)
            if(res.meta.status!==200){
                return this.$message.error('删除权限失败！')
            }
            // 为防止删除权限之后，页面会自动合起来，把服务器返回的最新的权限直接赋值给当前角色的children属性
            // 防止整个列表的刷新 this.getRolesList()，提高用户的体验！ 
            role.children = res.data

3.为一级el-tag标签添加 
	closable
	@close="removeRightById(scope.row,item1.id)"

4.为二级el-tag标签添加
	closable
	@close="removeRightById(scope.row,item2.id)"
	
```

#### 6.13分配权限-弹出分配权限对话框并请求权限数据；获取所有权限数据

- 请求路径：rights/:type
- 请求方法：get
- 请求参数
  * type      值 list 或 tree , list 列表显示权限, tree 树状显示权限,`参数是url参数:type`
- 响应参数
  * id
  * authName
  * level
  * pid
  * path
- 响应数据 type=tree(项目需要响应数据呈现树状结构)

```vue
  {
    data: [
      {
        id: 101,
        authName: '商品管理',
        path: null,
        pid: 0,
        children: [
          {
            id: 104,
            authName: '商品列表',
            path: null,
            pid: 101,
            children: [
              {
                id: 105,
                authName: '添加商品',
                path: null,
                pid: '104,101'
              }
            ]
          }
        ]
      }
    ],
    meta: {
      msg: '获取权限列表成功',
      status: 200
    }
  }
```



** Dialog对话框**

1. 点击分配权限按钮，弹出分配权限对话框；同时获取分配权限的数据

```vue
第一步：为分配权限按钮添加事件   @click="showSetRightDialog"

第二步：定义分配权限的事件showSetRightDialog
		// 展示分配权限的对话框
        async showSetRightDialog(){
            // 获取所有权限的数据
            const {data: res} = await this.$http.get('rights/tree')
            if(res.meta.status!==200){
                return this.$message.error('获取所有权限失败！')
            }
            // 把获取到的权限数据保存到data数据中
            this.rightslist = res.data
            this.setRightDialogVisible = true
        }
```

#### 6.14分配权限-初步配置并使用el-tree控件

** Tree树形控件**

1. 通过:data绑定数据源     :data="rightslist" 
2. 通过 :props指定树形绑定对象  :props="treeProps"
   *  label        看到哪个属性对应的值                   label: 'authName'
   *  children   父子节点通过哪个属性实现嵌套    children: 'children'

```vue
第一步：在element.js中，导入el-tree组件
	import Tree from 'element-ui'
	Vue.use(Tree)

第二步：引入树形控件
 			<!-- 树形控件 -->
            <el-tree 
            :data="rightslist" 
            :props="treeProps"></el-tree>

第三步：在data数据中
			// 树形控件的属性绑定对象
            treeProps: {
                label: 'authName',
                children: 'children'
            }
```

#### 6.15分配权限-优化树形控件的展示效果

** Tree树形控件--Attributes:(node-key,default-expand-all)**

```vue
第一步：为每个树形控件添加复选框   
	解决方法：为树形控件el-tree控件添加属性  show-checkbox

第二步：为每一个节点默认选中这一项对应的id值
	解决方法：为树形控件el-tree控件添加   node-key = "id"

第三步：打开对话框，要求打开树形结构的所有节点
	解决方法：为树形控件el-tree控件添加   default-expand-all

```

#### 6.16分配权限-分析已有权限默认勾选的实现思路；加载当前角色已有的权限   (不懂！！！)

1. 点击分配权限按钮的同时，获取当前角色三级权限的id，将id放在数组中

​       并且将数组通过属性绑定交给 default-checked-keys

2. 定义一个递归函数，将角色信息传入递归函数中，通过递归的形式将三级节点的id保存在数组中

   将这个数组赋值给defKeys数组，就能够实现点击分配权限的时候，把那些已有的权限加载出来！



** Tree树形控件--Attributes:(default-checked-keys)**

```vue

```

#### 6.17分配权限-在关闭对话框时重置defKeys数组

每次点击分配权限按钮，都会把当前角色已有的三级权限id保存到数组中

但是我们关闭对话框的时候并没有清空数组，导致长此以往数组中的id越来越多

为防止这个bug，我们应该在每次对话框关闭期间都清空一个数组里面的内容

```vue
第一步：为分配权限的对话框添加事件  @click="setRightDialogClosed"

第二步：在methods方法中
	// 监听分配权限对话框的关闭事件
        setRightDialogClosed(){
            this.defKeys=[]
        }
```

#### 6.18分配权限-调用API完成分配权限的功能

- 请求路径：roles/:roleId/rights
- 请求方法：post
- 请求参数：通过 `请求体` 发送给后端
  * :roleId       角色 ID                    不能为空`携带在url中`
  * rids     权限 ID 列表(字符串)    以 `,` 分割的权限 ID 列表（获取所有被选中、叶子节点的key和半选中节点的key, 包括 1，2，3级节点）
- 响应数据

```vue
{
    "data": null,
    "meta": {
        "msg": "更新成功",
        "status": 200
    }
}
```

思路：

1. 点击分配权限按钮时，立即把当前角色的id保存在data中，以便后续使用！
2. 点击确认按钮的时候，拿到树形结构的引用
3. 分别调用getCheckedKeys 和 getHalfCheckedKeys函数，就可以获取选中节点的id数组和半选中节点的id数组
4. 然后将两个数组合并为一个新的数组，将这个数组以逗号进行字符串拼接
5. 然后发起post请求：将保存的角色id和拼接的id字符串发送到服务器端
6. 如果请求失败，则提示：分配权限失败
7. 否则就提示：分配权限成功--刷新角色权限列表--关闭分配角色权限的对话框

```vue
第一步：在data数据中定义当前即将分配权限的角色id           roleId: ''

第二步：在showSetRightDialog函数中，将角色id传入roleId    this.roleId = role.id

第四步：为确定按钮添加点击事件  @click="allotRights"

第五步：在methods方法中
		// 点击为角色分配权限;使用展开运算符将两个数组合并为一个新的数组
        allotRights(){
            const Keys = [
                ...this.$refs.treeRef.getCheckedKeys(),
                ...this.$refs.treeRef.getHalfCheckedKeys()
            ]
            console.log(Keys);
            // 以，号拼接字符串
            const idStr = Keys.join(',')
            const {data: res} = await this.$http.post(`roles/${this.roleId}/rights`,{rids: idStr})
            if(res.meta.status!==200){
                return this.$message.error('分配权限失败！')
            }
            this.$message.success('分配权限成功！')
            // 刷新获取角色权限列表
            this.getRolesList()
            // 关闭分配权限对话框
            this.setRightDialogVisible = false
        }
```

#### 完善用户列表中分配角色的功能--Users.vue组件

#### 角色列表

- 请求路径：roles

- 请求方法：get

- 响应数据说明

  - 第一层为角色信息


  - 第二层开始为权限说明，权限一共有 3 层权限
  - 最后一层权限，不包含 `children` 属性

- 响应数据

```vue
{
    "data": [
        {
            "id": 30,
            "roleName": "主管",
            "roleDesc": "技术负责人",
            "children": [
                {
                    "id": 101,
                    "authName": "商品管理",
                    "path": null,
                    "children": [
                        {
                            "id": 104,
                            "authName": "商品列表",
                            "path": null,
                            "children": [
                                {
                                    "id": 105,
                                    "authName": "添加商品",
                                    "path": null
                                }
                            ]
                        }
                    ]
                }
            ]
        }
    ],
    "meta": {
        "msg": "获取成功",
        "status": 200
    }
}
```



** Dialog对话框**

```vue
第一步：在Users.vue中，将对话框结构复制粘贴到修改用户对话框的下面

第二步：在data中定义控制分配角色对话框的显示与隐藏  setRoleDialogVisible: false

第三步：为分配角色的el-button按钮，添加事件  @click="setRole(scope.row)"

第四步：在methods中定义
// 展示分配角色的对话框
 setRole(userInfo){
            this.userInfo=userInfo
            this.setRoleDialogVisible=true    点击分配角色按钮--显示对话框的同时显示用户的基本信息
 }
第五步：在data的return中，定义需要被分配角色的用户信息  userInfo: {}

第六步：将分配角色的用户信息展示在页面上---下面代码放在分配角色对话框的内容区域

 <div>
    <p>当前的用户：{{userInfo.username}}</p>
    <p>当前的角色：{{userInfo.role_name}}</p>
 </div>

第七步：在data的return中，定义所有角色的数据列表 rolesList:[]

第八步：调用接口获取所有角色列表
		// 展示分配角色的对话框
        async setRole(userInfo){
            this.userInfo=userInfo
            // console.log(this.userInfo);

            // 在展示对话框之前，获取所有角色的列表
            const {data: res} = await this.$http.get('roles')
            if(res.meta.status!==200){
                return this.$message.error('获取角色列表失败！')
            }
            // 将角色列表保存在页面数据中，首先在data中定义 rolesList:[]
            this.rolesList = res.data

            this.setRoleDialogVisible=true
        }

第九步：拿到角色的数据列表 rolesList:[] 之后，将这个数组渲染成页面的下拉菜单
```

#### 分配角色--渲染角色列表的select下拉菜单

* 通过v-model双向绑定到具体的值上
* 所有选项通过for循环生成      v-for="item in rolesList"     循环第九步拿到角色的数据列表 rolesList:[]
  *  :label      用户看到的文本
  *  :value     才是真正选中的值

** Select选择器**

```vue
第十步：在element.js导入 Select/Option组件

第十一步：在data的return中，定义已选中的角色ID值 selectedRoleId: ''

第十二步：赋值粘贴select结构，放在分配角色对话框的内容区域
 			<div>
               <p>当前的用户：{{userInfo.username}}</p>
               <p>当前的角色：{{userInfo.role_name}}</p>
               <P>分配新角色：
                    <el-select v-model="selectedRoleId" placeholder="请选择">
                        <el-option
                        v-for="item in rolesList"
                        :key="item.id"
                        :label="item.roleName"
                        :value="item.id">
                        </el-option>
                    </el-select>
               </P>
           </div>

```

#### 分配用户角色

- 请求路径：users/:id/role
- 请求方法：put
- 请求参数
  * id      用户 ID    不能为空`参数是url参数:id`
  * rid    角色 id     不能为空`参数body参数`
- 响应数据

```vue
{
    "data": {
        "id": 508,
        "rid": "30",
        "username": "asdf1",
        "mobile": "123123",
        "email": "adfsa@qq.com"
    },
    "meta": {
        "msg": "设置角色成功",
        "status": 200
    }
}
```

```vue
第十三步：为分配角色对话框的确定按钮绑定事件处理函数  <el-button  @click="saveRoleInfo">确 定</el-button>
第十四步：在methods方法中，定义saveRoleInfo
 		// 点击按钮，分配角色
        async saveRoleInfo(){
            if(!this.selectedRoleId){
                return this.$message.error('请选择要分配的角色')
            }
            const {data: res} = await this.$http.put(`users/${this.userInfo.id}/role`,{
                rid: this.selectedRoleId
            })
            console.log(res);
            
            if(res.meta.status!==200){
                return this.$message.error('更新角色失败！')
            }
            // 1.更新角色成功提示
            this.$message.success('更新角色成功！')
            // 2.刷新当前用户列表
            this.getUserList()
            // 3.隐藏分配角色的对话框
            this.setRoleDialogVisible=false
        }

第十五步：为分配角色的对话框el-dialog，添加close事件   @close="setRoleDialogClosed"

第十六步：在methods方法中，定义setRoleDialogClosed
 	// 监听分配角色对话框的关闭事件
        setRoleDialogClosed(){
            // 1.重置已选中的角色ID值
            this.selectedRoleId=''
            // 2.重置需要被分配角色的用户信息
            this.userInfo={}
        }
```

#### 分支操作-提交本地代码到玛云

```tex
在项目根目录，运行：
	1.git branch   查看当前所处分支，发现当前处于rights子分支
	2.git add .
	3.git commit -m "完成了权限功能的开发"
	4.git push      将本地的rights分支提交到玛云的rights分支
	5.git checkout master  首先在切换到master主分支
    6.git merge rights     然后将rights分支中的代码合并到master主分支，此时本地的master主分支中的代码是最新的代码
    7.git push             将本地的master分支中的代码推送到云端master主分支进行保存
```

### 分类管理

#### 1.商品分类--创建goods_cate子分支并推送到玛云

```tex
在项目根目录，运行：
	1.git branch                    	查看当前所处分支，发现当前处于master主分支。如果不是要切换到master主分支
	2.git checkout -b  goods_cate   	在master主分支上，创建goods_cate子分支
	3.git branch        				发现当前处于goods_cate子分支
	4.git push -u origin  goods_cate    将goods_cate子分支推送到玛云仓库中
```

#### 2.商品分类-通过路由加载商品分类组件

```vue
第一步:在components下，新建goods文件夹/新建Cate.vue
第二步：在router.js导入Cate.vue组件
第三步：在home组件的children属性中，加载路由规则 { path: '/categories',component: Cate }
```

#### 3.商品分类-绘制商品分类组件的基本页面布局--Cate.vue

```vue
在template标签中，添加下面代码：
	<div>
        <!-- 面包屑导航区域 -->
        <el-breadcrumb separator-class="el-icon-arrow-right">
            <el-breadcrumb-item :to="{ path: '/home' }">首页</el-breadcrumb-item>
            <el-breadcrumb-item>分类管理</el-breadcrumb-item>
            <el-breadcrumb-item>分类列表</el-breadcrumb-item>
        </el-breadcrumb>
        <!-- 卡片视图 -->
        <el-card>
            <el-row>
                <el-col>
                    <el-button type="primary">添加分类</el-button>
                </el-col>
            </el-row>
            <!-- 表格 -->

            <!-- 分页 -->
        </el-card>
    </div>
```

#### 4.商品分类-调用API获取商品分类列表数据

- 请求路径：categories
- 请求方法：get
- 请求参数
  * type   [1,2,3]     值：1，2，3 分别表示显示一层二层三层分类列表<br />【可选参数】如果不传递，则默认获取所有级别的分类
  * pagenum    当前页码值                    【可选参数】如果不传递，则默认获取所有分类
  * pagesize      每页显示多少条数据    【可选参数】如果不传递，则默认获取所有分类
- 响应数据

```vue
{
    "data": [
        {
            "cat_id": 1,
            "cat_name": "大家电",
            "cat_pid": 0,
            "cat_level": 0,
            "cat_deleted": false,
            "children": [
                {
                    "cat_id": 3,
                    "cat_name": "电视",
                    "cat_pid": 1,
                    "cat_level": 1,
                    "cat_deleted": false,
                    "children": [
                        {
                            "cat_id": 6,
                            "cat_name": "曲面电视",
                            "cat_pid": 3,
                            "cat_level": 2,
                            "cat_deleted": false
                        },
                        {
                            "cat_id": 7,
                            "cat_name": "海信",
                            "cat_pid": 3,
                            "cat_level": 2,
                            "cat_deleted": false
                        }
                    ]
                }
            ]
        }
    ],
    "meta": {
        "msg": "获取成功",
        "status": 200
    }
}
```

```vue
第一步：在data数据的return中
	1.定义商品分类的数据列表，默认为空 catelist: []

	2.定义查询条件
		 queryInfo: {
                type: 3,
                pagenum: 1,
                pagesize: 5
          }

	3.总数据条数   total: 0
第二步：在created中，调用获取分类列表数据 this.getCateList()

第三步：在methods方法中，定义getCateList
	// 获取商品分类数据
        async getCateList(){
            const {data: res} = await this.$http.get('categories',{
                params: this.queryInfo      ..1.首先在data中定义 queryInfo
            })
            if(res.meta.status!==200){
                return this.$message.error('获取商品分类失败！')
            }
            console.log(res.data);
            // 把数据列表，赋值给catelist
            this.catelist = res.data.result  ..2.首先在data中定义商品分类的数据列表，默认为空  catelist: []
            // 为总数据条数赋值
            this.total = res.data.total      ..3.首先在data中定义总数据条数   total: 0
        }

```

#### 5.商品分类-初步使用vue-table-width-tree-grid

```vue
第一步：在依赖--运行依赖--搜索：vue-table-width-tree-grid--安装插件
第二步：在main.js，导入插件
	import TreeTable from 'vue-table-width-tree-grid'
	Vue.component('tree-table', TreeTable)
第三步：在data中为table指定列的定义
	columns: [{
                label: '分类名称',   label用来指定：列的标题
                prop: 'cat_name'    prop指定：这一列所绑定的数据属性
    }]
第四步：在Cate.vue的卡片视图中
	 		<!-- 表格 -->
            <tree-table
            border                	 添加纵向分割线
            :data="catelist"
            :columns="columns"
            :selection-type="false"   移除复选框效果
            :expand-type="false"      移除展开行效果
            :show-row-hover="false"   鼠标悬停时，是否显示高亮当前行
            index-text="#"			  自定义索引名称
            show-index>               show-index 渲染索引列
            </tree-table>
```

#### 6.商品分类-使用自定义模板列渲染表格数据

* label                                          用来指定：列的标题
* prop                                          指定：这一列所绑定的数据属性
* type: 'template'                       如果列对象有这个属性，说明这一列要渲染为自定义模板列
* template: '自定义插槽名称'    自定义模板列要指定的作用域插槽，template属性指定插槽的名称

** Tree-table中如何使用作用域插槽

* 如果"cat_deleted": false  页面渲染为绿色的√
* 如果"cat_deleted": true   页面渲染为红色的×

```vue
第一步：在data数据的columns数组中，添加自定义模板列对象
			{
                label: '是否有效',
                // 表示将当前列定义为模板列
                type: 'template',
                // 表示当前这一列使用模板名称
                template: 'isok'
            }
第二步：在tree-table标签里面，添加作用域插槽template标签   
       slot="isok"          slot指向作用域插槽的名称
       slot-scope="scope"   slot-scope属性接收这一行的数据
				<!-- 是否有效 -->
				<template slot="isok" slot-scope="scope">
                    <i class="el-icon-success" v-if="scope.row.cat_deleted===false" style="color: lightgreen"></i>
                    <i class="el-icon-error" v-else style="color: lightred"></i>
                </template>
```

#### 7.商品分类-渲染排序和操作对应的UI结构

```vue
...............................................................排序
第一步：在data数据的columns数组中，添加自定义模板列对象
			{
                label: '排序',
                // 表示将当前列定义为模板列
                type: 'template',
                // 表示当前这一列使用模板名称
                template: 'order'
            }

第二步：在tree-table标签里面，添加作用域插槽template标签  
				<!-- 排序 -->
                <template slot="order" slot-scope="scope">
                   <el-tag size="mini" v-if="scope.row.cat_level===0">一级</el-tag>
                   <el-tag size="mini" type="success" v-else-if="scope.row.cat_level===1">二级</el-tag>
                   <el-tag size="mini" type="warning" v-else>三级</el-tag>
                </template>
...............................................................操作
第一步：在data数据的columns数组中，添加自定义模板列对象
			{
                label: '操作',
                // 表示将当前列定义为模板列
                type: 'template',
                // 表示当前这一列使用模板名称
                template: 'opt'
            }
第二步：在tree-table标签里面，添加作用域插槽template标签 
				<!-- 操作 -->
                <template slot="opt" slot-scope="scope">
                    <el-button size="mini" type="primary" icon="el-icon-edit">编辑</el-button>
                    <el-button size="mini" type="danger"  icon="el-icon-delete">删除</el-button>
                </template>
```

#### 8.商品分类--实现分页功能

** Pagenation分页--附加功能**

```vue
第一步：将分页代码粘贴到分页区域
			<!-- 分页 -->
            <el-pagination
            @size-change="handleSizeChange"
            @current-change="handleCurrentChange"
            :current-page="queryInfo.pagenum"
            :page-sizes="[3, 5, 10, 15]"
            :page-size="queryInfo.pagesize"
            layout="total, sizes, prev, pager, next, jumper"
            :total="total">
            </el-pagination>

第二步：在methods方法中
		// 1.监听pagesize改变
        handleSizeChange(newSize){
            this.queryInfo.pagesize = newSize
            this.getCateList()
        },
        // 2.监听pagenum改变
        handleCurrentChange(newPage){
            this.queryInfo.pagenum = newPage
            this.getCateList()
        }

```

#### 9.商品分类-渲染添加分类的对话框和表单

** Dialog对话框--Form表单--表单验证**

```vue
第一步：将对话框代码结构粘贴到卡片视图区域下面
	<!-- 添加分类的对话框 -->
        <el-dialog
        title="添加分类"
        :visible.sync="addCateDialogVisible"
        width="50%">
            <!-- 添加分类的表单 -->
            <el-form 
            :model="addCateForm" 
            :rules="addCateFormRules" 
            ref="addCateFormRef" 
            label-width="100px">
                <el-form-item label="分类名称" prop="cat_name">
                    <el-input v-model="addCateForm.cat_name"></el-input>
                </el-form-item>
                <el-form-item label="父级分类">
                   
                </el-form-item>
            </el-form>
            <span slot="footer" class="dialog-footer">
                <el-button @click="addCateDialogVisible = false">取 消</el-button>
                <el-button type="primary" @click="addCateDialogVisible = false">确 定</el-button>
            </span>
        </el-dialog>

第二步：在data数据的return中定义   
	1. 控制添加分类对话框的显示与隐藏  addCateDialogVisible: false

	2. 添加分类的表单数据对象  
            addCateForm: {
                // 1.将要添加的分类的名称
                cat_name: '',
                // 2.父级分类的id
                cat_pid: 0,
                // 3.分类的等级，默认要添加的是1级分类
                cat_level: 0
            }
	3.添加分类表单的验证规则对象
            addCateFormRules: {
                cat_name: [
                    { required: true, message: '请输入分类名称', trigger: 'blur' }
                ]
            }

第三步：为添加分类按钮，绑定事件  <el-button type="primary" @click="showAddCateDialog">添加分类</el-button>

第四步：在methods方法中
	// 点击按钮，展示添加分类的对话框
        showAddCateDialog(){
            this.addCateDialogVisible = true
        }

```

#### 10.商品分类-获取父级分类数据列表

- 请求路径：categories
- 请求方法：get
- 请求参数
  * type   [1,2,3]   值：1，2，3 分别表示显示一层二层三层分类列表<br />【可选参数】如果不传递，则默认获取所有级别的分类
  * pagenum     当前页码值                  【可选参数】如果不传递，则默认获取所有分类
  * pagesize      每页显示多少条数据   【可选参数】如果不传递，则默认获取所有分类
- 响应数据

```vue
{
    "data": [
        {
            "cat_id": 1,
            "cat_name": "大家电",
            "cat_pid": 0,
            "cat_level": 0,
            "cat_deleted": false,
            "children": [
                {
                    "cat_id": 3,
                    "cat_name": "电视",
                    "cat_pid": 1,
                    "cat_level": 1,
                    "cat_deleted": false,
                    "children": [
                        {
                            "cat_id": 6,
                            "cat_name": "曲面电视",
                            "cat_pid": 3,
                            "cat_level": 2,
                            "cat_deleted": false
                        },
                        {
                            "cat_id": 7,
                            "cat_name": "海信",
                            "cat_pid": 3,
                            "cat_level": 2,
                            "cat_deleted": false
                        }
                    ]
                }
            ]
        }
    ],
    "meta": {
        "msg": "获取成功",
        "status": 200
    }
}
```

代码演示：

```vue
第一步：在data中定义，父级分类的列表  parentCateList: []

第二步：在methods方法中
		// 点击按钮，展示添加分类的对话框
        showAddCateDialog(){
            // **1.先获取父级分类的数据列表**
            this.getParentCateList()
            // 再展示出对话框
            this.addCateDialogVisible = true
        }

		// **2.获取父级分类的数据列表**
        async getParentCateList(){
            const {data: res} = await this.$http.get('categories',{
                params: {type: 2}
            })
            if(res.meta.status!==200){
                return this.$message.error('获取父级分类数据失败！')
            }
            console.log(res.data);
            this.parentCateList = res.data
        }

```

#### 11.商品分类-渲染级联选择器

** Cascader级联选择器**

```vue
第一步：在element.js导入Cascader组件

第二步：将级联选择器代码粘贴到父级分类内容区域
	 		  <el-form-item label="父级分类">
                   <!-- 级联选择器 -->
                   <!-- options 用来指定数据源 -->
                   <!-- props   用来指定配置对象 -->
                   <!-- v-model 将选定的值双向绑定到data中，v-model必须绑定一个数组-->
                   <el-cascader
                    expand-trigger='hover'
                    clearable     是否支持清空选项
                    v-model="selectedKeys"
                    :options="parentCateList"
                    :props="cascaderProps"
                    @change="parentCateChanged">
                    </el-cascader>
                </el-form-item>
	

第三步：在data数据中，指定级联选择器的配置对象
			// 父级分类的列表
            parentCateList: [],
            // 指定级联选择器的配置对象
            // value      选中的值
            // label      看到的内容
            // children   父子节点之间通过children实现嵌套
            cascaderProps: {
                expandTrigger: 'hover',
                value: 'cat_id',
                label: 'cat_name',
                children: 'children'
            },
            // 选中的父级分类的ID数组
            selectedKeys: []

第四步：在stle样式中
	 .el-cascader{
        width: 100%;
    }
第五步：在global.css样式中(解决页面宽度不够，各级内容全部在一列显示！)
	.el-cascader-menu__wrap {
    	height: 204px!important;
	}
```

#### 12.商品分类-根据父分类的变化处理表单中的数据

```vue
1.为确定按钮添加点击事件    <el-button type="primary" @click="addCate">确 定</el-button>

2.在methods方法中：
	 // 点击按钮，添加新的分类
        addCate(){
            console.log(this.addCateForm);
            
        }，
	// 选择项发送变化触发这个函数
        parentCateChanged(){
            console.log(this.selectedKeys);
            // 如果selectedKeys 数组中的length大于0，证明选中的父级分类
            // 反之，就说明没有选中任何父级分类
            if(this.selectedKeys.length > 0){
                // 父级分类的id
                this.addCateForm.cat_pid = this.selectedKeys[this.selectedKeys.length - 1]
                // 为当前分类的等级赋值
                this.addCateForm.cat_level = this.selectedKeys.length
                return
            }else{
                // 父级分类的id
                this.addCateForm.cat_pid = 0
                // 为当前分类的等级赋值
                this.addCateForm.cat_level = 0
            }
        }
```

#### 13.商品分类-在对话框的close事件中重置表单数据

```vue
第一步：为添加分类对话框el-dialog添加close事件     @close="addCateDialogClosed"

第二步：在methods方法中
	// 监听对话框的关闭事件，重置表单数据
        addCateDialogClosed(){
            this.$refs.addCateFormRef.resetFields()
            this.selectedKeys = []
            this.addCateForm.cat_level = 0
            this.addCateForm.cat_pid = 0
        }
```

#### 15.商品分类-完成添加分类的操作

1. 点击添加分类确定按钮的时候，对表单里面的数据进行预验证
2. 预验证通过之后，调用接口发起请求添加新的分类

- 请求路径：categories
- 请求方法：post
- 请求参数
  * cat_pid         分类父 ID     不能为空，如果要添加1级分类，则父分类Id应该设置为  `0`
  * cat_name    分类名称       不能为空
  * cat_level      分类层级       不能为空，`0`表示一级分类；`1`表示二级分类；`2`表示三级分类
- 响应数据

```vue
{
    "data": {
        "cat_id": 62,
        "cat_name": "相框",
        "cat_pid": "1",
        "cat_level": "1"
    },
    "meta": {
        "msg": "创建成功",
        "status": 201
    }
}
```

```vue
	// 点击按钮，添加新的分类
        addCate(){
            // console.log(this.addCateForm);
            this.$refs.addCateFormRef.validate(async valid=>{
                if(!valid) return
                const {data: res} = await this.$http.post('categories',this.addCateForm)
                if(res.meta.status!==201){
                    return this.$message.error('添加分类失败！')
                }
                // 1.成功提示
                this.$message.success('添加分类成功！')
                // 2.刷新列表
                this.getCateList()
                // 3.关闭对话框
                this.addCateDialogVisible = false
            })
        }
```

#### 16.分支操作-将goods_cate分支上的代码提交到玛云

```tex
在项目根目录，运行：
	1. git branch  查看当前所处分支，此时处于goods_cate分支上
	2. git status
	3. git add .
	4. git commit -m "完成了分类功能的开发"
	5. git status
	6. git push    将本地goods_cate分支上的代码，提交到玛云goods_cate分支上
	7. git checkout master   首先切换到master主分支
	8. git merge goods_cate  此时本地master主分支就是最新的
	9. git push              将本地master主分支上的最新代码，提交到玛云master主分支上
```

### 分类参数

#### 1.分支操作-创建goods_params分支

```vue
在项目根目录，运行：
1. git branch  当前处于master分支
2. git checkout -b goods_params   基于master主分支，创建goods_params子分支
3. git branch  当前处于goods_params分支
4. git push -u origin goods_params  将本地goods_params分支，推送到玛云goods_params分支；此时玛云就多了一个goods_params分支
```

#### 2.分类参数-通过路由加载分类参数组件页面

```vue
第一步：在goods文件下，新建Params.vue组件
第二步：在router.js导入Params.vue组件
第三步：在home路由的children属性中，添加子路由规则

```

#### 3.分类参数-渲染分类参数页面的基本UI结构

** Alert警告**

* closable属性         控制显示/隐藏关闭的按钮
* show-icon属性     显示前面的图标

```vue
第一步：在element.js，导入Alert组件

第二步：赋值粘贴源代码，放在卡片视图区域
 	<div>
        <!-- 面包屑导航区域 -->
        <el-breadcrumb separator-class="el-icon-arrow-right">
            <el-breadcrumb-item :to="{ path: '/home' }">首页</el-breadcrumb-item>
            <el-breadcrumb-item>商品管理</el-breadcrumb-item>
            <el-breadcrumb-item>参数列表</el-breadcrumb-item>
        </el-breadcrumb>
        <!-- 卡片视图区域 -->
        <el-card>
            <!-- 警告区域 -->
            <el-alert
            title="注意：只允许为第三级分类设置相关参数！"
            type="warning"
            show-icon
            :closable="false">
            </el-alert>

            <!-- 选择商品分类区域 -->
            <el-row class="cat_opt">
                <el-col>
                    <span>选择商品分类：</span>
                    <!-- 选择商品分类的级联选择框 -->
                </el-col>
            </el-row>
        </el-card>
    </div>

第三步：在style样式
  .cat_opt{
        margin: 15px 0;
    }
```

#### 4.分类参数--调用API获取商品分类列表数据

- 请求路径：categories
- 请求方法：get
- 请求参数
  * type   [1,2,3]      值：1，2，3 分别表示显示一层二层三层分类列表<br />【可选参数】如果不传递，则默认获取所有级别的分类
  * pagenum    当前页码值                    【可选参数】如果不传递，则默认获取所有分类
  * pagesize      每页显示多少条数据    【可选参数】如果不传递，则默认获取所有分类
- 响应数据

```vue
{
    "data": [
        {
            "cat_id": 1,
            "cat_name": "大家电",
            "cat_pid": 0,
            "cat_level": 0,
            "cat_deleted": false,
            "children": [
                {
                    "cat_id": 3,
                    "cat_name": "电视",
                    "cat_pid": 1,
                    "cat_level": 1,
                    "cat_deleted": false,
                    "children": [
                        {
                            "cat_id": 6,
                            "cat_name": "曲面电视",
                            "cat_pid": 3,
                            "cat_level": 2,
                            "cat_deleted": false
                        },
                        {
                            "cat_id": 7,
                            "cat_name": "海信",
                            "cat_pid": 3,
                            "cat_level": 2,
                            "cat_deleted": false
                        }
                    ]
                }
            ]
        }
    ],
    "meta": {
        "msg": "获取成功",
        "status": 200
    }
}
```

```vue
第一步：在data的return中，定义
	1.商品分类列表   catelist: []
第二步：在created函数中，调用获取所有商品分类列表函数   this.getCateList()
第三步：在methods方法中
	// 获取所有的商品分类列表
        async getCateList(){
            const {data: res} = await this.$http.get('categories')
            if(res.meta.status!==200){
                return this.$message.error('获取商品分类失败！')
            }
            this.catelist = res.data
            console.log(this.catelist);
        }

```

#### 5.分类参数-渲染商品分类的级联选择框

** Cascader级联选择器**

* options    指定数据源
* props       配置级联选择框
* v-model   可以把选中的id值，双向绑定到数组中
* change    级联选择框选中项变化，会触发这个函数

```vue
第一步:复制级联选择器代码，粘贴到商品分类下面
 				<el-col>
                    <span>选择商品分类：</span>
                    <!-- 选择商品分类的级联选择框 -->
                    <el-cascader
                    expandTrigger='hover'
                    :props="cateProps"
                    v-model="selectedCateKeys"
                    :options="catelist"
                    @change="handleChange"></el-cascader>
                </el-col>
第二步：在data的return中，定义
	1.级联选择框的配置对象
		 cateProps: {
                value: 'cat_id',
                label: 'cat_name',
                children: 'children'
          }
	2.级联选择框双向绑定到的数组   selectedCateKeys: []

第三步：在methods方法中
	 // 级联选择框选中项变化，会触发这个函数
        handleChange(){
            // **控制级联选择框的选中范围**

            // 1.如果数组长库不等于3，证明选中的不是三级分类
            if(this.selectedCateKeys.length!==3){
                this.selectedCateKeys = []
                return
            }
            // 2.证明选中的是三级分类
            console.log(this.selectedCateKeys);
        }
	
```

#### 6.分类参数-渲染分类参数的Tabs页签

**Tabs标签页**

```vue
第一步：在element.js导入Tabs/TabPane
第二步：将Tabs标签页代码放在el-row代码下面
		<!-- 标签页区域 -->
            <el-tabs v-model="activeName" @tab-click="handleTabClick">
                <el-tab-pane label="动态参数" name="first">动态参数</el-tab-pane>
                <el-tab-pane label="静态属性" name="second">静态属性</el-tab-pane>
            </el-tabs>
第三步：在data的return中，定义
	1.被激活的页签的名称   activeName: 'first'
第四步：在methods方法中
	// Tab 页签点击事件的处理函数
        handleTabClick(){
            console.log(this.activeName);
        }
```

#### 7.分类参数-渲染添加参数按钮并控制按钮的禁用和启用状态

方法：通过定义一个计算属性isBtnDisabled返回一个布尔值，来控制按钮的禁用和启用状态

```vue
第一步：添加按钮
	<!-- 标签页区域 -->
            <el-tabs v-model="activeName" @tab-click="handleTabClick">
                <!-- 添加动态参数的面板 -->
                <el-tab-pane label="动态参数" name="first">
                    <!-- 添加动态参数的按钮 -->
                    <el-button type="primary" size="mini" :disabled="isBtnDisabled">添加参数</el-button>
                </el-tab-pane>
                <!-- 添加静态属性的面板 -->
                <el-tab-pane label="静态属性" name="second">
                    <!-- 添加静态属性的按钮 -->
                    <el-button type="primary" size="mini" :disabled="isBtnDisabled">添加属性</el-button>
                </el-tab-pane>
            </el-tabs>

第二步：添加计算属性
 computed: {
        // 如果按钮需要被禁用，则返回true,否则返回false
        isBtnDisabled(){
            if(this.selectedCateKeys.length!==3){
                return true
            }
            return false
        }
    }

```

#### 8.分类参数-获取参数列表数据

- 请求路径：categories/:id/attributes
- 请求方法：get
- 请求参数
  * :id    分类 ID             不能为空`携带在url中`
  * sel    [only,many]    不能为空,通过 only 或 many 来获取分类静态参数还是动态参数
- 响应数据

```vue
{
    "data": [
        {
            "attr_id": 1,
            "attr_name": "cpu",
            "cat_id": 22,
            "attr_sel": "only",
            "attr_write": "manual",
            "attr_vals": "ffff"
        }
    ],
    "meta": {
        "msg": "获取成功",
        "status": 200
    }
}
```

```vue
第一步：将name对应的first、second变更为only或者many

第二步：在computed中，添加cateId函数
	// 当前选中的三级分类的ID
        cateId(){
            if(this.selectedCateKeys.length===3){
                return  this.selectedCateKeys[2]
            }
            return null
        }

第二步：在handleChange函数中，如果证明选中是第三级分类就调用API接口
 	// 级联选择框选中项变化，会触发这个函数
        async handleChange(){
            // 控制级联选择框的选中范围

            // 如果数组长库不等于3，证明选中的不是三级分类
            if(this.selectedCateKeys.length!==3){
                this.selectedCateKeys = []
                return
            }
            // 证明选中的是三级分类
            console.log(this.selectedCateKeys);
            // 根据所选分类的id,和当前所处的面板，获取对应的参数
            const {data: res} = await this.$http.get(`categories/${this.cateId}/attributes`,{
                params: {sel: this.activeName}
            })
            
            if(res.meta.status!==200){
                return this.$message.error('获取参数列表失败！')
            }
            // 获取参数成功
            console.log(res.data);
        },

```

#### 9.分类参数-切换Tabs面板后重新获取参数列表

切换面板或者切换三级分类，都会获取数据

```vue
第一步：将原先handleChange函数中的代码，剪切

第二步：在methods方法中
	getParamsData(){
      粘贴到这里
	}

第三步：
	在handleTabClick函数中调用  this.getParamsData()
	在handleChange函数中调用    this.getParamsData()

```

#### 10.分类参数-将获取到的参数数据挂载到不同的数据数组中

```vue
第一步：在data的return中定义
	1.动态参数的数据  manyTableData: []
	2.静态属性的数据  onlyTableData: []
第二步：在getParamsData函数中
			// 获取参数成功
            console.log(res.data);
......................................................
            if(this.activeName === 'many'){
                this.manyTableData = res.data
            }else{
                this.onlyTableData = res.data
            }

```

#### 11.分类参数-渲染动态参数和静态属性的Table表格

```vue
1.在添加动态参数的按钮，下面：
			<!-- 动态参数表格 -->
                    <el-table :data="manyTableData" border stripe>
                        <!-- 展开行 -->
                        <el-table-column type="expand"></el-table-column>
                        <!-- 索引列 -->
                        <el-table-column type="index"></el-table-column>
                        <el-table-column label="参数名称" prop="attr_name"></el-table-column>
                        <el-table-column label="操作">
                            <template slot-scope="scope">
                                <el-button size="mini" type="primary" icon="el-icon-edit">编辑</el-button>
                                <el-button size="mini" type="danger" icon="el-icon-delete">删除</el-button>
                            </template>
                        </el-table-column>
                    </el-table>
2.在添加静态属性的按钮，下面：
			<!-- 静态参数表格 -->
                    <el-table :data="onlyTableData" border stripe>
                        <!-- 展开行 -->
                        <el-table-column type="expand"></el-table-column>
                        <!-- 索引列 -->
                        <el-table-column type="index"></el-table-column>
                        <el-table-column label="属性名称" prop="attr_name"></el-table-column>
                        <el-table-column label="操作">
                            <template slot-scope="scope">
                                <el-button size="mini" type="primary" icon="el-icon-edit">编辑</el-button>
                                <el-button size="mini" type="danger" icon="el-icon-delete">删除</el-button>
                            </template>
                        </el-table-column>
                    </el-table>
```

#### 12.添加参数-渲染添加参数的对话框

** Dialog对话框--Form表单**

```vue
第一步：在el-card卡片视图下面，添加下面代码：
	<!-- 添加参数对话框区域 -->
        <el-dialog
        :title="'添加'+ titleText"
        :visible.sync="addDialogVisible"
        width="50%"
        @close="addDialogClosed">
            <!-- 添加参数的表单 -->
            <el-form 
            :model="addForm" 
            :rules="addFormRules" 
            ref="addFormRef" 
            label-width="100px">
                <el-form-item :label="titleText" prop="attr_name">
                    <el-input v-model="addForm.attr_name"></el-input>
                </el-form-item>
            </el-form>
            <span slot="footer" class="dialog-footer">
                <el-button @click="addDialogVisible = false">取 消</el-button>
                <el-button type="primary" @click="addDialogVisible = false">确 定</el-button>
            </span>
        </el-dialog>
第二步：在created中，动态计算标题的文本   **效果：添加参数和添加属性共用一个对话框**
	 // 动态计算标题的文本
        titleText(){
            if(this.activeName === 'many'){
                return '动态参数'
            }else{
                return '静态属性'
            }
        }
第三步：在data的return中
	1.控制添加对话框的显示与隐藏 addDialogVisible: false
	2.添加参数的表单数据对象    
		addForm: {
          attr_name: ''
		}
	3. 添加表单的验证规则对象
			addFormRules: {
                attr_name: [
                    { required: true, message: '请输入参数名称', trigger: 'blur' }
                ]
            }
第四步：为添加属性和添加参数绑定事件  @click = "addDialogVisible = true"

第五步：为el-dialog对话框绑定close事件   @close="addDialogClosed"

第六步：在methods方法中
 	// 监听对话框的关闭事件
        addDialogClosed(){
            this.$refs.addFormRef.resetFields()
        }
```

#### 13.添加参数-完成动态参数和静态属性的添加操作

- 请求路径：categories/:id/attributes
- 请求方法：post
- 请求参数
  * :id                  分类 ID                                                                            不能为空`携带在url中`
  * attr_name    参数名称                                                                         不能为空
  * attr_sel        [only,many]                                                                    不能为空
  * attr_vals      如果是 many 就需要填写值的选项，以逗号分隔      【可选参数】
- 响应数据

```vue
{
    "data": {
        "attr_id": 44,
        "attr_name": "测试参数",
        "cat_id": "1",
        "attr_sel": "many",
        "attr_write": "list",
        "attr_vals": "a,b,c"
    },
    "meta": {
        "msg": "创建成功",
        "status": 201
    }
}
```

```vue
第一步：为el-button确定按钮，添加事件   <el-button type="primary" @click="addParams">确 定</el-button>
第二步：在methods方法中
 	// 点击按钮，添加参数
        addParams(){
            this.$refs.addFormRef.validate(async valid=>{
                if(!valid) return
                const {data: res} = await this.$http.post(`categories/${this.cateId}/attributes`,{
                    attr_name: this.addForm.attr_name,
                    attr_sel: this.activeName
                })
                if(res.meta.status!==201){
                    return this.$message.error('添加参数失败！')
                }
                // 1.成功提示
                this.$message.success('添加参数成功！')
                // 2.关闭对话框
                this.addDialogVisible = false
                // 3.刷新参数列表
                this.getParamsData()
            })
        }
```

#### 14.修改参数-渲染修改参数的对话框

```vue
首先，在添加参数的对话框下面，添加修改参数的对话框代码
	<!-- 修改参数的对话框 -->
        <el-dialog
        :title="'修改'+ titleText"
        :visible.sync="editDialogVisible"
        width="50%"
        @close="editDialogClosed">
            <!-- 添加参数的表单 -->
            <el-form 
            :model="editForm" 
            :rules="editFormRules" 
            ref="editFormRef" 
            label-width="100px">
                <el-form-item :label="titleText" prop="attr_name">
                    <el-input v-model="editForm.attr_name"></el-input>
                </el-form-item>
            </el-form>
            <span slot="footer" class="dialog-footer">
                <el-button @click="editDialogVisible = false">取 消</el-button>
                <el-button type="primary" @click="editParams">确 定</el-button>
            </span>
        </el-dialog>

然后在data中定义：
	1.控制修改对话框的显示与隐藏  editDialogVisible: false
	2.修改的表单数据对象          editForm: {}
	3.修改表单的验证规则对象
	 editFormRules: {
                attr_name: [
                    { required: true, message: '请输入参数名称', trigger: 'blur' }
                ]
            }

第一步：为动态参数和静态属性的编辑按钮，添加点击事件   @click="showEditDialog"
第二步：在methods方法中
	// 1.点击按钮，展示修改的对话框
        showEditDialog(){
            this.editDialogVisible = true
        },
    // 2.重置修改的表单
        editDialogClosed(){
            this.$refs.editFormRef.resetFields()
        },
    // 3.点击按钮，修改参数信息
        editParams(){

        }
```

#### 15.修改参数-完成修改参数的操作

- 请求路径：categories/:id/attributes/:attrId
- 请求方法：get
- 请求参数
  * :id            分类 ID              不能为空`携带在url中`
  * :attrId      属性 ID             不能为空`携带在url中`
  * attr_sel    [only,many]    不能为空
  * attr_vals     如果是 many 就需要填写值的选项，以逗号分隔
- 响应数据

```vue
{
    "data": {
        "attr_id": 1,
        "attr_name": "cpu",
        "cat_id": 22,
        "attr_sel": "only",
        "attr_write": "manual",
        "attr_vals": "ffff"
    },
    "meta": {
        "msg": "获取成功",
        "status": 200
    }
}
```

```vue
第一步：点击编辑按钮，传递参数id    @click="showEditDialog(scope.row.attr_id)"
第二步：在showEditDialog函数中，发送请求
 	// 点击按钮，展示修改的对话框
        async showEditDialog(attr_id){
            // 查询当前参数的信息
            const {data: res} = await this.$http.get(`categories/${this.cateId}/attributes/${attr_id}`,{
                params: {attr_sel: this.activeName}
            })
            if(res.meta.status!==200){
                return this.$message.error('获取参数信息失败！')
            }
            // 如果获取参数信息成功，将数据保存到编辑的表单上
            this.editForm = res.data

            this.editDialogVisible = true
        }

```

####  编辑提交参数

- 请求路径：categories/:id/attributes/:attrId
- 请求方法：put
- 请求参数
  * :id                   分类 ID             				  不能为空`携带在url中`
  * :attrId            属性 ID                                               不能为空`携带在url中`
  * attr_name    新属性的名字                                     不能为空，携带在`请求体`中
  * attr_se          属性的类型[many或only]                 不能为空，携带在`请求体`中
  * attr_vals       参数的属性值                                     可选参数，携带在`请求体`中
- 响应数据

```vue
{
    "data": {
        "attr_id": 9,
        "attr_name": "测试更新",
        "cat_id": "43",
        "attr_sel": "only",
        "attr_write": "manual",
        "attr_vals": "abc"
    },
    "meta": {
        "msg": "更新成功",
        "status": 200
    }
}
```

```vue
第三步：点击按钮，修改参数信息
        editParams(){
            // 表单预验证validate
            this.$refs.editFormRef.validate(async valid=>{
                if(!valid) return
                const {data: res} = await this.$http.put(`categories/${this.cateId}/attributes/${this.editForm.attr_id}`,{
                    attr_name: this.editForm.attr_name,
                    attr_sel: this.activeName
                })
                if(res.meta.status!==200){
                    return this.$message.error('修改参数失败！')
                }
                // 1.修改参数成功
                this.$message.success('修改参数成功！')
                // 2.刷新获取参数列表
                this.getParamsData()
                // 3.关闭编辑对话框
                this.editDialogVisible = false
            })
        }
```

#### 16.删除参数-完成删除参数的业务逻辑

- 请求路径： categories/:id/attributes/:attrid
- 请求方法：delete
- 请求参数
  * :id          分类 ID           不能为空`携带在url中`
  * :attrid    参数 ID           不能为空`携带在url中`
- 响应数据

```vue
{
    "data": null,
    "meta": {
        "msg": "删除成功",
        "status": 200
    }
}

```

```vue
** MessageBox弹框 **
第一步：为删除按钮绑定事件，传递参数id  @click="removeParams(scope.row.attr_id)"
第二步：在methods方法中
	// 根据id删除对应的参数项
        async removeParams(attr_id){
            const confirmResult = await this.$confirm(
                '此操作将永久删除该参数, 是否继续?', '提示',
                {
                    confirmButtonText: '确定',
                    cancelButtonText: '取消',
                    type: 'warning'
                }).catch(err => err)
                // 用户取消了删除的操作
                if(confirmResult!=='confirm'){
                    return this.$message.info('已取消删除！')
                }
                // 删除的业务逻辑
                const {data: res} = await this.$http.delete(`categories/${this.cateId}/attributes/${attr_id}`)
                if(res.meta.status!==200){
                    return this.$message.error('删除参数失败！')
                }
                this.$message.success('删除参数成功！')
                this.getParamsData()
        }

```

#### 17.分类参数-渲染参数下的可选框

1. 将服务器返回的数组中的每一项进行for循环，每循环一次都会拿到参数项
2. 立即将参数项身上的attr_vals,以空格进行分隔；将字符串分隔为数组，再重新给attr_vals赋值
3. 这样每一项的attr_vals就是一个数组，然后渲染每一行的时候在展开行中通过for循环将数组中的每一项渲染为Tab标签

```vue
第一步：在getParamsData函数中
 			if(res.meta.status!==200){
                return this.$message.error('获取参数列表失败！')
            }
            // 获取参数成功
            .....................................................................................书写代码如下：
            // 1.将服务器返回的数组中的每一项进行for循环，每循环一次都会拿到参数项
				三元表达式的格式：  布尔表达式? 值0 : 值1   布尔表达式为真，结果为0   布尔表达式为假，结果为
				首先判断item.attr_vals是否为空：
                如果不为空立即将参数项身上的attr_vals,以空格进行分隔；将字符串分隔为数组，再重新给attr_vals赋值
				否则就返回一个空数组
			 
            res.data.forEach(item=>{
               item.attr_vals = item.attr_vals?item.attr_vals.split(' '):[]   **解决attr_vals为空字符串的bug**
            })
第二步：2.在动态参数表格的展开行中，通过for循环将数组中的每一项渲染为Tab标签
			<!-- 展开行 -->
                        <el-table-column type="expand">
                            <template slot-scope="scope">   ** 作用域插槽 **
                                <el-tag v-for="(item,i) in scope.row.attr_vals" :key="i" closable>{{item}}</el-tag>
                            </template>
                        </el-table-column>

第三步：在style样式
 .el-tag {
        margin: 10px;
    }
```

#### 18.分类参数-控制按钮与文本框的切换显示

** Tag标签--动态编辑标签**

```vue
第一步：复制 动态编辑标签中的代码，粘贴到el-tag标签下面
						<!--输入的文本框  -->
                                <el-input
                                class="input-new-tag"
                                v-if="inputVisible"
                                v-model="inputValue"
                                ref="saveTagInput"
                                size="small"
                                @keyup.enter.native="handleInputConfirm"
                                @blur="handleInputConfirm"
                                >
                                </el-input>
                                <!-- 添加按钮 -->
                                <el-button v-else class="button-new-tag" size="small" @click="showInput">
                                  + New Tag
								</el-button>

第二步：在data的return中
		// 1.控制按钮与文本框的切换显示
            inputVisible: false,
        // 2.文本框中输入的内容
            inputValue: ''	
第三步：在methods方法中
	// 1.文本框失去焦点，或 摁下了 enter 都会触发
        handleInputConfirm(){
            console.log('ok');
            
        },
   // 2.点击按钮，展示文本输入框
        showInput(){
            this.inputVisible = true
        }

第四步：在style样式
  .input-new-tag {
        width: 120px;
    }

```

#### 19.分类参数-为每一行数据提供单独的inputVisible

bug:点击任一个切换显示的按钮，其他行的切换显示按钮也会同时起效果

​	如果在文本输入框，输入内容，其他行的文本输入框也会显示输入的内容

原因：每渲染一个展开行，共用了inputVisible 和 inputValue值

解决：为每一行数据提供单独的inputVisible 和 inputValue值

​	inputVisible  控制自己的显示与隐藏

​	自己输入的内容，保存到自己的inputValue中

```vue
第一步:在getParamsData函数中
 			res.data.forEach(item=>{
                item.attr_vals = item.attr_vals?item.attr_vals.split(' '):[]
			.........................这样每一行数据都有了自己的inputVisible 和 inputValue ..................
                // 1.为item添加属性inputVisible，控制文本框的显示与隐藏
                item.inputVisible  = false
                // 2.为item添加属性 inputValue，文本框的输入的值
                item.inputValue = ''
            })
第二步：在el-input中
 v-if="scope.row.inputVisible"       inputVisible  控制自己的显示与隐藏
 v-model="scope.row.inputValue"      自己输入的内容，保存到自己的inputValue中

第三步：在data中，删除下面代码
		// 1.控制按钮与文本框的切换显示
            inputVisible: false,
        // 2.文本框中输入的内容
            inputValue: ''	
第四步：在el-button按钮的点击事件中，传递参数 @click="showInput(scope.row)"
 <el-button v-else class="button-new-tag" size="small" @click="showInput(scope.row)">+ New Tag</el-button>
第五步：在methods方法中
  // 点击按钮，展示文本输入框
        showInput(row){
            row.inputVisible = true
	     ..................................................让文本框自动获得焦点
			// $nextTick 方法的作用，就是当页面上元素被重新渲染之后，才会指定回调函数中的代码
            this.$nextTick(_ => {
                this.$refs.saveTagInput.$refs.input.focus();
            });
        }
```

#### 20.分类参数-实现文本框与按钮的切换显示

```vue
第一步：在el-input标签，为事件处理函数传递参数
 @keyup.enter.native="handleInputConfirm(scope.row)"
 @blur="handleInputConfirm(scope.row)"
第二步：在methods方法中
	// 文本框失去焦点，或 摁下了 enter 都会触发
        handleInputConfirm(row){
            if(row.inputValue.trim().length===0){
                row.inputValue = ''
                row.inputVisible = false
                return
            }
            // 如果没有return，则证明输入的内容，需要做后续处理
           
            
        },
```

#### 21.分类参数-完成参数可选项的添加操作-编辑提交参数

- 请求路径：categories/:id/attributes/:attrId
- 请求方法：put
- 请求参数
  - :id                     分类 ID  		                      不能为空`携带在url中` 
  - :attrId             属性 ID                                        不能为空`携带在url中`  
  - attr_name      新属性的名字                             不能为空，携带在`请求体`中  
  - attr_sel            属性的类型[many或only]        不能为空，携带在`请求体`中 
  - attr_vals          参数的属性值                           可选参数，携带在`请求体`中 
- 响应数据

```vue
{
    "data": {
        "attr_id": 9,
        "attr_name": "测试更新",
        "cat_id": "43",
        "attr_sel": "only",
        "attr_write": "manual",
        "attr_vals": "abc"
    },
    "meta": {
        "msg": "更新成功",
        "status": 200
    }
}
```

```vue
// 文本框失去焦点，或 摁下了 enter 都会触发
        async handleInputConfirm(row){
            if(row.inputValue.trim().length===0){
                row.inputValue = ''
                row.inputVisible = false
                return
            }
            ..............................................如果没有return，则证明输入的内容，需要做后续处理
            // 1.将用户输入的值保存到attr_vals数组中
            row.attr_vals.push(row.inputValue.trim())
            // 2.清空文本框的内容
            row.inputValue=''
            // 3.关闭文本框
            row.inputVisible=false
            // 4.需要发起请求，保存这次操作
            const {data: res} = await this.$http.put(`categories/${this.cateId}/attributes/${row.attr_id}`,{
                attr_name: row.attr_name,
                attr_sel: row.attr_sel,
                // 服务器要求接收字符串，所以将数组转换为字符串
                attr_vals: row.attr_vals.join(' ')
            })
            if(res.meta.status!==200){
                return this.$message.error('修改参数项失败！')
            }
            this.$message.success('修改参数项成功！')
        }
```

#### 22.分类参数-删除参数下的可选项



```vue
第一步：为el-tag标签，添加close事件   @close="handleClosed(i,scope.row)"
第二步：在methods方法中
 // 1.将对attr_vals的操作，保存到数据库
        async saveAttrVals(row){
            // .............发起修改参数请求，保存这次操作(将handleInputConfirm函数中发起请求的代码剪切到saveAttrVals函数中)
            const {data: res} = await this.$http.put(`categories/${this.cateId}/attributes/${row.attr_id}`,{
                attr_name: row.attr_name,
                attr_sel: row.attr_sel,
                // 服务器要求接收字符串，所以将数组转换为字符串
                attr_vals: row.attr_vals.join(' ')
            })
            if(res.meta.status!==200){
                return this.$message.error('修改参数项失败！')
            }
            this.$message.success('修改参数项成功！')
        },
 // 2.删除对应的参数可选项
        handleClosed(i,row){
            // 1.删除数组中的数据
            row.attr_vals.splice(i,1)
            // 2.发起修改参数请求，保存这次操作
            this.saveAttrVals(row)
        }

3.在handleInputConfirm中，调用这个函数  this.saveAttrVals(row)

```

#### 23.分类参数-清空表格数据

1. 商品分类只允许选中第三级分类，不允许选中一级或者二级分类

   如果选中了一级或者二级分类，

   1.当前分类的选择器被清空了

   2.添加分类的按钮也被禁用了

   3.但是对应的表格数据没有被清空，这样在进行编辑或者删除操作的时候，可能会用到商品分类id

   但是此时分类的选择器被清空了，所以没有商品分类的id,最后可能会报错！

2. 所以只要选中的不是三级分类，对应的表格数据也应该被清空

```vue
 在getParamsData函数中
		// 如果数组长库不等于3，证明选中的不是三级分类
            if(this.selectedCateKeys.length!==3){
                this.selectedCateKeys = []
		.........................................如果选中不是三级分类，清空表格数据
                this.manyTableData = []
                this.onlyTableData = []
                return
            }
```

#### 24.分类参数--完成静态属性表格中的展开行效果

```vue
将动态参数展开行的代码复制粘贴到，静态属性展开行的位置！
						<el-table-column type="expand">
                            <template slot-scope="scope">
                                <el-tag 
                                v-for="(item,i) in scope.row.attr_vals" 
                                :key="i"
                                closable
                                @close="handleClosed(i,scope.row)">{{item}}</el-tag>
                                <!--输入的文本框  -->
                                <el-input
                                class="input-new-tag"
                                v-if="scope.row.inputVisible"
                                v-model="scope.row.inputValue"
                                ref="saveTagInput"
                                size="small"
                                @keyup.enter.native="handleInputConfirm(scope.row)"
                                @blur="handleInputConfirm(scope.row)"
                                >
                                </el-input>
                                <!-- 添加按钮 -->
                                <el-button v-else class="button-new-tag" size="small" @click="showInput(scope.row)">
                                  + New Tag
                              	</el-button>
                            </template>
                        </el-table-column>
```

#### 25.分支操作-将本地goods_params中的代码提交到玛云

```tex
在项目根目录，运行：
1.git branch  当前处于goods_params子分支
2.git status
3.git add .
4.git commit -m "完成了分类参数的添加"
5.git status
6.git push   登录玛云查看提交状态
7.git checkout master      首先切换到master主分支
8.git merge goods_params   将goods_params子分支，合并到master主分支
9.git push      将本地主分支master上的代码，提交到玛云
```

### 商品列表功能

#### 1.分支操作-创建goods_list子分支并推送到玛云

```tex
在项目根目录，运行：
1.git branch                       当前处于master分支
2.git checkout -b goods_list       基于master主分支创建goods_list子分支
3.git branch                 	   当前处于goods_list子分支
3.git push -u origin goods_list    将goods_list推送到玛云保存
```

#### 2.商品列表-通过路由加载商品列表组件

```vue
第一步：在goods文件夹下，新建List.vue组件
第二步：在router.js中，导入List.vue组件
	   并且在home组件的children属性中添加路由规则
第三步：在template标签中
<template>
    <div>
        <!-- 面包屑导航区域 -->
        <el-breadcrumb separator-class="el-icon-arrow-right">
            <el-breadcrumb-item :to="{ path: '/home' }">首页</el-breadcrumb-item>
            <el-breadcrumb-item>商品管理</el-breadcrumb-item>
            <el-breadcrumb-item>商品列表</el-breadcrumb-item>
        </el-breadcrumb>
        <!-- 卡片视图 -->
        <el-card>
            <el-row :gutter="20">    **Row 组件 提供 gutter 属性来指定每一栏之间的间隔，默认间隔为 0。**
                <!-- 搜索框 -->
                <el-col :span="8">
                    <el-input
                    placeholder="请输入内容"
                    >
                    <el-button slot="append" icon="el-icon-search"></el-button>
                    </el-input>
                </el-col>
                <!-- 添加商品按钮 -->
                <el-col :span="4">
                    <el-button type="primary">添加商品</el-button>
                </el-col>
            </el-row>
        </el-card>
        <!-- 数据表格区域 -->
    </div>
</template>
```

#### 3.商品列表-获取商品列表数据

- 请求路径：goods
- 请求方法：get
- 请求参数
  - query  查询参数  可以为空  
  - pagenum  当前页码  不能为空 
  - pagesize  每页显示条数  不能为空
- 响应数据

```vue
{
    "data": {
        "total": 50,
        "pagenum": "1",
        "goods": [
            {
                "goods_id": 144,
                "goods_name": "asfdsd",
                "goods_price": 1,
                "goods_number": 1,
                "goods_weight": 1,
                "goods_state": null,
                "add_time": 1512954923,
                "upd_time": 1512954923,
                "hot_mumber": 0,
                "is_promote": false
            }
        ]
    },
    "meta": {
        "msg": "获取成功",
        "status": 200
    }
}
```

```vue
第一步：在data数据中，定义
	1.查询参数对象
	 queryInfo: {
          query: '',
          pagenum: 1,
          pagesize: 10
     }
	2. 商品列表
       goodslist: [],
    3.总数据条数
       total: 0

第二步：在created函数中，调用函数   this.getGoodsList()

第三步：在methods方法中
	// 根据分页获取对应的商品列表
        async getGoodsList(){
            const {data: res} = await this.$http.get('goods',{
               params: this.queryInfo
            })
            if(res.meta.status!==200){
                return this.$message.error('获取商品列表数据失败！')
            }
            this.$message.success('获取参数列表成功！')
            console.log(res.data);
            this.goodslist = res.data.goods
            this.total = res.data.total
        }

```

#### 4.商品列表-渲染商品表格数据

```vue
第一步：在el-row下面，添加商品表格结构
	<!-- 数据表格区域 -->
        <el-table :data="goodslist" border stripe>
            <!-- 索引列 -->
            <el-table-column type="index"></el-table-column>
            <el-table-column label="商品名称" prop="goods_name"></el-table-column>
            <el-table-column width="95px" label="商品价格(元)" prop="goods_price"></el-table-column>
            <el-table-column width="70px" label="商品重量" prop="goods_weight"></el-table-column>
            <el-table-column width="140px" label="创建时间" prop="add_time"></el-table-column>
            <el-table-column width="180px" label="操作">
                <template slot-scope="scope">
                    <el-button size="mini" type="primary" icon="el-icon-edit">编辑</el-button>
                    <el-button size="mini" type="danger" icon="el-icon-delete">删除</el-button>
                </template>
            </el-table-column>
        </el-table>

```

#### 5.商品列表-自定义格式化时间的全局过滤器

```vue
第一步：在main.js中
Vue.filter('dateFormat', function(originVal) {
  const dt = new Date(originVal)

  const y = dt.getFullYear()
  const m = (dt.getMonth() + 1 + '').padStart(2, '0')
  const d = (dt.getDate() + '').padStart(2, '0')

  const hh = (dt.getHours() + '').padStart(2, '0')
  const mm = (dt.getMinutes() + '').padStart(2, '0')
  const ss = (dt.getSeconds() + '').padStart(2, '0')

  return `${y}-${m}-${d} ${hh}:${mm}:${ss}`
})

第二步：在创建时间中
			<el-table-column width="140px" label="创建时间" prop="add_time">
                <template slot-scope="scope">
                    {{scope.row.add_time | dateFormat}}
                </template>
            </el-table-column>
```

#### 6.商品列表-实现商品列表的分页功能

** Pagenation组件**

```vue
第一步：将分页代码复制粘贴到表格区域下面
	<!-- 分页区域 -->
        <el-pagination 
        @size-change="handleSizeChange" 
        @current-change="handleCurrentChange" 
        :current-page="queryInfo.pagenum" 
        :page-sizes="[5, 10, 15, 20]" 
        :page-size="queryInfo.pagesize" 
        layout="total, sizes, prev, pager, next, jumper" 
        :total="total" background>
        </el-pagination>
第二步：在methods方法中
   		handleSizeChange(newSize) {
            this.queryInfo.pagesize = newSize
            this.getGoodsList()
        },
        handleCurrentChange(newPage) {
            this.queryInfo.pagenum = newPage
            this.getGoodsList()
        }

```

#### 7.商品列表-实现搜索与清空的功能

```vue
第一步：为el-input绑定属性或者事件如下
	v-model="queryInfo.query"
	clearable
	@clear="getGoodsList"
第二步：为el-button按钮，绑定事件  @click="getGoodsList"
```

#### 8.商品列表-根据id删除商品数据

- 请求路径：goods/:id
- 请求方法：delete
- 请求参数
  - id  商品 ID  不能为空`携带在url中`
- 响应数据

```vue
{
    "data": null,
    "meta": {
        "msg": "删除成功",
        "status": 200
    }
}
```

```vue
第一步：为删除按钮绑定事件   @click="removeById(scope.row.goods_id)"

第二步：在methods方法中
 	// 根据id删除商品
        async removeById(id) {
        const confirmResult = await this.$confirm(
        '此操作将永久删除该商品, 是否继续?',
        '提示',
        {
          confirmButtonText: '确定',
          cancelButtonText: '取消',
          type: 'warning'
        }
        ).catch(err => err)

        if (confirmResult !== 'confirm') {
            return this.$message.info('已经取消删除！')
        }

        const { data: res } = await this.$http.delete(`goods/${id}`)

        if (res.meta.status !== 200) {
            return this.$message.error('删除失败！')
        }
        // 删除成功
        this.$message.success('删除成功！')
        // 刷新数据列表
        this.getGoodsList()
        }

```

#### 9.商品列表-通过编程式导航跳转到商品添加页

```vue
第一步：为添加商品按钮绑定事件   @click="goAddpage"
第二步：在methods方法中
	goAddpage() {
      this.$router.push('/goods/add')
    }
第三步：在goods文件夹下，新建Add.vue组件
第四步：在router.js导入Add.vue组件，在home的children属性中添加路由规则
```

#### 10.商品添加-渲染添加页面的基本结构

** Alert警告**

** Steps进度条--含状态步骤条**

el-steps 标签属性

1. align-center       让进度条居中显示
2. :active="0"        控制激活项的索引，激活第一项索引为0        :active="activeIndex - 0"      将字符串转化为数字的方法    "字符串-0"

```vue
第一步：复制粘贴代码
	Alert警告代码
	Steps进度条代码
第二步：在element.js，全局注册Step/Steps
```

#### 11.商品添加-美化步骤条组件

```vue
第一步：在global.css样式中
.el-steps {
    margin: 15px 0;
}

.el-step__title {
    font-size: 13px!important;
}
第二步：在data数据中
	1.activeIndex: 0
```

#### 12.商品添加-渲染tab栏区域

** Tabs标签页**

1. 可以通过 `tab-position` 设置标签的位置  :tab-position="'left'" 

```vue
第一步：将对应的结构复制粘贴到el-steps标签下面

```

#### 13.商品添加-实现步骤条和tab栏的数据联动效果

```vue
 代码演示：
<!-- 步骤条区域 -->
      <el-steps 
      :space="200" 
      :active="activeIndex - 0"     因为步骤条要求传递数字，所以将字符串转化为数字的方法    "字符串-0"
      finish-status="success" 
      align-center>
        <el-step title="基本信息"></el-step>     索引为0   对应 name="0"
        <el-step title="商品参数"></el-step>     索引为1   对应 name="1"
        <el-step title="商品属性"></el-step>     索引为2   对应 name="2"
        <el-step title="商品图片"></el-step>     索引为3   对应 name="3"
        <el-step title="商品内容"></el-step>     索引为4   对应 name="4"
        <el-step title="完成"></el-step>
      </el-steps>

<el-tabs v-model="activeIndex"  :tab-position="'left'">
    <el-tab-pane label="基本信息" name="0">用户管理</el-tab-pane>
    <el-tab-pane label="商品参数" name="1">商品参数</el-tab-pane>
    <el-tab-pane label="商品属性" name="2">商品属性</el-tab-pane>
    <el-tab-pane label="商品图片" name="3">商品图片</el-tab-pane>
  	<el-tab-pane label="商品内容" name="4">商品内容</el-tab-pane>
</el-tabs>

<script>
  export default {
    data() {
      return {
        activeIndex: '0'
      }
    }
  }
</script>
思路：
对于el-tabs标签页来说，它具有v-model属性，用于指定激活的是哪个面板
如果点击是第一个面板用户管理，会将这个面板的name属性值绑定到v-model的值activeName身上

我们只需要让el-tabs的v-model属性和el-steps的active属性绑定到同一个值身上，就可以了
核心实现思路：让el-tabs和el-steps这两个组件，共用同一个数据项activeIndex就可以了。

实现过程：点击不同的面板就会修改activeIndex的值，这个值就会绑定到步骤条身上
```

#### 14.商品添加-分析表单的组成部分

** Form表单**

1. 表单域标签的位置，如果值为 left 或者 right 时，则需要设置 `label-width`      可选值  right/left/top
2. label-position="top"    效果是：文字在上，文本框在下。

```vue
第一步：在el-tabs标签之外，放el-form进行包裹   el-form>el-tabs>el-tab-pane

第二步：在data数据中，定义
1.添加商品的表单数据对象   addForm: {}
2.验证规则    addFormRules: {}

```

#### 15.商品添加-绘制基本信息面板的UI结构

```vue
第一步:添加结构代码
		<el-tab-pane label="基本信息" name="0">
            <el-form-item label="商品名称" prop="goods_name">
              <el-input v-model="addForm.goods_name"></el-input>
            </el-form-item>
            <el-form-item label="商品价格" prop="goods_price">
              <el-input v-model="addForm.goods_price" type="number"></el-input>
            </el-form-item>
            <el-form-item label="商品重量" prop="goods_weight">
              <el-input v-model="addForm.goods_weight" type="number"></el-input>
            </el-form-item>
            <el-form-item label="商品数量" prop="goods_number">
              <el-input v-model="addForm.goods_number" type="number"></el-input>
            </el-form-item>
          </el-tab-pane>
第二步：在data数据中，完善信息
	// 添加商品的表单数据对象
      addForm: {
        goods_name: '',
        goods_price: 0,
        goods_weight: 0,
        goods_number: 0
      },
      addFormRules: {
        goods_name: [
          { required: true, message: '请输入商品名称', trigger: 'blur' }
        ],
        goods_price: [
          { required: true, message: '请输入商品价格', trigger: 'blur' }
        ],
        goods_weight: [
          { required: true, message: '请输入商品重量', trigger: 'blur' }
        ],
        goods_number: [
          { required: true, message: '请输入商品数量', trigger: 'blur' }
        ]
      }
```

#### 16.商品添加-获取商品分类数据

- 请求路径：categories
- 请求方法：get
- 响应数据

```vue
{
    "data": [
        {
            "cat_id": 1,
            "cat_name": "大家电",
            "cat_pid": 0,
            "cat_level": 0,
            "cat_deleted": false,
            "children": [
                {
                    "cat_id": 3,
                    "cat_name": "电视",
                    "cat_pid": 1,
                    "cat_level": 1,
                    "cat_deleted": false,
                    "children": [
                        {
                            "cat_id": 6,
                            "cat_name": "曲面电视",
                            "cat_pid": 3,
                            "cat_level": 2,
                            "cat_deleted": false
                        },
                        {
                            "cat_id": 7,
                            "cat_name": "海信",
                            "cat_pid": 3,
                            "cat_level": 2,
                            "cat_deleted": false
                        }
                    ]
                }
            ]
        }
    ],
    "meta": {
        "msg": "获取成功",
        "status": 200
    }
}
```

```vue
第一步：在data数据中，定义
	1.商品分类列表  catelist: []

第二步：在created函数中，调用   this.getCateList()

第三步：在methods方法中
// 获取所有商品分类数据
    async getCateList() {
      const { data: res } = await this.$http.get('categories')
      if (res.meta.status !== 200) {
        return this.$message.error('获取商品分类数据失败！')
      }
      this.catelist = res.data   将返回的数据保存在商品分类列表数组
      console.log(this.catelist)
    }
```

#### 17.商品添加-绘制商品分类的级联选择器

** 级联选择器--基础用法**

```vue
第一步：在商品数量后面，添加商品分类
			<el-form-item label="商品分类" prop="goods_cat">     添加效验规则
              <el-cascader  
              :options="catelist"  定义catelist
              :props="cateProps"   首先在data数据中，定义cateProps
              v-model="addForm.goods_cat"  定义商品所属的分类数组
              @change="handleChange"   定义handleChange事件         
              >
              </el-cascader>
            </el-form-item>
第二步：在data数据中，定义
 	cateProps: {
        label: 'cat_name',
        value: 'cat_id',
        children: 'children'
    },
	addForm: {
        // 商品所属的分类数组
        goods_cat: []
	}，
	addFormRules: {
      goods_cat: [
          { required: true, message: '请选择商品分类', trigger: 'blur' }
        ]
	}
	
第三步：在methods方法中，定义handleChange
// 级联选择器选中项变化，会触发这个函数
    handleChange() {
      console.log(this.addForm.goods_cat)
.......................................................商品添加-只允许选中三级商品分类
      if (this.addForm.goods_cat.length !== 3) {
        this.addForm.goods_cat = []
      }
    }
```

#### 18.商品添加-阻止页签切换

** Tabs页签**

* before-leave   切换标签之前的钩子，若返回 false 或者返回 Promise 且被 reject，则阻止切换。

  Function(activeName, oldActiveName)  

  第一个形参，表示即将进入的标签页的name

  第二个形参，表示即将离开的标签页的name

只有选中了商品分类中的三级商品分类，才允许页签切换、修改其他的商品的信息

思路：1.监听标签页的切换事件，然后在事件的处理函数中判断当前是否处于第一个页签

​	       还要判断选中的是否是三级商品分类(判断商品分类的数组长度是否等于3)

​		如果数组长度≠3，阻止页签切换

​		如果数组长度=3，允许页签切换

```vue
第一步：为el-tabs添加   :before-leave="beforeTabLeave" 
第二步：在methods方法中
 beforeTabLeave(activeName, oldActiveName) {
      // console.log('即将离开的标签页名字是：' + oldActiveName)
      // console.log('即将进入的标签页名字是：' + activeName)
      // return false  写在这里，表示一直阻止标签页的切换，这是不合理的！应该有条件的阻止

      // 如果即将离开标签页的名字为0且选中的商品分类的长度≠3，就阻止标签页的切换
      if (oldActiveName === '0' && this.addForm.goods_cat.length !== 3) {
        this.$message.error('请先选择商品分类！')
        // return false  阻止标签页的切换
        return false
      }
	  //允许切换
   }
```

#### 19.商品添加-获取动态参数列表数据

- 请求路径：categories/:id/attributes
- 请求方法：get
- 请求参数
  - :id  分类 ID  不能为空`携带在url中`  
  - sel  需要指定many 来获取动态参数
- 响应数据

```vue
{
    "data": [
        {
            "attr_id": 1,
            "attr_name": "cpu",
            "cat_id": 22,
            "attr_sel": "only",
            "attr_write": "manual",
            "attr_vals": "ffff"
        }
    ],
    "meta": {
        "msg": "获取成功",
        "status": 200
    }
}
```

```vue
第一步：为el-tabs标签绑定事件   @tab-click="tabClicked"  tab 被选中时触发

第二步：在created函数中，将三级分类的id设置为计算属性
 cateId() {
      if (this.addForm.goods_cat.length === 3) {
        return this.addForm.goods_cat[2]
      }
      return null
 }

第三步：在data数据中
	// 1.动态参数列表数据
      manyTableData: []
	
第四步：在methods方法中
async tabClicked() {
      // console.log(this.activeIndex)
      // 如果this.activeIndex === '1'，证明访问的是动态参数面板
      if (this.activeIndex === '1') {
        const { data: res } = await this.$http.get(
          `categories/${this.cateId}/attributes`,
          {
            params: { sel: 'many' }  表示获取动态参数的数据
          }
        )

        if (res.meta.status !== 200) {
          return this.$message.error('获取动态参数列表失败！')
        }
		// 获取动态参数成功
        console.log(res.data)

	.....绘制商品参数面板中的复选框组,适用于多个勾选框绑定到同一个数组的情景.....使用字符串分隔形成数组...............
        res.data.forEach(item => {
          item.attr_vals =
            item.attr_vals.length === 0 ? [] : item.attr_vals.split(' ')
        })
        this.manyTableData = res.data                   将动态参数数据保存到manyTableData

    .....................如果this.activeIndex === '2'，证明访问的是静态属性面板..................................
      } else if (this.activeIndex === '2') {
        const { data: res } = await this.$http.get(
          `categories/${this.cateId}/attributes`,
          {
            params: { sel: 'only' }
          }
        )

        if (res.meta.status !== 200) {
          return this.$message.error('获取静态属性失败！')
        }

        console.log(res.data)
        this.onlyTableData = res.data
      }
  }
```

#### 20.商品添加-绘制商品参数面板中的复选框组

** CheckBox复选框--多选框组**

1. el-checkbox-group   v-model="item.attr_vals"   双向绑定到一个数组

```vue
第一步：tabClicked函数中，完善代码
	** 获取到服务器返回的数据之后，首先先判断数据的长度=0？           
		如果数据长度≠0，将数据进行for循环每循环一个都会生成item项，
		将item.attr_vals用空格分割，就会得到attr_vals数组
		拿到attr_vals数组之后，就可以渲染为复选框组(因为复选框组  适用于多个勾选框绑定到同一个数组的情景) ** 
 		res.data.forEach(item => {
          item.attr_vals =  item.attr_vals.length === 0 ? [] : item.attr_vals.split(' ')
        })
        this.manyTableData = res.data        将动态参数数据保存到manyTableData数组中

第二步：完成商品参数
		<el-tab-pane label="商品参数" name="1">
            <!-- 1.渲染表单的Item项 -->
            <el-form-item :label="item.attr_name" v-for="item in manyTableData" :key="item.attr_id">
              <!-- 2.复选框组  适用于多个勾选框绑定到同一个数组的情景，通过是否勾选来表示这一组选项中选中的项 -->
              <el-checkbox-group v-model="item.attr_vals">    绑定到每一项的attr_vals数组身上
                <el-checkbox :label="cb" v-for="(cb, i) in item.attr_vals" :key="i" border></el-checkbox>
              </el-checkbox-group>
            </el-form-item>
          </el-tab-pane>

第三步：在element.js中，全局注册CheckboxGroup/Checkbox

第四步：优化复选框的样式，在style样式中
.el-checkbox {
  margin: 0 10px 0 0 !important;
}
```

#### 21.商品添加-获取静态属性列表数据

- 请求路径：categories/:id/attributes
- 请求方法：get
- 请求参数 
  * :id  分类 ID  不能为空`携带在url中` 
  * sel 需要指定only 获取分类静态参数

```vue
第一步：在data数据中，定义
	// 静态属性列表数据
      onlyTableData: []

第二步：在tabClicked函数中
	else if (this.activeIndex === '2') {
        const { data: res } = await this.$http.get(
          `categories/${this.cateId}/attributes`,
          {
            params: { sel: 'only' }
          }
        )

        if (res.meta.status !== 200) {
          return this.$message.error('获取静态属性失败！')
        }

        console.log(res.data)
        this.onlyTableData = res.data      将静态数组数据保存到onlyTableData数组中
      }
```

#### 22.商品添加-渲染商品属性面板的UI结构

```vue
完善商品属性代码
		<el-tab-pane label="商品属性" name="2">
            <el-form-item :label="item.attr_name" v-for="item in onlyTableData" :key="item.attr_id">
              <el-input v-model="item.attr_vals"></el-input>
            </el-form-item>
        </el-tab-pane>
```

#### 23.商品添加-初步使用upload上传组件

- 请求路径：upload
- 请求方法：post
- 请求参数
  * file    上传文件
- 响应数据

```vue
{
    "data": {
        "tmp_path": "tmp_uploads/ccfc5179a914e94506bcbb7377e8985f.png",
        "url": "http://127.0.0.1:8888tmp_uploads/ccfc5179a914e94506bcbb7377e8985f.png"
    },
    "meta": {
        "msg": "上传成功",
        "status": 200
    }
}
```

** Upload上传--图片列表缩略图**

1. :action="uploadURL"                      表示上传图片的URL地址，必须是后台的地址
2. :on-preview="handlePreview"     指定预览事件
3. list-type="picture"                         指定当前预览组件的呈现方式
4. headers                                            接收上传的请求头

```vue
第一步：在element.js中，全局注册upload组件

第二步：在data数据中，定义
	// 1.上传图片的URL地址
    uploadURL: 'http://127.0.0.1:8888/api/private/v1/upload',
	// 2.因为上传组件没有调用axios，所以需要手动为upload组件绑定headers请求头对象   图片上传组件的headers请求头对象
      headerObj: {
        Authorization: window.sessionStorage.getItem('token')
      },

第三步：完善商品图片
		<el-tab-pane label="商品图片" name="3">
            <!-- action 表示图片要上传到的后台API地址 -->
            <el-upload 
            :action="uploadURL" 
            :on-preview="handlePreview" 
            :on-remove="handleRemove" 
            list-type="picture" 
            :headers="headerObj"    需要手动为upload组件绑定headers请求头对象
            :on-success="handleSuccess">
              <el-button size="small" type="primary">点击上传</el-button>
            </el-upload>
          </el-tab-pane>

第四步：在methods方法中
	// 处理图片预览效果
    handlePreview(file) {
      console.log(file)
      this.previewPath = file.response.data.url
      this.previewVisible = true
    },
    // 处理移除图片的操作
    handleRemove(file) {
      // console.log(file)
      // 1. 获取将要删除的图片的临时路径
      const filePath = file.response.data.tmp_path
      // 2. 从 pics 数组中，找到这个图片对应的索引值
      const i = this.addForm.pics.findIndex(x => x.pic === filePath)
      // 3. 调用数组的 splice 方法，把图片信息对象，从 pics 数组中移除
      this.addForm.pics.splice(i, 1)
      console.log(this.addForm)
    },
    // 监听图片上传成功的事件
    handleSuccess(response) {
      console.log(response)
      // 1. 拼接得到一个图片信息对象
      const picInfo = { pic: response.data.tmp_path }
      // 2. 将图片信息对象，push 到pics数组中
      this.addForm.pics.push(picInfo)
      console.log(this.addForm)
    }

```

#### 24.商品添加-监听upload组件的on-success事件

```tex
处理图片上传成功之后的操作：
1.点击上传图片，上传完成以后并不意味操作结束；
  此时上传成功只代表服务器存储了这张图片，但是这张图片的相关信息还需要存储到添加表单中。
  
  pics指向一个数组，数组中包含每一个对象
  每一个对象代表成功上传的图片   
  每一个对象有pic属性，指向服务器返回的 图片的临时路径
  "pics":[
    	{"pic":"/tmp_uploads/30f08d52c551ecb447277eae232304b8"} 
    ]
```

** upload上传**

1. on-success    文件上传成功时的钩子   function(response, file, fileList)
   1. 第一个参数response      代表服务器返回的数据
   2. 第二个参数file                 文件的信息
   3. 第三个参数fileList           当前上传组件的文件列表

```vue
第一步：为el-upload标签添加  :on-success="handleSuccess"

第二步：在methods方法中
	// 监听图片上传成功的事件
    handleSuccess(response) {
      console.log(response)
      // 1. 拼接得到一个图片信息对象   
      const picInfo = { pic: response.data.tmp_path }       ** 首先为addForm对象添加属性  pics: [] **
      // 2. 将图片信息对象，push 到pics数组中                 ** 将服务器返回的数据以对象的形式添加到pics数组中 **
      this.addForm.pics.push(picInfo)
      console.log(this.addForm)
    }

第三步：在data数据中，为addForm对象添加属性  pics: []
addForm: {
  // 图片的数组
  pics: []
}
```

#### 25.商品添加-监听upload组件的on-remove事件

```tex
触发移除事件的时候，立即拿到移除图片的信息
1.获取将要删除的图片的临时路径
2.从 pics 数组中，找到这个图片对应的索引值
3.调用数组的 splice 方法，把图片信息对象，从 pics 数组中移除
```



** upload上传**

1. on-remove    文件列表移除文件时的钩子  function(file, fileList)
   1. 第一个形参file   将要被移除的信息对象
   2. 第二个形参fileList

```vue
第一步：为el-upload标签，添加  :on-remove="handleRemove" 
第二步：在methods方法中  
// 处理移除图片的操作
    handleRemove(file) {
      // console.log(file)

      // 1. 获取将要删除的图片的临时路径
      const filePath = file.response.data.tmp_path

      // 2. 从 pics 数组中，找到这个图片对应的索引值  
            ** 形参x表示数组pics中的每一项，将对应这一项的索引值i返回 **
      const i = this.addForm.pics.findIndex(x => x.pic === filePath) 
		
      // 3. 调用数组的 splice 方法，把图片信息对象，从 pics 数组中移除
      this.addForm.pics.splice(i, 1)
      console.log(this.addForm)
    }
```

#### 26.商品添加-实现图片的预览效果

```tex
监听el-upload组件的on-preview事件                                :on-preview="handlePreview" 
在预览的事件处理函数handlePreview中接收了将要预览的图片的信息file   handlePreview(file) {}
从图片信息中得到了图片的完整路径data.url                           this.previewPath = file.response.data.url
然后在页面上放置预览窗口，为预览窗口的图片，动态绑定预览图片的地址    :src="previewPath" 
最后将对话框显示，就可以实现图片的预览效果了！                      this.previewVisible = true
```



** upload上传**

1. on-preview   点击文件列表中已上传的文件时的钩子   function(file)
   1. 第一个形参file  表示预览图片的信息

** Dialog对话框**

1. 将对话框结构，复制粘贴到el-card标签的下面

```vue
第一步：在data数据中，定义
	1.预览路径                    previewPath: ''
	2.隐藏或者显示图片预览对话框   previewVisible: false

第二步：将对话框结构，复制粘贴到el-card标签的下面
<!-- 图片预览 -->
    <el-dialog title="图片预览" :visible.sync="previewVisible" width="50%">   **首先在data数据中定义 previewVisible: false**
      <img :src="previewPath" alt="" class="previewImg">
    </el-dialog>

第三步：为el-upload标签添加  :on-preview="handlePreview" 

第四步：在methods方法中
	// 处理图片预览效果
    handlePreview(file) {
      console.log(file)
      this.previewPath = file.response.data.url
      this.previewVisible = true   显示图片预览对话框
    }

第五步：在style样式中
.previewImg {
  width: 100%;
}

```

#### 27.商品添加-安装并配置富文本编辑器 vue-quill-editor

```vue
第一步：在可视化面板--依赖--运行依赖    vue-quill-editor

第二步：在main.js中
	1.导入富文本编辑器
	import VueQuillEditor from 'vue-quill-editor'
	2.导入富文本编辑器对应的样式
	import 'quill/dist/quill.core.css'
	import 'quill/dist/quill.snow.css'
	import 'quill/dist/quill.bubble.css'
	3.将富文本编辑器注册为全局可用的组件
	Vue.use(VueQuillEditor)

第三步：在global.css样式中
.ql-editor {
    min-height: 300px;
}
第四步：在style样式中
.btnAdd {
  margin-top: 15px;
}
第五步：在data数据中
addForm: {
  // 商品的详情描述
  goods_introduce: ''
}

第六步：添加富文本编辑器结构
		<el-tab-pane label="商品内容" name="4">
            <!-- 富文本编辑器组件 -->
            <quill-editor v-model="addForm.goods_introduce"></quill-editor>             ** 双向数据绑定**
            <!-- 添加商品的按钮 -->
            <el-button type="primary" class="btnAdd" @click="add">添加商品</el-button>   **添加点击事件**
          </el-tab-pane>

第七步：在methods方法中
// 添加商品
    add() {
	  console.log(this.addForm);
.........................................................实现表单数据的预验证
      this.$refs.addFormRef.validate(async valid => {
        if (!valid) {
          return this.$message.error('请填写必要的表单项！')
        }
................参考28.商品添加...........................................执行添加的业务逻辑
        // lodash   cloneDeep(obj)
        const form = _.cloneDeep(this.addForm)          **深拷贝对象，拷贝的新对象命名为form**
        form.goods_cat = form.goods_cat.join(',')       **把form对象中的goods_cat数组转化为字符串**
		console.log(form)
.......................参考29.商品添加........循环动态参数列表.................................处理动态参数
				客户在页面上所勾选的商品参数和和填写的静态属性，都要存储在attrs数组中
				此时这些数据保存在newInfo对象中，所以将newInfo对象添加到数组attrs
        this.manyTableData.forEach(item => {
          const newInfo = {
            attr_id: item.attr_id,
            attr_value: item.attr_vals.join(' ')    ** 将动态参数的attr_vals数组转换为字符串 **
          }
          this.addForm.attrs.push(newInfo)          ** 将newInfo对象添加到数组attrs **
        })
........................参考29.商品添加........循环静态参数列表.........................处理静态属性
				客户在页面上所勾选的商品参数和填写的静态属性，都要存储在attrs数组中
				此时这些数据保存在newInfo对象中，所以将newInfo对象添加到数组attrs
        this.onlyTableData.forEach(item => {
          const newInfo = { attr_id: item.attr_id, attr_value: item.attr_vals }    ** 静态属性的attr_vals是字符串 **
          this.addForm.attrs.push(newInfo)                                         ** 将newInfo对象添加到数组attrs **
        })
        form.attrs = this.addForm.attrs     将 this.addForm.attrs 保存在 新对象form的attrs中
        console.log(form)

...............................................................................................发起请求添加商品
        // 商品的名称，必须是唯一的.                 
        const { data: res } = await this.$http.post('goods', form)           ** 请求路径：goods，请求方式：post **

        if (res.meta.status !== 201) {
          return this.$message.error('添加商品失败！')
        }

        this.$message.success('添加商品成功！')
        this.$router.push('/goods')                  ** 编程式导航跳转到商品列表页面 **
      })
    }

```

#### 28.商品添加-把goods_cat从数组转化为字符串

```vue
通过表单的预校验之后，准备发起数据请求
但是在发起请求之前需要对表单里面的数据进行处理
当前请求的接口：
请求路径：goods
请求方式：post
请求参数中有一项goods_cat 以为','分割的商品分类的id列表   "goods_cat": "1,2,3"
goods_cat指定的值需要是字符串,里面以逗号分隔 一级 二级 三级商品分类的列表
但是此时addForm中的goods_cat是一个数组，里面存着每个分类的id  goods_cat: []
所以在发起请求之前把goods_cat从数组转化为字符串

此时运行，后台会报错！
因为级联选择器el-cascader的v-model="addForm.goods_cat"，要求双向绑定到一个数组，
但是此时我们把goods_cat从数组转化为字符串,所以会报错！

解决方法：在操作goods_cat之前对addForm对象进行深拷贝
深拷贝：把这个对象原封不动的拷贝出一个新的对象，和原对象互不相关！
怎么做深拷贝呢？
使用lodash包  它上面有一个cloneDeep函数  cloneDeep(obj)  obj指拷贝的对象
只有调用了lodash的cloneDeep函数，就会将obj原封不动的拷贝出一个新的对象，
我们可以操作新的对象，就不会报错了

级联选择器el-cascader的v-model="addForm.goods_cat"，双向绑定到一个数组
这个数组还是绑定到原对象上
我们进行join拼接的时候，操作的是拷贝的新对象，这样就不会报错了！
 
具体做法：
第一步：在运行面板--依赖--运行依赖--lodash
第二步：在Add.vue中的script刚开始引入  import _ from 'lodash'
<script>
	import _ from 'lodash'    **官方规定命名为下划线**
    export default {}
</script>
第三步：在Add函数中，执行添加的业务逻辑   lodash   cloneDeep(obj)
        const form = _.cloneDeep(this.addForm)      深拷贝对象，拷贝的新对象命名为form,
        form.goods_cat = form.goods_cat.join(',')   然后就将form中的goods_cat数组转换为字符串
```

#### 29.商品添加-处理attrs数组

```vue
当前请求的接口：
请求路径：goods
请求方式：post
请求参数中有一项attrs    商品的参数（数组），包含动态参数和静态属性
"attrs":[
    {
      "attr_id":15,
      "attr_value":"ddd"
    },
    {
      "attr_id":15,
      "attr_value":"eee"
    }
]

** 客户在页面上所勾选的商品参数和静态属性，都要存储在attrs数组中 **

第一步：在data数据的addForm中添加  attrs: []
第二步：在add函数中，处理动态参数和静态属性的逻辑   ** 参考27.商品添加 **
```

#### 30.分支操作-将goods_list分支提交到玛云

```vue
在项目根目录，运行：
1.git branch    当前处于goods_list分支
2.git status
3.git add .
4.git commit -m "完成了商品列表功能开发"  此时本地goods_list分支中的代码是最新的
5.git status
6.git push                将本地goods_list分支中的代码，推送到玛云goods_list分支
7.git checkout master     首先切换到master主分支
8.git merge goods_list    此时master主分支中的代码是最新的
9.git push                将本地master主分支中的代码，推送到玛云master主分支
```

### 订单列表order组件

#### 1.分支操作-创建order子分支

```vue
在项目根目录，运行：
1.git branch  当前处于master主分支
2.git checkout -b order   创建order子分支
3.git branch   当前处于order子分支
4.git push -u origin order   在玛云创建order子分支
```

#### 2.订单列表-通过路由渲染订单列表页面

```vue
第一步：在components下，新建order文件夹/新建Order.vue组件

第二步：在router.js中导入Order.vue组件
在home路由的children属性中添加路由规则

第三步：完善页面结构
<template>
    <div>
        <!-- 面包屑导航区域 -->
        <el-breadcrumb separator-class="el-icon-arrow-right">
            <el-breadcrumb-item :to="{ path: '/home' }">首页</el-breadcrumb-item>
            <el-breadcrumb-item>订单管理</el-breadcrumb-item>
            <el-breadcrumb-item>订单列表</el-breadcrumb-item>
        </el-breadcrumb>

        <!-- 卡片视图 -->
        <el-card>
            <!-- 搜索区域 -->
            <el-row>
                <el-col :span="8">
                    <el-input
                    placeholder="请输入内容"
                    clearable
                    >
                    <el-button slot="append" icon="el-icon-search"></el-button>
                    </el-input>
                </el-col>
            </el-row>
            <!-- 表格区域 -->
        </el-card>
    </div>
</template>
```

#### 3.订单列表-根据分页获取订单列表数据

接口文档1.10.1       订单数据列表

```vue
第一步：在data数据中，定义
	1.查询对象queryInfo
            queryInfo: {
                query: '',
                pagenum: 1,
                pagesize: 10
            }
	2.总数据条数 total: 0,
 	3.订单列表    orderlist: []
           
第二步：在created函数中调用  this.getOrderList()

第三步：在methods方法中
		async getOrderList(){
            const {data: res} = await this.$http.get('orders',{
                params: this.queryInfo
            })
            if(res.meta.status!==200){
                return this.$message.error('获取订单列表失败！')
            }
            console.log(res);
            this.total = res.data.total
            this.orderlist = res.data.goods
            
        }

```

#### 4.订单列表-渲染订单table表格

```vue
在el-row标签下面，添加下面内容：
<!-- 订单列表数据 -->
      <el-table :data="orderlist" border stripe>
        <el-table-column type="index"></el-table-column>
        <el-table-column label="订单编号" prop="order_number"></el-table-column>
        <el-table-column label="订单价格" prop="order_price"></el-table-column>
        <el-table-column label="是否付款" prop="pay_status">
          <template slot-scope="scope">
            <el-tag type="success" v-if="scope.row.pay_status === '1'">已付款</el-tag>
            <el-tag type="danger" v-else>未付款</el-tag>
          </template>
        </el-table-column>
        <el-table-column label="是否发货" prop="is_send">
          <template slot-scope="scope">
            <template>
              {{scope.row.is_send}}
            </template>
          </template>
        </el-table-column>
        <el-table-column label="下单时间" prop="create_time">
          <template slot-scope="scope">
            {{scope.row.create_time | dateFormat}}
          </template>
        </el-table-column>
        <el-table-column label="操作">
          <template slot-scope="scope">
            <el-button size="mini" type="primary" icon="el-icon-edit"></el-button>
            <el-button size="mini" type="success" icon="el-icon-location"></el-button>
          </template>
        </el-table-column>
      </el-table>
```

#### 5.订单列表-实现分页功能

** Pagination 分页**

```vue
第一步：在el-table标签下面，添加下面内容：
	<!-- 分页区域 -->
            <el-pagination 
            @size-change="handleSizeChange" 
            @current-change="handleCurrentChange" 
            :current-page="queryInfo.pagenum" 
            :page-sizes="[5, 10, 15]" 
            :page-size="queryInfo.pagesize" 
            layout="total, sizes, prev, pager, next, jumper" 
            :total="total">
            </el-pagination>

第二步：在methods方法中
 	handleSizeChange(newSize) {
      this.queryInfo.pagesize = newSize
      this.getOrderList()
    },
    handleCurrentChange(newPage) {
      this.queryInfo.pagenum = newPage
      this.getOrderList()
    }
```

#### 6.订单列表-实现省市区县数据联动效果

```vue
第一步：为操作添加事件 @click="showBox"

第二步：复制粘贴对话框组件结构，放在el-card标签下面。
	<!-- 修改地址的对话框 -->
        <el-dialog 
        title="修改地址" 
        :visible.sync="addressVisible" 
        width="50%" 
        @close="addressDialogClosed">
        <el-form :model="addressForm" :rules="addressFormRules" ref="addressFormRef" label-width="100px">
            <el-form-item label="省市区/县" prop="address1">
            <el-cascader :options="cityData" v-model="addressForm.address1"></el-cascader>
            </el-form-item>
            <el-form-item label="详细地址" prop="address2">
            <el-input v-model="addressForm.address2"></el-input>
            </el-form-item>
        </el-form>
        <span slot="footer" class="dialog-footer">
            <el-button @click="addressVisible = false">取 消</el-button>
            <el-button type="primary" @click="addressVisible = false">确 定</el-button>
        </span>
        </el-dialog>

第三步：在data数据中，定义
 	addressVisible: false    ** 关闭对话框 **
	addressForm: {
        address1: [],   将来是一个级联选择器，所以定义为数组
        address2: ''    是一个文本输入框，定义为字符串就可以了
      }
	addressFormRules: {
        address1: [
          { required: true, message: '请选择省市区县', trigger: 'blur' }
        ],
        address2: [
          { required: true, message: '请填写详细地址', trigger: 'blur' }
        ]
      }
	cityData,
    progressVisible: false,
   
第四步：在methods方法中
 // 展示修改地址的对话框
    showBox() {
      this.addressVisible = true
    },
    addressDialogClosed() {
      this.$refs.addressFormRef.resetFields()   关闭对话框时，清空标签数据
    }

第五步：将cityData.js放在order文件夹里面，然后在script标签刚开始引入  import cityData from './citydata.js'
然后在data数据中，定义 cityData

第六步：在style样式中
.el-cascader {
  width: 100%;
}

第七步：为el-dialog对话框，添加close事件  @close="addressDialogClosed"

```

#### 7.订单列表-展示物流进度对话框并获取物流信息

1.10.5. 查看物流信息     

请求路径：/kuaidi/:id

请求方法：get

供测试的物流单号：1106975712662

```vue
第一步：为物流进度按钮，绑定事件  @click="showProgressBox"

第二步：复制粘贴对话框组件代码，放在修改地址对话框的下面
<!-- 展示物流进度的对话框 -->
    <el-dialog title="物流进度" :visible.sync="progressVisible" width="50%">
     	<span>这是一条信息</span>
    </el-dialog>

然后在data数据中，定义  progressVisible: false

第二步：在methods方法中
	async showProgressBox() {
      const { data: res } = await this.$http.get('/kuaidi/804909574412544580')

      if (res.meta.status !== 200) {
        return this.$message.error('获取物流进度失败！')
      }

      this.progressInfo = res.data      ** 首先在data数据中，定义progressInfo: [] **

      this.progressVisible = true       ** 展示物流进度对话框 **
      console.log(this.progressInfo)
    }


```

#### 8订单列表-手动导入并使用Timeline组件

** Timeline时间线**

```vue
第一步：将tiemline文件夹和timeline-item文件夹，放在plugins中
第二步：在element.js中导入相应的js文件
	import Timeline from './timeline/index.js'
	import TimelineItem from './timeline-item/index.js'
	Vue.use(Timeline)
	Vue.use(TimelineItem)
第三步：将Timeline时间线代码，放在物流对话框的内容区域
		<!-- 时间线 -->
            <el-timeline>
                <el-timeline-item v-for="(activity, index) in progressInfo" :key="index" :timestamp="activity.time">
                {{activity.content}}
                </el-timeline-item>
            </el-timeline>
第四步：在style样式中，引入时间线的样式
@import '../../plugins/timeline/timeline.css';
@import '../../plugins/timeline-item/timeline-item.css';
```

#### 9.分支操作-将本地order分支提交到玛云

```vue
在项目根目录，运行：
1.git branch    当前处于order子分支
2.git status
3.git add .
4.git commit -m "完成了订单功能开发"  此时本地order分支中的代码是最新的
5.git status
6.git push                将本地order分支中的代码，推送到玛云order分支
7.git checkout master     首先切换到master主分支
8.git merge order    此时master主分支中的代码是最新的
9.git push                将本地master主分支中的代码，推送到玛云master主分支

```

### report功能开发

#### 1.分支操作-创建report子分支

```vue
在项目根目录，运行：
1.git branch  当前处于master主分支
2.git checkout -b report   创建report子分支
3.git branch   当前处于report子分支
4.git push -u origin report   在玛云创建report子分支
```

#### 2.数据统计-通过路由加载数据报表组件

```vue
第一步：在components下，新建report文件夹/新建Report.vue组件

第二步：在router.js中，导入Report.vue组件
在home路由的children属性中，添加路由规则

第三步：完善组件结构
<template>
    <div>
        <!-- 面包屑导航区域 -->
        <el-breadcrumb separator-class="el-icon-arrow-right">
            <el-breadcrumb-item :to="{ path: '/home' }">首页</el-breadcrumb-item>
            <el-breadcrumb-item>数据统计</el-breadcrumb-item>
            <el-breadcrumb-item>数据报表</el-breadcrumb-item>
        </el-breadcrumb>
        <!-- 卡片视图区域 -->
        <el-card>
            123
        </el-card>
    </div>
</template>
```

#### 3.数据统计-安装Echarts并渲染Demo图表

```vue
第一步：在可视化面板--依赖--运行依赖--echarts

百度搜索：echarts--文档--教程（分为5步）
1.在script标签中，导入echarts  import echarts from 'echarts'

在卡片视图区域，放置 
	<!-- 2.为 ECharts 准备一个具备大小（宽高）的 DOM -->
    <div id="main" style="width: 600px;height:400px;"></div>

在mounted函数中     ** 此时，页面上的元素，已经被渲染完毕了！**
 	 mounted(){
         // 3.基于准备好的dom，初始化echarts实例
        var myChart = echarts.init(document.getElementById('main'));
        // 4.准备数据和配置项
        var option = {
            title: {
                text: 'ECharts 入门示例'
            },
            tooltip: {},
            legend: {
                data:['销量']
            },
            xAxis: {
                data: ["衬衫","羊毛衫","雪纺衫","裤子","高跟鞋","袜子"]
            },
            yAxis: {},
            series: [{
                name: '销量',
                type: 'bar',
                data: [5, 20, 36, 10, 10, 20]
            }]
        };
        // 5.展示数据--使用刚指定的配置项和数据显示图表
        myChart.setOption(option);
    },
```

#### 4.数据统计-获取折线图数据并渲染图表

1.11.1.  基于时间统计的折线图

- 请求路径：reports/type/1
- 请求方法：get
- 响应数据
- 需要合并的选项

```vue
options: {
        title: {
          text: '用户来源'
        },
        tooltip: {
          trigger: 'axis',
          axisPointer: {
            type: 'cross',
            label: {
              backgroundColor: '#E9EEF3'
            }
          }
        },
        grid: {
          left: '3%',
          right: '4%',
          bottom: '3%',
          containLabel: true
        },
        xAxis: [
          {
            boundaryGap: false
          }
        ],
        yAxis: [
          {
            type: 'value'
          }
        ]
      }
```

```vue
鼠标跟随效果：服务器返回的折线图的数据是不完整的，要想有鼠标跟随效果。
需要将服务器返回的数据res.data和文档中提供的options选项进行合并，得到一个新对象result
最终将合并的结果result赋值给   myChart.setOption(result)
问题：如何将两个对象合并得到一个新对象？
使用lodash的merge函数，可以合并两个对象    merge(对象1，对象2)
	1.在script标签中，导入  import _ from 'lodash'
	2.在准备数据和配置项     const result = _.merge(res.data, this.options)
	3. 展示数据             myChart.setOption(result)

<template>
  <div>
    <!-- 面包屑导航区域 -->
    <el-breadcrumb separator-class="el-icon-arrow-right">
      <el-breadcrumb-item :to="{ path: '/home' }">首页</el-breadcrumb-item>
      <el-breadcrumb-item>数据统计</el-breadcrumb-item>
      <el-breadcrumb-item>数据报表</el-breadcrumb-item>
    </el-breadcrumb>

    <!-- 卡片视图区域 -->
    <el-card>
      <!-- 2. 为ECharts准备一个具备大小（宽高）的Dom -->
      <div id="main" style="width: 750px;height:400px;"></div>
    </el-card>
  </div>
</template>

<script>
// 1. 导入 echarts
import echarts from 'echarts'
import _ from 'lodash'

export default {
  data() {
    return {
      ............将文档中的数据，放在这里.........................需要合并的数据
      options: {
        title: {
          text: '用户来源'
        },
        tooltip: {
          trigger: 'axis',
          axisPointer: {
            type: 'cross',
            label: {
              backgroundColor: '#E9EEF3'
            }
          }
        },
        grid: {
          left: '3%',
          right: '4%',
          bottom: '3%',
          containLabel: true
        },
        xAxis: [
          {
            boundaryGap: false
          }
        ],
        yAxis: [
          {
            type: 'value'
          }
        ]
      }
    }
  },
  created() {},
  // 此时，页面上的元素，已经被渲染完毕了！
  async mounted() {
    // 3. 基于准备好的dom，初始化echarts实例
    var myChart = echarts.init(document.getElementById('main'))
.........................................................................................发起请求获取数据
    const { data: res } = await this.$http.get('reports/type/1')
    if (res.meta.status !== 200) {
      return this.$message.error('获取折线图数据失败！')
    }
  
    // 4. 准备数据和配置项--合并两个对象，得到一个新的对象result
    const result = _.merge(res.data, this.options)

    // 5. 传入得到的新对象--展示数据
    myChart.setOption(result)
  },
  methods: {}
}
</script>

<style lang="less" scoped>
</style>

```

#### 5.分支操作-将本地的report子分支的上传玛云

```tex
在项目根目录，运行：
1.git branch    当前处于report子分支
2.git status
3.git add .
4.git commit -m "完成了报表功能的开发"  此时本地report分支中的代码是最新的
5.git status
6.git push                将本地report分支中的代码，推送到玛云report分支
7.git checkout master     首先切换到master主分支
8.git merge report    此时master主分支中的代码是最新的
9.git push                将本地master主分支中的代码，推送到玛云master主分支
```

#### 项目优化：

```tex
1.点击页面实现跳转的时候，添加进度条loading效果
具体实现步奏：
1.打开可视化面板：依赖--运行依赖--安装nprogress
2.在main.js中：导入Nprogress包对应的js和css
	import Nprogress from 'nprogress' 	**js实现进度条效果**
	import 'nprogress/nprogress.css'  	**css美化进度条**
	......................
	1.在request拦截器中，展示进度条  Nprogress.start()
		axios.interceptors.request.use(config=>{Nprogress.start()})   **展示进度条**
	2.在response拦截器中，隐藏进度条 Nprogress.done()
		axios.interceptors.response.use(config=>{Nprogress.done()})   **隐藏进度条**
```

#### 解决eslint与代码格式化冲突

```tex
...................运行server命令，产生的报错信息：
1.报错信息： Expected "[" and "]" to be on the same line   这两个符号应该在一行上（不应该换行）
  如果调整之后，保存！恢复原样，说明格式冲突
  解决：.prettierrc文件，添加 ["printWidth": 200]  默认是80  一行最多有多少个字符，如果超过就会换行
  
2.Identifier 'attr id' is not in camel case   attr id   不是驼峰命名
  
  
  
....................运行build命令，产生的报错信息：
运行build命令会生成gist目录，生成的gist目录就可以用于生成环境的发布了！
拿到发布文件期间，必须运行build命令！
1.报错信息：Unexpected console statement   项目发布期间，不允许出现console

```













































































































​	

  













