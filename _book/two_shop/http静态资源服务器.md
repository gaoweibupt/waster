## http静态资源服务器

```
http.Handle("/static/", http.StripPrefix("/static/",http.FileServer(http.Dir("assets"))))
```

```
func serveFile(w ResponseWriter, r *Request, fs FileSystem, name string, redirect bool)
```

* 首先我们使用 http.FileServer 创建一个使用给定文件系统的内容响应所有 HTTP 请求的处理程序
* http.Handle("/static/", http.StripPrefix("/static/", fs)) 让文件服务器使用 assets 目录下的文件响应 URL 路径以 /static/ 开头的所有 HTTP 请求。
* assets 被设置为文件服务器的文件系统根目录，文件服务器会处理以 /static 开头的 URL 的请求，所以我们需要使用 http.StripPrefix() 把 static 前缀去掉才能在 assets 目录中搜索到请求的文件。