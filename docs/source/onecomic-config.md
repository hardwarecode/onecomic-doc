# 配置文件

根据示例创建配置文件

### 配置文件示例
```
[mail]

# SMTP主机 发送账户是163邮箱则设置为 smtp.163.com
smtp_server=smtp.qq.com

# SMTP服务端口（SSL）
smtp_port=465

# 发送者账户
sender=xx.qq.com

# 登录失败可能需要使用授权码登录 https://service.mail.qq.com/cgi-bin/help?subtype=1&&id=28&&no=1001256
# 发送者账户密码或者授权码
sender_passwd=密码或授权码

# 邮件接收者列表，多个则以半角逗号隔开。如 xxx@qq.com,yyy@qq.com
receivers=11111@qq.com,22222@qq.com


[crawler]
# 默认的下载目录
# download_dir=/home/xxx/MyComicBook

# 配置指定站点代理地址
# proxy_18comic=socks5://127.0.0.1:1080
# proxy_manhuagui=socks5://127.0.0.1:1080
# proxy_nhentai=socks5://127.0.0.1:1080
# proxy_wnacg=socks5://127.0.0.1:1080
# proxy_acg456=socks5://127.0.0.1:1080
# proxy_mh1234=socks5://127.0.0.1:1080
# proxy_177pic=socks5://127.0.0.1:1080
# proxy_18hmmcg=socks5://127.0.0.1:1080
# proxy_xiuren=socks5://127.0.0.1:1080
# proxy_twhentai=socks5://127.0.0.1:1080
# proxy_copymanga=socks5://127.0.0.1:1080
# proxy_toomics=socks5://127.0.0.1:1080
# proxy_webtoons=socks5://127.0.0.1:1080


# 若站点域名变更，页面样式不变，可通过参数修改域名
# site_index_gufengmh=https://www.gufengmh9.com/
# site_index_mh160=https://mh160.cc/


# webdriver 配置
# driver_type=Chrome
# driver_path=/home/xxx/chromedriver_win32/chromedriver.exe


# node模块位置
# node_modules=/home/xxx/js/node_modules

# cookies存放目录（自动读取该目录下的cookeis文件），文件名命名规范: 如 toomics.json qq.json {site}.json
# cookies_dir=/home/xxx/cookies

# 长图质量 最大100
# quality=95
# 长图最大高度 最大65500
# max_height=20000

# 图片下载超时时间 单位秒
image_timeout=30

# 站点访问超时时间 单位秒
crawler_timeout=30

# 每个章节下载时间间隔 单位秒
crawler_delay=0

# User-Agent 配置
# user_agent=Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/93.0.4577.82 Safari/537.36

# 将下载的webp格式的图片自动转换成jpg
transfer_webp=1


# 日志输出文件路径
log_file=/home/xxx/MyComicBook/xxx.log
```

将上述配置保存为`config.ini`

如`onecomic -s u17 -id 195 -c 1`会默认读取当前目录下的`config.ini`配置文件

或者通过环境变量配置默认的配置文件
```sh
# 将以下命令添加到 ~/.bashrc 或 ~/.zshrc 文件末尾
export ONECOMIC_CONFIG_FILE="/home/xxx/MyConfig/config.ini"
```

也可以通过参数指定配置文件`onecomic -s u17 -id 195 -c 1 --config config.ini`
