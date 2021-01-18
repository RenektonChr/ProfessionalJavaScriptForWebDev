# JavaScript高级程序设计读书笔记

## ES6实现模块化时遇到的跨域问题
 
```javascript
<script src="./src/data.js" type="module"></script>
<script type="module">
  import func from './src/data.js';

  func()
</script>
```
 
解析：  
+ 这段代码在语法上是没有错误的。  
+ 在浏览器中以file协议的方式打开时，浏览器会报跨域的错误。
  + Access to script at xxx from origin 'null' has been blocked by CORS policy: Cross origin requests are only supported for protocol schemes: http, data, chrome, chrome-extension, chrome-untrusted, https.
+ 通过分析报错得出：访问脚本文件：xxx "from origin" null已被CORS策略阻止：跨源请求仅支持协议方案：http、data、chrome、chrome扩展、https。
+ 原因是HTML中 script 标签在使用type="module"时会默认产生跨域请求，我们是在本地打开的文件，但是file协议并不支持跨域请求。
  
解决方案：  
1. 部署到服务器上
2. Visual Studio Code下载Live Server 插件，使用插件打开。
  
- 注：script标签的type属性为module时，自动启动严格模式。
  
## script标签的解析问题  
 
使用了scr属性的script标签不应该再在saript标签中包含其他的JS代码，如果两者都提供的话，浏览器只会下载并执行外部脚本文件，从而忽略行内代码。  
### 推迟执行脚本  
解析：  
+ html4.01为script标签定义了一个defer的属性。这个属性表示脚本在执行的时候不会改变页面结构。也就是说，脚本会被延迟到整个页面机械完毕后再运行。  
+ 在script元素上设置defer属性，相当于告诉浏览器立即下载，但是延迟执行。  
+ defer属性对于外部脚本才有效。
  
### HTTP、HTTPS、SPDY、HTTP2  
+ HTTP：
