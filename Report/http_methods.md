# HTTP 请求方法一览

## GET

The GET method requests a representation of the specified resource. Requests using GET should only retrieve data and should have no other effect. (This is also true of some other HTTP methods.) The W3C has published guidance principles on this distinction, saying, "Web application design should be informed by the above principles, but also by the relevant limitations."

向指定的资源发出“显示”请求。使用GET方法应该只用在读取数据，而不应当被用于产生“副作用”的操作中，例如在 Web Application 中。其中一个原因是 GET 可能会被网络蜘蛛等随意访问。

## HEAD
The HEAD method asks for a response identical to that of a GET request, but without the response body. This is useful for retrieving meta-information written in response headers, without having to transport the entire content.

与 GET 方法一样，都是向服务器发出指定资源的请求。只不过服务器将不传回资源的本文部分。它的好处在于，使用这个方法可以在不必传输全部内容的情况下，就可以获取其中“关于该资源的信息”（元信息或称元数据）。

## POST
The POST method requests that the server accept the entity enclosed in the request as a new subordinate of the web resource identified by the URI. The data POSTed might be, for example, an annotation for existing resources; a message for a bulletin board, newsgroup, mailing list, or comment thread; a block of data that is the result of submitting a web form to a data-handling process; or an item to add to a database.

向指定资源提交数据，请求服务器进行处理（例如提交表单或者上传文件）。数据被包含在请求本文中。这个请求可能会创建新的资源或修改现有资源，或二者皆有。

## PUT
The PUT method requests that the enclosed entity be stored under the supplied URI. If the URI refers to an already existing resource, it is modified; if the URI does not point to an existing resource, then the server can create the resource with that URI.

向指定资源位置上传其最新内容。

## DELETE
The DELETE method deletes the specified resource.

请求服务器删除 Request-URI 所标识的资源。

## TRACE
The TRACE method echoes the received request so that a client can see what (if any) changes or additions have been made by intermediate servers.

回显服务器收到的请求，主要用于测试或诊断。

## OPTIONS

The OPTIONS method returns the HTTP methods that the server supports for the specified URL. This can be used to check the functionality of a web server by requesting '*' instead of a specific resource.

这个方法可使服务器传回该资源所支持的所有 HTTP 请求方法。用 '*' 来代替资源名称，向 Web 服务器发送 OPTIONS 请求，可以测试服务器功能是否正常运作。

## CONNECT

The CONNECT method converts the request connection to a transparent TCP/IP tunnel, usually to facilitate SSL-encrypted communication (HTTPS) through an unencrypted HTTP proxy.

HTTP/1.1 协议中预留给能够将连接改为管道方式的代理服务器。通常用于 SSL 加密服务器的链接（经由非加密的 HTTP 代理服务器）。

## PATCH（由 RFC 5789 指定的方法）

The PATCH method applies partial modifications to a resource.

用于将局部修改应用到资源。


|HTTP method|RFC|Request has Body|Response has Body	|Safe|Idempotent|Cacheable|
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
|GET|RFC 7231|Optional|YES|YES|YES|YES|
|HEAD|RFC 7231|NO|NO|YES|YES|YES|
|POST|RFC 7231|YES|YES|NO|NO|YES|
|OPTIONS|RFC 7231|Optional|YES|YES|YES|NO|
|TRACE|RFC 7231|NO|YES|YES|YES|NO|
|PUT|RFC 7231|YES|YES|NO|YES|NO|
|DELETE|RFC 7231|NO|YES|NO|YES|NO|
|CONNECT|RFC 7231|YES|YES|NO|NO|NO|
|PATCH|RFC 5789|YES|YES|NO|NO|NO|

## 参考
* [Hypertext Transfer Protocol](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol#Request_methods)


