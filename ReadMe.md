## csrf
```
跨站请求伪造
常见：转账，评论等
手段：钓鱼网站
    通过点击钓鱼网站，发送已知的数据格式和接口
    主要是表单提交, 并非使用ajax提交， 不存在跨域问题，提交时，自动带有对应域名下的cookie
预防手段：
    不能仅通过cookie进行验证客户的合法性，即可预防csrf
    1. 添加验证码(体验不好)
    2. 根据referer 判断来源
    3. token(加入到头部自定义（常规）或者post数据中，后端进行验证即可) ? express-captcha
     保证token的安全性，在跳转其他网站时，不需要添加token；黑客referer同样可以获取token(用户手动关闭)
     
参考：https://www.ibm.com/developerworks/cn/web/1102_niugang_csrf/index.html
```

## xss 
```
  跨站脚本攻击: cross site scripting
  攻击手段：注入非法html或者js片段 控制浏览器
  1. dom xss
    dom元素根据js动态更新页面展示，不需要服务器解析响应的直接参与。
  2. 反射型 xss
     非持久性Xss, 前端发送的内容含有可执行代码，后端响应中出现这段xss代码。httponly: false, 降低受损范围
  3. 存储型 xss
     比较隐蔽，危害性更大
     允许用户存储数据的 web 程序都可能存，在存储型 XSS 漏洞，当攻击者提交一段 XSS 代码后，被服务器接收并存储，当所有浏览器访问某个页
     面时都会被 XSS，其中最典型的例子就是留言板
  影响:
    显示伪造图片或文章
    利用虚假输入表单骗取个人用户信息.
    窃取cookie
  预防手段：
    httpOnly: true,降低受损范围，前端无法通过js获取cookie.
    过滤：前后端同时对常用表单：邮箱，电话号码，用户名，密码。。。进行格式校验.
    htmlEncode: 某些情况下，不能对用户数据进行严格过滤，需要对标签进行转,html进行转义
    JavaScriptEncode
```
