# 微信小程序+nginx

## 官方文档

[视图容器 / cover-image (qq.com)](https://developers.weixin.qq.com/miniprogram/dev/component/)

https://vant-contrib.gitee.io/vant-weapp/#/home（视图组件）

[登录 (dcloud.net.cn)](https://unicloud.dcloud.net.cn/pages/login/login?uniIdRedirectUrl=%2Fpages%2Findex%2Findex)（unicloud 在线存储）

### 开发模式

+ 申请小程序开发账号
+ 安装小程序开发者工具
+ 创建和配置小程序项目

### 官方示例

![image-20230627192626165](C:\Users\17994\AppData\Roaming\Typora\typora-user-images\image-20230627192626165.png)

## 准备工作

### 注册

1. [微信公众平台 (qq.com)](https://mp.weixin.qq.com/)
2. 注册->注册小程序->个人用户（无法使用支付等高级API）

### appID

1. [微信公众平台 (qq.com)](https://mp.weixin.qq.com/)
2. 开发管理->开发设置  wxcb0b019f86c44188

### 开发者工具下载

### 项目基本组成结构

1. pages 页面存放,每个文件以单独的文件夹存在
   1. index
      1. index.js   存放数据、处理函数
         + Page()函数创建并运行页面
      2. index.json 外观配置，该配置若与app.json冲突，以index.json为准
      3. index.wxml 模板结构文件（Weixin  Markup Language 类似HTML）
         + 标签名称 HTML（div，span,img,a） WXML(view,text,image,navigator)
         + 属性节点 HTML (<a href=''></a>>)  WXML(<navigator url=""></navigator>)
         + 类似Vue的模板语法 数据绑定 列表渲染 条件渲染
      4. index.wxss 样式表
         + 新增rpx尺寸单位，在不同大小屏幕进行自动单位换算
         + 提供全局和局部样式
         + 支持常用css选择器
   2. logs
2. utils 工具性质模块
3. app.js 入口文件
   + App（）函数启动程序
4. app.json 全局配置文件

~~~json
{
    //记录页面路径，并在此进行页面创建
  "pages":[
    "pages/index/index",
    "pages/logs/logs"
  ],
  "window":{
      //全局定义小程序所有页面的背景色、文字颜色等
    "backgroundTextStyle":"light",
    "navigationBarBackgroundColor": "#fff",
    "navigationBarTitleText": "Weixin",
    "navigationBarTextStyle":"black"
  },
    //全局定义小程序组件使用的样式版本  v2为新版样式
  "style": "v2",
    //指明sitemap.json的路径
  "sitemapLocation": "sitemap.json"
}

~~~

5. app.wxss 全局样式文件

6. project.config.json 项目配置文件
   + 详情-本地设置进行体现
7. sitemap.json 是否允许被索引

## JSON

+ JSON是一种数据格式，总是以配置文件的形式出现在开发过程中

## 错误与警告

+ The resource http://127.0.0.1:12612/appservice/__dev__/WAServiceMainContext.js?t=wechat&s=1687866803719&v=2.19.4 was preloaded using link preload but not used within a few seconds from the window's load event.  Please make sure it has an appropriate `as` value and it is preloaded intentionally.

  解决：详情->设置->禁用独立域调试

+ [sitemap 索引情况提示] 根据 sitemap 的规则[0]，当前页面 [pages/index/index] 将被索引

  解决：project.config.json->checkSiteMap=false

  修改：sitemap.json->"action": "allow/disallow"

+ [自动热重载] 已开启代码文件保存后自动热重载（不支持 json）

  解决：详情->设置->关闭热重载

## 使用

### 快捷键

~~~js
.xxx > .xxx
## 可以直接生成 view标签 并附有类名xxx
## 生成嵌套

.xxx{$}*8
## 可直接生成 view列表

alt+上下键
## 将正行代码上下移动

ctrl+a 
## 全选
~~~

### 标签

~~~css
view
## 块级标签

text
## 行级标签
~~~

### 特殊字符

~~~html
&lt; &gt; 
## < > 
~~~

### rpx

~~~html
## 响应式单位
~~~

### CSS补充

~~~css
white-space：nowrap
## 允许块元素排列至一行

display: inline-block;
## 行级块元素

text-align: center;
## 文字居中

display: flex
## 定义元素的显示方式，为弹性显示

align-items: center;
## 弹性容器中垂直轴上的对齐方式

justify-content: center;
## 弹性容器中水平轴上的对齐方式
justify-content: space-between；
## 子元素沿着主轴均匀分布，同时第一个子元素位于容器的起始位置，最后一个子元素位于容器的结束位置。

box-sizing: border-box;
## 用于指定元素的盒模型。指定border-box盒模型，设置一个元素的宽度为200像素，那么元素的整体宽度将是200像素，包括内容、边框和填充。

box-shadow:0 15rpx 40rpx rgba(0, 0, 0, 0.5);
## 用于为盒子添加阴影。
## 水平偏移（右）- 垂直偏移（下） - 模糊程度 - 颜色以及透明度

padding：10px 10px 10px 10px;
## 会以 上右下左 的顺序进行外填充

flex:1
## 弹性布局中，设置子元素相对大小

overflow: hidden;
## 将溢出部分进行隐藏
## 可解决：列表中子元素首个margin-top不起作用
## 根据规范，一个盒子如果没有上补白和上边框，那么它的上边距应该和其文档流中的第一个孩子元素的上边距重叠。
~~~

### 路径

~~~文理
/xxx/xxx
../../xxx/xxx
## 
~~~

### 标签属性

~~~css
hover-class=""
## 点击事件，修改css

bind:tap=""
## 点击事件，触发函数
## 参考文档 :https://developers.weixin.qq.com/miniprogram/dev/framework/view/wxml/event.html

data-xxx=""
## 传送数据
## 数值在 currentTarget.dataset 中
~~~

### js补充

~~~javascript
setTimeout(()=>{},2000)
/*
箭头函数,{}中书写函数体
此方法为计时器
*/

this.setData({name:""})
/*
由于内部需要传入的为一个结构体，因此需要加{}
该方法用于修改页面初始数据
*/

onClick(event){}，
/*
函数格式
event 用于接收前端参数
*/

console.log()
// 在控制台打印数据

parseInt(Math.random())
// 随机数取整

let x=`rgb(${xxx},${xxx},${xxx})`
// 模板字符串 , ${xxx} 变量引用

array.splice(index,howmany,item1,...,itemX)
// Array对象拼接删除操作。 下标，多少元素（0，1，5），添加到数组的新元素

array.push()
// 添加元素
~~~

### wxml语法

~~~html
<view>
  my name is : {{name}}
</view>
<!-- 使用{{ xxx }} 进行数据绑定 -->

<input model:value="{{value}}" />
<!-- 双向绑定 -->

<block></block>
<!-- 专门用于布局的标签，不会被渲染，不会破坏布局。可用于条件语句等功能 -->
~~~



## nginx

### window

+ 官网上下载安装即可
+ nginx基础操作

~~~nginx
nginx
## cmd 中来到nginx根目录下 启动nginx服务

nginx -s stop
## 停止服务

nginx -s reload
## 重启服务

~~~



+ 在 nginx.conf 中进行常见的配置更改

~~~nginx
server {
        listen       80;                                 //监听接口
        server_name  192.168.1.132;						 //本机的域名或ip地址

        location / {                                     //网址中显示路径
            root   html;								 //root 指令用于定义Nginx服务器上的根文件夹或文档根目录，当客户端请求一个URL时，Nginx将从root指定的目录开始查找文件，并将请求映射到该目录中的文件。
            index  index.html index.htm;  				 //Nginx会按照以下顺序查找并提供这些默认文件
        }

        location /images/ {
             alias D:/nginx/nginx-1.25.2/static/images/;  //用于将URL路径映射到不同于Nginx配置的根目录的文件夹或目录
             index index.html index.htm;
        }
        
        error_page   500 502 503 504  /50x.html;          //定义错误页面的处理方式  定义一组HTTP错误状态码 一个特定的错误页面
        location = /50x.html {							  // '='表示精确匹配
            root   html;								  // 查找错误页面的目录
        }
        }
~~~

