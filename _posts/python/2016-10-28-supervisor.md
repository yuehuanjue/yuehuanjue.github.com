---
layout: article
title: Supervisor插件
description:  Supervisor是一个多进程管理工具，由python实现的，在github上可以找到它的源码。
updateData:  14:14-- 2016/10/28
categories: django插件/运维
share: false
image:
  feature: 
  teaser: 
  credit: yuehuanjue
---
### 

####一、安装指令

```
pip install supervisor


```

####二、配置环境

```
echo_supervisord_conf > supervisor.conf  # 生成 supervisor 默认配置文件

vim  supervisor.conf                   # 修改 supervisor 配置文件，添加 gunicorn 进程管理

在 supervisor.conf 底部下添加 myweb.py 的配置 `/home/***/supervisor/super` 项目目录」

添加如下：
[program:***]   # ***代表进程的名字，用ps aux可查询
command=/home/**/supervisor/super/bin/gunicorn -w 4 -b 0.0.0.0:8000 myweb:app                                                                     
directory=/home/wang/supervisor                                             
startsecs=0                                                                   
stopwaitsecs=0                                                                  
autostart=false                                                                
autorestart=false                                                                 
user= 。。                                                                     
stdout_logfile=/home/wang/supervisor/log/gunicorn.log                  
stderr_logfile=/home/wang/supervisor/log/gunicorn.err

注：注释是;
```

####三、常见的命令

```
supervisord -c supervisor.conf                           查看supervisor的运行状态

supervisorctl -c supervisor.conf status                  查看supervisor的状态                        
              
supervisorctl -c supervisor.conf reload                  重新载入 配置文件

supervisorctl -c supervisor.conf start [all]|[appname]   启动指定/所有 supervisor 管理的程序进程

supervisorctl -c supervisor.conf stop [all]|[appname]    关闭指定/所有 supervisor 管理的程序进程

```

####四、web管理界面的配置

```
[inet_http_server]     ; inet (TCP) server disabled by default

port=127.0.0.1:9001    ; (ip_address:port specifier, *:port for alliface)

username=。。          ; (default is no username (open server)

password=123           ; (default is no password (open server))

[supervisorctl]
serverurl=unix:///tmp/supervisor.sock ; use a unix:// URL  for a unix socket

serverurl=http://127.0.0.1:9001       ; use an http:// url to specify an inet socket

username=。。                         ; should be same as http_username if set

password=123                          ; should be same as http_password if set

;prompt=mysupervisor                  ; cmd line prompt (default "supervisor")

;history_file=~/.sc_history           ; use readline history if available

```

####五、运行supervisor

```
supervisord -c supervisor.conf

```
