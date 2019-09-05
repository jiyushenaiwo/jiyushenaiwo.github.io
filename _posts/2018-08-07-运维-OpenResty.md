# OpenResty

openresty是一个基于Nginx和Lua的高性能web平台，内部集成了大量Lua库、第三方模块以及大多数的依赖项。用于方便的搭建能够处理超高并发、拓展性极高的动态web应用、web服务和动态网关。

## 下载

安装openresty首先下载预编译安装包

[下载地址](<http://openresty.org/cn/download.html>)

我使用的是ubuntu系统

首先需要在系统中添加APT仓库，这样会比较方便安装和更新软件包，下面的是步骤：

```js
#导入 GPG密钥
wget -qO - https://openresty.org/package/pubkey.gpg | sudo apt-key add -

#安装	add-apt-repository 命令
# （之后你可以删除这个包以及对应的关联包）
sudo apt-get -y install software-properties-common

#添加official APT 仓库
sudo add-apt-repository -y "deb http://openresty.org/package/ubuntu$(lsb_release -sc) main"

#更新
sudo apt-get update

#安装软件包
sudo apt-get install openresty
```

之前的只是准备工作，只是让我们的安装更加顺利

[下载](<http://openresty.org/cn/download.html>)

进行下载openresty的源码，一定要记得自己下载到了那里，位置一定要记清楚

## 安装

```js
tar -xzvf openresty-VERSION.tar.gz
#VERSION 代表的是你的版本号，别傻傻的复制上去
```

* ./configure

进入openresty-VERSION/目录，输入命令配置

```js
./configure
```

* make

使用下面的命令进行编译

```js
make
```

* make install

```js
make install
```

## hello word

首先创建一个文件夹  要有logs 和 conf文件夹 进行存放配置文件和日志

```js
mkdir ~/work
cd ~/work
mkdir logs/ conf/
```

在conf/目录下创建文件nginx.conf

```js
worker_processes  1;
error_log logs/error.log;
events {
    worker_connections 1024;
}
http {
    server {
        listen 8080;
        location / {
            default_type text/html;
            content_by_lua_block {
                ngx.say("<p>hello, world</p>")
            }
        }
    }
}
```

启动nginx服务器

假设你已经安装了[OpenResty](http://openresty.org/cn/openresty.html)到`/usr/local/openresty`（这是默认值），我们使我们的`nginx`我们的可执行[OpenResty](http://openresty.org/cn/openresty.html)我们可用的安装`PATH`环境：

```
PATH=/usr/local/openresty/nginx/sbin:$PATH
export PATH
```

然后我们以这种方式用我们的配置文件启动nginx服务器：

```
nginx -p `pwd`/ -c conf/nginx.conf
```

错误消息将转到stderr设备或`logs/error.log`当前工作目录中的默认错误日志文件。

访问服务器

```js
curl http://localhost:8080/
```

如果一切正常会输出

```js
<p>hello , world</p>
```

## 组件

### LuaJIT

LuaJIT是lua编程语言的即时编程工具

### Aeeay Var Nginx

这个Nginx模块增加了对nginx配置文件的数量变量的支持

### Auth Request Nginx Module

这个模块是针对Nginx的验证请求模块

### Coolkit Nginx

这个模块是小而有用的Nginx附加组件的集合

默认情况下启用此模块，可以通过将`--without-http_coolkit_module`选项传递给[OpenResty](http://openresty.org/cn/openresty.html)的`./configure`脚本来禁用此模块。

### Drizzle Nginx Module

这是个Nginx上游模块，通过 libdirzzle 与MySQL/或Drizzle数据库服务通信

默认情况下，此ngx_drizzle模块未启用。您应该`--with-http_drizzle_module`在配置OpenResty时指定optiotn。

该libdrizzle C库是不再捆绑OpenResty。您需要从https://launchpad.net/drizzle下载小雨服务器tarball 。

### Echo Nginx Module

该模块包含了Nginx内部API，用于流输入和输出，并行/顺序子请求，定时器和休眠，以及各种元数据访问。

基本上它提供了各种实用程序， 通过简单地模拟不同类型的伪子请求位置来帮助测试和调试其他模块。

### Encrypted Session Nginx  Module

此模块基于 AES-256和Mac的Nginx变量提供加密和解密支持

该模块通常与SetMiscNginxModule和rewrite Module的指令一起使用

此模块可用于实现web应用程序的简单用户登录和访问控制

### Form  Input Nginx Module

这是一个Nginx模块，它读取在“application / x-www-form-urlencoded”中编码的HTTP POST和PUT请求体，并将请求体中的参数解析为Nginx变量。

### Header  more Nginx Module

这个模块允许你添加，设置或清除您指定的任何响应或请求表头

这个是标准头模块的增强版本，因为他提供了更多实用程序，如重置或清除内置类型，内容长度和服务器等“内置表头”

### Iconv Nginx Module

这是一个使用libiconv  转换不同编码字符的Nginx模块。它所带来的set_iconv,并iconv_filter命令Nginx

它可以处理nginx变量或处理响应主体作为输出过滤器。

默认情况下不会启动这个模块，需要	`--with-http_iconv_module`在构建 OprenResty时指定该选项，这个nginx模块将libiconv安装到你的系统中

### Standard Lua  Interpret

默认情况下启用标准Lua解释器，如果启用了LuaJIT，则将自动禁用此解释器

### Memc Nginx Module

该模块扩展了标准memcached模块，几乎支撑了整个memcached ascil协议。

他允许你memcached服务器定义RESIT接口，或者通过子请求或独立虚假请求以非常有效的方式从nginx服务器访问memcached

### Nginx

这个就不需要介绍了吧

### Nginx Devel Kit

NDK是一个Nginx模块，旨在以一种可用作其他Nginx模块基础的方式扩展优秀Nginx Web服务器的核心功能

### Lua  Cjson  Library

Lua  CJSON 是Lua C模块 为lua提供json解析和编码支持。

默认情况下启动此库。你可以指定`--without-lua_cjson`选项OpenResty的`./configure`脚本明确禁止他

### Lua Nginx Module

这个模块Lua解释器或LuaJIT嵌入到nginx核心中，并通过nginx子请求将lua线程，集成到nginx事件模型中。

与Apache的mod_lua和Lighttpd的mod_magnet不同，只要您使用ngx.location.capture或ngx.location.capture_multi接口让nginx核心完成所有请求，在此模块上面编写的Lua代码就可以100％无阻塞网络流量到mysql，postgresql，memcached，上游http web服务等等（有关详细信息，请参阅ngx_drizzle，ngx_postgres，ngx_memc和ngx_proxy模块）。

Lua解释器实例在单个nginx工作进程中的所有请求之间共享。

请求上下文通过Lua（轻量级）线程（也称为Lua协同程序）彼此隔离。加载的Lua模块在nginx工作进程级别上是持久的。因此，即使您的nginx工作进程同时处理10K请求，内存占用也非常小。

### Lua Rds Parser Library

该Lua库可用于将由[Drizzle Nginx Module](http://openresty.org/cn/drizzle-nginx-module.html)和[Postgres Nginx Module](http://openresty.org/cn/postgres-nginx-module.html)生成的Resty-DBD-Stream格式数据解析为Lua数据结构。在过去，我们必须使用JSON作为中间数据格式，这在内存和CPU时间方面都是非常低效的。

为了最大化速度并最小化内存占用，该库以纯C实现。

默认情况下启用此库; 使用该`--without-lua_rds_parser`选项在运行时禁用它`./configure`以构建[OpenResty](http://openresty.org/cn/openresty.html)。

### Lua Redis Parser Library

lua-redis-parser库实现了一个瘦而快的redis原始响应解析器，它构造了相应的lua数据结构，以及构造redis原始请求的函数。

### Lua Resty Core Library

使用LuaJIT FFI 重新实现  Lua Nginx模块提供Lua API

### Lua Resty DNS Library

基于cosoket API 的Lua nginx模块 的非阻塞DNS解析器

默认情况下启动，可以指定`--without-lua_resty_dns` 选项OpenResty 的  `./configure`脚本来明确禁止它。

### Lua Resty Lock Library

这个Lua库实现了一个基于[Lua Nginx Module](http://openresty.org/cn/lua-nginx-module.html)的共享内存字典的简单非阻塞互斥锁API 。对于消除“狗堆效应”非常有用。

默认情况下启用此库。您可以指定`--without-lua_resty_lock`选项[OpenResty](http://openresty.org/cn/openresty.html)的`./configure`脚本来明确禁止它。

### Lua Resty Lrucache Library

为[OpenResty](http://openresty.org/cn/openresty.html)实现Lua-land LRU缓存。

默认情况下启用此库。您可以指定`--without-lua_resty_lrucache`选项[OpenResty](http://openresty.org/cn/openresty.html)的`./configure`脚本来明确禁止它。

### Lua Resty Memcached Library

Lua [Memcached](http://memcached.org/)基于cosocket API的[Lua Nginx模块](http://openresty.org/cn/lua-nginx-module.html)的客户端驱动程序

默认情况下启用此库。您可以指定`--without-lua_resty_memcached`选项[OpenResty](http://openresty.org/cn/openresty.html)的`./configure`脚本来明确禁止它。

### Lua Resty MySQL Library

Lua 基于cosocket API的[Lua Nginx模块](http://openresty.org/cn/lua-nginx-module.html)的[MySQL](http://en.wikipedia.org/wiki/MySQL)客户端驱动程序。

默认情况下启用此库。您可以指定`--without-lua_resty_mysql`选项[OpenResty](http://openresty.org/cn/openresty.html)的`./configure`脚本来明确禁止它。

### Lua Resty Redis Library

Lua [Redis](http://redis.io/)基于cosocket API的[Lua Nginx模块](http://openresty.org/cn/lua-nginx-module.html)客户端驱动程序。

默认情况下启用此库。您可以指定`--without-lua_resty_redis`选项[OpenResty](http://openresty.org/cn/openresty.html)的`./configure`脚本来明确禁止它。

### Lua Resty String Library

一个Lua库，为[Lua Nginx模块](http://openresty.org/cn/lua-nginx-module.html)提供字符串实用程序和公共哈希函数。

默认情况下启用此库。您可以指定`--without-lua_resty_string`选项[OpenResty](http://openresty.org/cn/openresty.html)的`./configure`脚本来明确禁止它。

### Lua Resty Upload Library

基于[Lua Nginx Module](http://openresty.org/cn/lua-nginx-module.html)的cosocket API 进行HTTP文件上传的流式阅读器和解析器。

默认情况下启用此库。您可以指定`--without-lua_resty_upload`选项[OpenResty](http://openresty.org/cn/openresty.html)的`./configure`脚本来明确禁止它。

### Lua Resty Upstream Healthcheck Library

Pure Lua中[Nginx](http://openresty.org/cn/nginx.html)上游服务器的运行状况检查程序。

默认情况下启用此库。您可以指定`--without-lua_resty_upstream_healthcheck`选项[OpenResty](http://openresty.org/cn/openresty.html)的`./configure`脚本来明确禁止它。

### Lua Resty Web Socket Library

这个Lua库实现了一个非阻塞的WebSocket服务器和一个基于[Lua Nginx Module](http://openresty.org/cn/lua-nginx-module.html)的cosocket API 的非阻塞WebSocket客户端。

默认情况下启用此库。您可以指定`--without-lua_resty_websocket`选项[OpenResty](http://openresty.org/cn/openresty.html)的`./configure`脚本来明确禁止它。

### Lua Upstream Nginx Module

这个[Nginx](http://openresty.org/cn/nginx.html) C模块为[Lua Nginx](http://openresty.org/cn/lua-nginx-module.html)模块公开了一个Lua API，用于经典的[Nginx](http://openresty.org/cn/nginx.html)上游。

### Postgres Nginx Module

ngx_postgres是一个上游模块，允许[Nginx](http://openresty.org/cn/nginx.html)直接与PostgreSQL数据库通信。

响应以RDS格式生成，因此它与[Rds Json Nginx模块](http://openresty.org/cn/rds-json-nginx-module.html)和 [Drizzle Nginx模块](http://openresty.org/cn/drizzle-nginx-module.html)模块兼容。

默认情况下不启用此模块，您需要`--with-http_postgres_module`在[构建OpenResty时](http://openresty.org/cn/installation.html)指定该选项。这个[Nginx](http://openresty.org/cn/nginx.html)模块需要将libpq安装到您的系统中。

### Rds Csv Nginx Module

这个[Nginx](http://openresty.org/cn/nginx.html)模块实现了一个高效的输出过滤器，它以流式方式将[Drizzle Nginx模块](http://openresty.org/cn/drizzle-nginx-module.html)和 [Postgres Nginx模块](http://openresty.org/cn/postgres-nginx-module.html)生成的Resty-DBD-Streams（RDS）转换为逗号分隔值（CSV）格式。

默认情况下，CSV格式符合RFC 4180：

```
    http://tools.ietf.org/html/rfc4180
```

默认情况下，此模块在[OpenResty中](http://openresty.org/cn/openresty.html)启用。您可以指定`--without-http_rds_csv_module`在运行时禁用此模块`./configure`以构建[OpenResty的选项](http://openresty.org/cn/openresty.html)。

### Redis2 Nginx Module

这是一个[Nginx](http://openresty.org/cn/nginx.html)上游模块，它使nginx以非阻塞方式与redis 2.x服务器通信。已实施完整的Redis 2.0统一协议，包括redis流水线支持。

此模块从redis服务器返回原始TCP响应。

### Resty CLI

Resty-cli是OpenResty的命令行实用程序的[集合](http://openresty.org/cn/openresty.html)。

该集合中最有用的实用程序是`resty`命令行实用程序，它运行无头侦听的无头nginx。

### Set Misc Nginx Module

This module adds various `set_xxx` directives added to [Nginx](http://openresty.org/cn/nginx.html)'s [rewrite module](http://wiki.nginx.org/NginxHttpRewriteModule) (MD5/SHA1, SQL/JSON quoting, and many more).

Every directive provided by this module can be mixed freely with other nginx rewrite module's directives, like `if`and `set`.

### Srcache Nginx Module

此模块为任意nginx位置提供透明缓存层（如使用上游或甚至提供静态磁盘文件的那些）。

通常，[Memc Nginx模块](http://openresty.org/cn/memc-nginx-module.html)与此模块一起使用，以提供具体的缓存存储后端。但从技术上讲，任何提供REST接口的模块都可以用作此模块使用的提取和存储子请求。

### Xss Nginx模块

该模块为nginx添加了跨站点AJAX支持。目前仅支持跨站点GET。

跨站点GET当前实现为JSONP（或“带填充的JSON”）。有关详细信息，请参见<http://en.wikipedia.org/wiki/JSON#JSONP>。

