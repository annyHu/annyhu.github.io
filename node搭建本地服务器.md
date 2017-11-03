##nodeJS搭建本地服务器
##安装Node JS；

####安装全局express；在express4.x版本中，安装时语句变为了这样：

` npm install -g express-generator`

####创建项目：

选择模板：ejs jade

`express name -ejs`
`cd name`   # **进入创建的项目**

`npm install`  # **安装依赖**

####启动项目：

`npm start`


##nodeJS服务端部分
####在express目录下，安装cors包
`npm install cors --save  `

![image.png](http://upload-images.jianshu.io/upload_images/3780749-dbcc98307d8d24d6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
####在app.js中配置：开启cors 

![image.png](http://upload-images.jianshu.io/upload_images/3780749-47f24eec93293464.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```node
var cors = require('cors');

//...............

app.user(cors({
  origin: ['http://localhost:8080'],
  methods: ['GET', 'POST', 'PUT', 'DELETE'],
  allowHeaders: ['Content-Type', 'Authorization']
}));
```
####在routes/index.js中配置一条路由映射

![image.png](http://upload-images.jianshu.io/upload_images/3780749-fef5d211663efd2f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
```node
router.post('/first', function(req, res, next) {
  res.json({name:'aaa',pwd:'123'});
});
```
##vue端，
构建一个[vue](http://www.cnblogs.com/xuange306/p/6092225.html)项目
####访问服务器的方法
```vue
<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <button @click="getUser">点击获取node层的数据</button>
    <div v-html="serviceHtml">aa</div>
    <br/>
    <br/>
    <br/>
    <button @click="postUser">获取用户帐号</button>
    <p>{{account}}</p>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      serviceHtml: '',
      account: ''
    }
  },
  methods: {
    getUser () {
      axios({
        url: 'http://localhost:3000/',
        method: 'get'
      }).then((res) => {
        this.serviceHtml = res.data
        console.log(res.data, 565)
      })
    },
    postUser () {
      axios({
        url: 'http://localhost:3000/first',
        method: 'post'
      }).then((res) => {
        this.account = res.data
        console.log(res.data, 565)
      })
    }
  }
}
</script>
```
+  get获取到的node渲染的模版

![image.png](http://upload-images.jianshu.io/upload_images/3780749-6ab0500c178c24fe.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
+  post获取帐号信息

![image.png](http://upload-images.jianshu.io/upload_images/3780749-b02021b4ca1dfb81.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)














