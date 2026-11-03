# 🗺️ Security Roadmap

> Web 安全 / 渗透测试学习路线图，记录我的学习路径与知识体系，持续更新中。

**为什么写这个仓库**：碎片化学完就忘，把知识整理成体系才能在实战中快速调用。这是我给自己整理的地图，也希望对你有帮助。

## 🧭 路线总览

```
基础 → Web 安全 → 渗透测试 → 内网渗透 → 进阶方向
```

---

## 第一阶段：基础

### 📡 网络基础
- [ ] TCP/IP 协议栈、三次握手 / 四次挥手
- [ ] HTTP/HTTPS 协议细节（方法、状态码、Header、Cookie/Session）
- [ ] DNS、CDN、负载均衡原理
- 📚 推荐：《图解 TCP/IP》

### 🖥️ 操作系统
- [ ] Linux 常用命令、文件权限、进程管理
- [ ] Linux 提权思路（SUID、内核漏洞、定时任务）
- [ ] Windows 域环境基础（AD、Kerberos、NTLM）
- 📚 推荐：《鸟哥的 Linux 私房菜》

### 💻 编程能力
- [x] Python：写 PoC / Exploit 脚本
- [ ] PHP：看懂常见 CMS 源码（审计需要）
- [ ] SQL：增删改查 + 注入语句构造
- [ ] JavaScript：XSS 利用与前端逻辑分析
- [ ] Go：阅读/编写安全工具（进行中）

### 🗄️ 数据库
- [ ] MySQL / MSSQL / PostgreSQL 基本操作
- [ ] Redis / MongoDB 未授权访问问题
- [ ] 各数据库的注入特性差异

---

## 第二阶段：Web 安全

### 核心漏洞（OWASP Top 10）
- [ ] SQL 注入（联合、报错、布尔、时间盲注、堆叠）
- [ ] XSS（反射 / 存储 / DOM、CSP 绕过）
- [ ] CSRF / SSRF（利用协议、绕过姿势）
- [ ] 文件上传 / 文件包含（LFI/RFI、伪协议）
- [ ] 命令注入 / 代码执行（反序列化）
- [ ] 逻辑漏洞（越权、支付、验证码、密码重置）

### 实战平台
| 平台 | 用途 | 状态 |
|---|---|---|
| DVWA | 漏洞入门 | ✅ 完成 |
| SQLi-Labs | 注入专精 | 🔄 刷题中 |
| Upload-Labs | 文件上传 | 🔄 刷题中 |
| PortSwigger Web Security Academy | 体系化 Web | 🔄 进行中 |
| Hack The Box | 综合实战 | 🔄 进行中 |

### 🛠️ 必会工具
Burp Suite（重点：Intruder、Repeater、插件开发）· sqlmap · Nmap · ffuf/dirsearch · AntSword

---

## 第三阶段：渗透测试

- [ ] 渗透流程：授权 → 信息收集 → 漏洞验证 → 后渗透 → 报告
- [ ] 信息收集：子域名枚举、指纹识别、目录爆破、OSINT
- [ ] 后渗透：权限维持、提权（Linux/Windows）、隧道搭建
- [ ] 内网横向：密码喷洒、Hash 传递、域攻击（Kerberoasting 等）
- 📚 推荐：《内网安全攻防》、HTB Pro Labs
- 🧰 工具：Metasploit · Cobalt Strike · frp/nps · Impacket

---

## 第四阶段：进阶方向（探索中）

- 🔴 红队：免杀、C2 开发、钓鱼、供应链
- 🔵 蓝队：应急响应、溯源分析、蜜罐、SIEM
- 🟣 代码审计：Java/PHP 代码审计、框架漏洞分析（Shiro/Fastjson/Log4j2）
- ☁️ 云安全：容器逃逸、云上攻防

---

## 📅 更新记录

- **2026-11**：创建仓库，规划整体路线
- *持续更新中……*

---

> ⚠️ 所有技术仅限合法授权测试使用。学习路上，共勉。
