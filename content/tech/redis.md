+++
date = '2026-01-04T14:30:35-05:00'
draft = false
title = 'Redis'

+++

# How to deal with redis in java

# 用户模块

### 登录验证方式

#### Cookie+Session VS JWT

| 对比项               | Cookie + Session                                             | JWT (JSON Web Token)                                         |
| -------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **状态存储位置**     | 服务端保存 Session（有状态）                                 | 客户端保存 Token（无状态）                                   |
| **认证流程**         | 登录后服务端创建 Session → 返回 SessionID（Cookie 保存） → 后续请求带 Cookie | 登录后服务端生成签名的 Token → 返回给客户端 → 后续请求带 Token（通常放在 Header） |
| **是否依赖 Cookie**  | 是（默认通过 Cookie）                                        | 否，可用 Header（Authorization: Bearer ...）                 |
| **扩展性（分布式）** | 需要 Session 共享（Redis 等）                                | 无状态，天然适合分布式或微服务                               |
| **安全性**           | Session 可随时失效、可控                                     | JWT 一旦签发除非过期或黑名单，否则无法撤销                   |
| **体积与性能**       | 只传一个 SessionID，小                                       | Token 自包含信息，体积较大，解析耗时略高                     |
| **常见场景**         | 传统 Web 系统（如 Spring MVC、Django）                       | 前后端分离、移动端、微服务、API Gateway                      |

| 场景                                | 主流选择                    | 原因                                  |
| ----------------------------------- | --------------------------- | ------------------------------------- |
| **传统 MVC 网站（如后台管理系统）** | ✅ Cookie + Session          | **简单、安全、支持服务端销毁会话**    |
| **前后端分离 / 移动端 / SPA 应用**  | ✅ JWT                       | 无状态，跨域方便，不依赖浏览器 Cookie |
| **微服务 / API Gateway**            | ✅ JWT / OAuth2 Access Token | 易于分布式验证、支持多服务共享登录态  |
| **高安全业务（银行、政务）**        | ✅ Session                   | **可控性更强，能主动使会话失效**      |







### Mybatis Plus

1. Mybastis plus 默认会在成功插入数据后把数据库生成的主键回填到实体对象中



### 密码加密

#### 加盐(Salting)

定义：在密码哈希之前，给每个密码加上一个字符串，让相同密码的哈希值变得不同，从而防止彩虹表攻击

彩虹表攻击：通过预先计算大量常见密码的哈希值并存储成表格，在数据库泄露时直接“查表”反推明文密码的攻击方式





### 网络

#### HttpServletRequest

代表浏览器前端发来的http请求对象

当客户端向服务器发送一个http请求时，服务器像是Tomcat会把这个请求的所有信息--请求行，请求头，请求体，参数，Cookie等--封装进一个HttpServletRequest对象中，然后传给Controller或Servlet方法

| 方法                        | 说明                              | 示例                                   |
| --------------------------- | --------------------------------- | -------------------------------------- |
| `getParameter(String name)` | 获取请求参数（表单 / Query 参数） | `req.getParameter("username")`         |
| `getHeader(String name)`    | 获取请求头                        | `req.getHeader("User-Agent")`          |
| `getCookies()`              | 获取请求中的 cookies              | `req.getCookies()`                     |
| `getMethod()`               | 获取请求方法                      | `req.getMethod()` → `"GET"` / `"POST"` |
| `getRequestURI()`           | 获取请求路径                      | `/api/user/login`                      |
| `getContextPath()`          | 获取应用上下文路径                | `/myapp`                               |
| `getSession()`              | 获取或创建 Session 对象           | `req.getSession()`                     |
| `getInputStream()`          | 获取请求体（比如 JSON 数据流）    | `req.getInputStream()`                 |
| `getRemoteAddr()`           | 获取客户端 IP 地址                | `req.getRemoteAddr()`                  |

