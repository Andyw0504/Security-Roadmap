# 01 · 网络基础：HTTP 协议要点

> Web 安全的地基。抓包分析前先把协议细节过一遍。

## 请求与响应

```
GET /login?user=a HTTP/1.1
Host: target.com
User-Agent: Mozilla/5.0
Cookie: PHPSESSID=abc123
Content-Type: application/x-www-form-urlencoded    (POST 时)
Content-Length: 20                                  (POST 时)

user=admin&pass=123456
```

## 必须掌握的点

| 点 | 安全相关 |
|---|---|
| 方法 GET/POST/PUT/DELETE/OPTIONS | OPTIONS 可探测允许的方法；不安全方法可能是攻击面 |
| 状态码 200/301/302/401/403/404/500 | 403 目录可能存在；500 报错信息常泄漏栈/路径 |
| Cookie vs Session | 会话固定、Cookie 属性（HttpOnly/Secure/SameSite） |
| 同源策略 | 协议+域名+端口 三者一致才是同源，CORS/XSS 的基础 |
| 编码 URL/HTML/Unicode | WAF 绕过的常客（双重编码、大小写、注释） |

## 常见 Header 速查

- `Referer`：来源校验（CSRF 防御之一，但可伪造）
- `X-Forwarded-For`：真实 IP 获取 —— **可伪造**，服务端信任它就有 SSRF/绕过风险
- `Content-Type`：`application/json` vs `multipart/form-data`，接口测试要选对
- `Range`：分块下载，某些目录遍历漏洞靠它触发

## 抓包分析流程（Burp）

1. Proxy 挂代理，浏览器访问目标，观察请求序列
2. Repeater 里改参数重放，对比响应
3. Intruder 爆破时注意速率与字典选择
4. HTTPS 抓包原理：Burp 生成 CA 证书装到系统里做中间人

## HTTP/HTTPS 细节

- HTTPS = TLS 握手（证书验证）→ 对称加密通信
- 抓不到包的常见原因：HSTS、证书不信任、代理配置错
- 降级攻击/协议版本：老站点可能还在用 TLS1.0/1.1

## 练习建议

- 用 `curl -v` 把每个请求的完整报文看一遍再进 Burp
- 读完一条请求能说出每一行的作用，就算过关
