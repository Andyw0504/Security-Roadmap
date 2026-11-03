# 02 · Linux 安全基础

> 渗透与应急的日常环境。命令不熟，动作就快不起来。

## 日常命令

```bash
# 文件与权限
ls -la / find / -name "*.conf" 2>/dev/null
chmod / chown / SUID(rws) SGID(rws) 粘滞位(st)

# 进程与网络
ps auxf                      # 进程树更直观
ss -antlp                    # 监听端口与关联进程
lsof -i :8080                # 谁占了端口

# 服务
systemctl list-units --type=service --state=running
```

## 权限模型速记

- `r=4 w=2 x=1`，三位分别属主/组/其他
- **SUID**：执行时以文件属主身份跑（`/usr/bin/passwd` 典型）→ 提权常见线索
- `find / -perm -4000 -type f 2>/dev/null` 找 SUID 文件，对照 GTFOBins

## 用户与登录痕迹

```bash
cat /etc/passwd | grep -E ":0:"      # 除 root 外 UID=0 的可疑账号
last / lastlog / w                   # 登录记录
/var/log/secure (或 auth.log)        # SSH 爆破/成功登录记录
```

## 提权检查清单

- [ ] `sudo -l`（看可免密执行什么）
- [ ] SUID 文件对照 GTFOBins
- [ ] `cat /etc/crontab` + `ls /etc/cron*`（root 的定时任务，是否有可写脚本）
- [ ] 内核版本 → searchsploit 看有无本地提权（如 dirty cow）
- [ ] 可写的 PATH 目录、`$PATH` 劫持
- [ ] Docker 组 / LXD 组成员身份

## 应急排查顺序

1. `w` / `last` — 谁登录过
2. `ps auxf` / `ss -antlp` — 异常进程与外连
3. 定时任务、`~/.ssh/authorized_keys`、`/etc/rc.local` — 持久化点
4. `find / -mtime -1 -type f 2>/dev/null` — 最近改动
5. Web 日志（如果带 Web 业务）搜 webshell 特征

## 包管理与环境

```bash
apt install python3-pip / pip3 install --user
python3 -m venv env && source env/bin/activate   # 工具环境隔离
```
