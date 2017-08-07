PWMIS.OAuth2.0 授权认证服务程序说明
=====================================

本程序分为2部分：
* 授权认证服务和工具类
* Demo和测试程序
	* 控制台测试程序
	* WinFom测试程序

# 1,授权模式
本系统采用OAuth 2.0 开放式授权协议，采用授权与认证相分离的模式，采用OAuth 2.0协议中的密码授权模式。

# 2,系统角色
在 OAuth 2.0 授权体系中，有下面几种角色：
* 【授权服务器】：对客户端对资源服务器的访问进行授权；
* 【资源服务器】：提供API等资源服务的服务器，是资源的提供者，供客户端访问；
* 【客户端】：访问资源服务器的对象，它可以是一个客户端程序，也可以是另外一个Web站点，甚至是另外一个资源服务器，准确的说，它是“资源”的消费者。
* 【认证服务器】：验证客户端的身份，根据使用OAuth 2.0协议模式的不同验证方式也不同，在本例中，采用验证用户名和密码的模式。
* 【用户】：使用客户端的终端用户，用户需要首先授权给自己可信任的客户端程序或者Web站点，然后系统后续流程才能运行。

# 3,授权流程
本系统虽然提供了4种OAuth 2.0 的授权模式，但本例重点仅演示说明密码模式授权流程。

## 3.1,密码模式授权流程
首先看授权认证服务流程图：
 

1，	用户在客户端输入自己的登录账号（用户名和密码），然后客户端将用户的登录账号信息POST到授权服务器；
2，	授权服务器携带用户的登录账号，去认证服务器验证用户的身份；
3，	验证通过，授权服务器为客户端生成一个访问令牌；
4，	客户端携带此访问令牌，访问资源服务器；
5，	资源服务器去授权服务器验证客户端的访问令牌是否有效；
6，	如果访问令牌有效，授权服务器给资源服务器发送用户标识信息；
7，	资源服务器根据用户标识信息，处理业务请求，最后发送响应结果给客户端。

# 4，解决方案设计
## 4.1，程序集说明
* 1	授权服务器	PWMIS.OAuth2.AuthorizationCenter	授权中心
* 2	资源服务器	Demo.OAuth2.WebApi	提供API资源
* 3	客户端	Demo.OAuth2.ConsoleTest	控制台测试程序
* 4		Demo.OAuth2.Port	用户的Web入口
                Demo.OAuth2.WinFormTest WinForm测试程序
* 5	认证服务器	Demo.OAuth2.IdentityServer	简单登录账号认证
* 6		PWMIS.OAuth2.Tools	提供OAuth2.0 协议访问的一些有用的工具类

## 4.2,授权服务器设计
* 客户端标识--使用客户端ID和客户端秘钥组成
* 用户账号--用户登录名称和密码
* 登录结果--登录的用户名和登录结果消息
* 身份认证模式
	* 集成认证--授权服务器跟认证服务器在一起
	* 认证服务器--使用WebAPI连接的外部认证服务
* OWIN身份认证方式
* 访问令牌
	* 令牌响应信息结构
	* 令牌有效期--默认10秒后过期
	* 申请令牌
	* 刷新令牌
* 数据库--LocalDB

## 4.3,资源服务器设计
* WebAPi 资源服务器
* 其它资源服务器

详细内容，请查看 [授权认证服务设计说明]

[我的博客](http://www.cnblogs.com/bluedoctor ) 