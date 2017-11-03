###从NodeJS搭建中间层再谈前后端分离
####先介绍一下get和post请求在node中使用的不同
+  get请求：
前台：
```js
function login() {  
    var name = $('#name').val();  
    var password = $('#password').val();  
    if (!name || !password) {  
        alert('用户名和密码都不能为空');  
        return;  
    }  
    $.ajax(  
        {  

           type: 'get',  
            url: '/login',  
            data: {  
                name: name,  
                password: password  
            },  
            dataType: 'json',  
            success: function (data) {  
                if (data) {  
                }  
            },  
            error: function () {  
                alert('登录失败!');  
                return;  
            }  
        });  
}
```
后台：
```node
var express = require('express');  
var router = express.Router();  
router.get('/login', function (req, res, next) {  
    var name = req.query.name;  
    var pass = req.query.password;  
    console.log('name:' + name);  
    console.log('pass:' + pass);  
    if (name == 'sis' && pass == '1') {  
        res.send('1');  
    }  
    res.end('is over');  
});  
```
+  post请求：
前台：
```js
function login() {  
    var name = $('#name').val();  
    var password = $('#password').val();  
    if (!name || !password) {  
        alert('用户名和密码都不能为空');  
        return;  
    }  
    $.ajax(  
        {  

           type: 'post',  
            url: '/login',  
            data: {  
                name: name,  
                password: password  
            },  
            dataType: 'json',  
            success: function (data) {  
                if (data) {  
                }  
            },  
            error: function () {  
                alert('登录失败!');  
                return;  
            }  
        });  
}
```
后台：
```node
var express = require('express');  
var router = express.Router();  
router.post('/login', function (req, res, next) {  
    var name = req.body.name;  
    var pass = req.body.password;  
    console.log('name:' + name);  
    console.log('pass:' + pass);  
    if (name == 'sis' && pass == '1') {  
        res.send('1');  
    }  
    res.end('is over');  
});  
```
####我通过http模块对真实后台发起http请求，然后通过express模块搭建后端服务。
```node
// http.js
var formatURL = require('./formatURL.js'); // 拼接实际访问的服务器地址 
var http = require('http');
const POSThttp = function(request){
  return new Promise((resolve, reject) => {
    let body = '';
    // http模块拿到真实后台api的数据
    http.get(formatURL(request.body.musicname), function(res){
      res.on('data', (data) => {
        body += data;
      }).on('end', () => {
        // 格式化
        const {
          name,
          audio: musicUrl,
          page,
          album: {
            name: musicName,
            picUrl,
          },
          artists: [{
            name: singer,
          }],
        } = JSON.parse(body).result.songs[0];
        const reply = {
          name,
          picUrl,
          musicUrl,
          page,
          singer,
        };
        resolve(reply);
      });
    });
  });
};
module.exports = POSThttp;

```
####得到数据传回前端
```node
var express = require('express');
var POSThttp = require('./POSThttp.js');
var bodyParser = require('body-parser');
// 使用body-parser解析post请求的参数，如果没有，req.body为undefined。
var app = express();
app.use(bodyParser.json());
app.use(bodyParser.urlencoded({
  extended: true
}));
app.post('/', (req, res) => {
  POSThttp(req).then((data) => {
    res.send(data);
  }).catch((err) => {
    res.send(err);
  });
});
app.listen(3000, () => {
  console.log('open wx-audio server successful!')
});
```