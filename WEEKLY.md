# 学习周报

> 每周日花 15 分钟记录：本周做了什么、学到什么、下周做什么。坚持复盘 > 苦学。

## 模板（复制使用）

```markdown
## 2026-W__（MM-DD ~ MM-DD）

### 本周完成
- [ ]

### 学到的知识点（3~5 条）
1. 

### 遇到的坑
- 

### 下周计划
- [ ]
```

---

## 2026-W45（11-02 ~ 11-08）

### 本周完成
- [x] 搭建学习体系：创建 Security-Roadmap / CTF-Writeups / sec-tools
- [x] SQLi-Labs 起步，整理 SQL 注入手册初稿

### 学到的知识点
1. `information_schema` 是 MySQL 注入查表查列的关键
2. 报错注入一次最多回显 32 字符，要分段
3. `secure_file_priv` 限制 INTO OUTFILE 的可用性

### 遇到的坑
- Burp 抓 HTTPS 忘了装 CA 证书，浪费半小时

### 下周计划
- [ ] SQLi-Labs 刷完 Less1~20
- [ ] 整理时间盲注脚本模板
