# HTML CSS

## HTML

```html
<!DOCTYPE html>
<html>
    <head>
        <titel></titel>
        <script> type="text/javascript" src="1.js"</script>
        <script type="text/javascript">
        var i=12;
        var j = 13
        alert(i+j)
        </script>
    </head>
    <body>
    <p></p>
    <div> </div>         
    </body>
</html>
```

## CSS

## Tomcat

## Servlet1



## http协议

 客户端给服务器发送数据叫请求。

服务器给客户端回传数据叫响应。

请求HTTP协议

GET请求

1. 请求行  GET

2. 请求头
   
   1. key:value

POST请求

1. 请求行
   
   1. 请求方式                     POST
   
   2. 请求的资源路径[+?+请求参数]
   
   3. 请求的协议的版本号           HTTP/1.1

2. 请求头
   
   1. key:value

3. 空行

4. 请求体

响应的HTTP协议

1. 响应行
   
   1. 响应协议和版本号
   
   2. 响应状态码
   
   3. 响应状态描述符

2. 响应头
   
   1. key:value

3. 空行

4. 响应体

## HttpServletRequest   HttpServletResponse

每次只要有请求进入 Tomcat 服务器，Tomcat 服务器就会把请求过来的 HTTP 协议信息解析好封装到 Request 对象中