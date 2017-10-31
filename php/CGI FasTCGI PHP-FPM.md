## 基础
* CGI：是 Web Server 与 Web Application 之间数据交换的一种协议。
* FastCGI：同 CGI，是一种通信协议，但比 CGI 在效率上做了一些优化。同样，SCGI 协议与 FastCGI 类似。
* PHP-CGI：是 PHP （Web Application）对 Web Server 提供的 CGI 协议的接口程序。
* PHP-FPM：是 PHP（Web Application）对 Web Server 提供的 FastCGI 协议的接口程序，额外还提供了相对智能一些任务管理。

## WEB 中
* Web Server 一般指Apache、Nginx、IIS、Lighttpd、Tomcat等服务器，
* Web Application 一般指PHP、Java、Asp.net等应用程序。

## 详解

* ### CGI
	CGI全称是“公共网关接口”(Common Gateway Interface)，HTTP服务器与你的或其它机器上的程序进行“交谈”的一种工具，其程序须运行在网络服务器上。

	CGI可以用任何一种语言编写，只要这种语言具有标准输入、输出和环境变量。如php,perl,tcl等

* ### FastCGI
	FastCGI像是一个常驻(long-live)型的CGI，它可以一直执行着，只要激活后，不会每次都要花费时间去fork一次（这是CGI最为人诟病的fork-and-execute 模式）。它还支持分布式的运算，即 FastCGI 程序可以在网站服务器以外的主机上执行并且接受来自其它网站服务器来的请求

	FastCGI是语言无关的、可伸缩架构的CGI开放扩展，其主要行为是将CGI解释器进程保持在内存中并因此获得较高的性能。众所周知，CGI解释器的反复加载是CGI性能低下的主要原因，如果CGI解释器保持在内存中并接受FastCGI进程管理器调度，则可以提供良好的性能、伸缩性、Fail- Over特性等等。

* ### PHP-CGI

	PHP-CGI是PHP自带的FastCGI管理器。

	PHP-CGI的不足：

	1. php-cgi变更php.ini配置后需重启php-cgi才能让新的php-ini生效，不可以平滑重启。
	2. 直接杀死php-cgi进程，php就不能运行了。(PHP-FPM和Spawn-FCGI就没有这个问题，守护进程会平滑从新生成新的子进程。）


* ### PHP-FPM
	PHP-FPM提供了更好的PHP进程管理方式，可以有效控制内存和进程、可以平滑重载PHP配置，比spawn-fcgi具有更多有点，所以被PHP官方收录了。在./configure的时候带 –enable-fpm参数即可开启PHP-FPM

## 优缺点
* CGI:每一个Web请求PHP都必须重新解析php.ini、重新载入全部扩展，并重初始化全部数据结构

* FastCGI是多进程,更消耗服务器资源 php-cgi 解释器每个进程大概消耗 7-25 M内存

* PHP-CGI是PHP自带的FastCGI管理器 但是在变更php.ini后必须重启php-cgi才能让其生效，直接杀死PHP-CGI后PHP就不能运行了

* PHP-FPM 是对于 FastCGI 协议的具体实现，他负责管理一个进程池，处理来自Web服务器的请求。目前，PHP5.3版本之后，PHP-FPM是内置于PHP的。

## 能解决的问题

使用PHP-FPM + FastCGI FastCGI 可以解决CGI重复fork的问题，支持分布式运算 PHP-FPM 可以管理PHP-CGI进程 实现平滑重启
