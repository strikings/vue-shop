### 项目介绍：后台管理系统 + 后端接口

> * 后台管理系统：vue_shopping
> * 后端服务器：vue_api_server
>
> 第一步：打开PHPStudy,打开mysql数据。
>
> 1. 新建数据库`mydb`
>
> 2. 将数据库文件sql导入数据库（数据库文件位置：vue_api_server / db）
>
> 	//=>vue_api_server / config文件夹 / default.js （下面参数可以修改）
> 	
> 	数据库名称：mydb
> 	
> 	数据库用户名：root
> 	
> 	密码：12345678
> 	
> 	数据库默认端口：3306（固定端口，不能修改）
>
>
> 第二步：进入后台管理系统：vue_shopping
>
> ```
> cd vue_shopping
> npm i
> npm run serve
> ```
>
> 第三步：进入后端服务器：vue_api_server
>
> ```
> cd vue_api_server
> npm i
> node app.js
> ```
>
> 