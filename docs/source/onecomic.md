# 一本漫画

**尊重版权，请支持正版**

**该项目仅供技术研究使用，请勿用于非法用途，否则后果自负**

**通过本工具下载或生成的资源禁止传播分享！禁止利用该项目从事营利性活动！**

项目地址： [https://github.com/hardwarecode/onecomic](https://github.com/hardwarecode/onecomic)

## 安装/升级步骤

自己找安装Python的教程（Python版本大于等于3.6）

安装nodejs环境，自己找教程安装

```sh
# 检查python版本
python --version
# 检查pip版本
pip --version
```

```sh
# 在线安装/升级（最新版本）
pip install -U onecomic

# 查看帮助
onecomic --help
```

## 常规使用

**Windows下，以下所有示例命令需要添加`python -m`前缀**

如: `python -m onecomic --url "http://ac.qq.com/Comic/ComicInfo/id/505430"`

```sh
# 注意参数里的 - 和 -- 的区别
# 从章节列表页面的URL 下载漫画的最新一集
onecomic --url "http://ac.qq.com/Comic/ComicInfo/id/505430"

# 下载漫画 id=505430 最新一集 注意不同站点的漫画id区别
onecomic -s qq -id=505430

# 下载所有章节
onecomic -s qq -id 505430 --all

# 下载第800集
onecomic -s qq -id 505430 -c 800

# 下载倒数第二集
onecomic -s qq -id 505430 -c -2

# 下载1到5集,7集，9到10集
onecomic -s qq -id 505430 -c 1-5,7,9-10

# 拼接成长图
onecomic -s qq -id 505430 --single-image --quality 95 --max-height 20000

# 压缩成zip文件
onecomic -s qq -id=505430 --zip

# 设置代理
onecomic -s qq -id 505430 --proxy "socks5://127.0.0.1:1080"

# 自定义保存目录
onecomic -s qq -id=505430 --output MyComicBook

# 将多话合并到单个文件夹和zip文件
onecomic -s manhuagui -id 1128 -c 320-322 --merge --merge-zip

# 下载单行本
onecomic -s manhuagui -id 1128 --ext-name 单行本 -c -1

# 跟据名字搜索comicid
onecomic -s qq --name 海贼

# 生成pdf文件
# 注意: 生成pdf文件需要额外安装依赖，需要先执行 pip install img2pdf 或 pip install reportlab
onecomic -s qq -id 505430 --pdf

# 推送到邮箱
# 注意: 发送到邮箱需预先配置好信息（详情请看配置文件部分）
onecomic -s qq -id 505430 --pdf --mail --config config.ini
```

从其它站点下载，注意不同站点的comicid区别
```sh
# 从哔哩哔哩漫画下载
onecomic -s bilibili -id mc24742 -c 1

# 从有妖气漫画下载
onecomic -s u17 -id 195 -c 1

# 从章节列表页面的URL下载
onecomic --url "https://manga.bilibili.com/detail/mc28603" -c 1
```

## 关于登录

登录后可下载已购买的付费资源

1. [安装EditThisCookie插件](https://chrome.google.com/webstore/detail/editthiscookie/fngmhnnpilhplaeedifhccceomclgfbg)
2. 在浏览器上登录某个站点，然后通过插件导出某个站点的cookies，并保存到本地文件 如`qq.json`
```sh
onecomic -s qq -id=505430 -c -1 --cookies-path="qq.json"
```


## 高级批量下载

```sh
# 通过指定的URL文件列表批量下载
onecomic --url-file test/test-url-file.txt
```

文件示例`test/test-url-file.txt`
```
# 海贼王
http://ac.qq.com/Comic/ComicInfo/id/505430
# 雏蜂
https://www.u17.com/comic/195.html
```
------

```sh
# 有些站点不一定支持，其它的通用参数也适用，可自行组合
# 下载最近更新页面的1到10页 所有漫画的最新一集
onecomic -s nvshens --latest --page 1-10

# 展示支持的标签
onecomic -s nvshens --show-tags

# 下载标签搜索结果页面的1到10页 所有漫画的全集
onecomic -s nvshens --tag 女神 --page 1-10 --all

# 下载搜索结果的所有漫画的全集
onecomic -s nhentai --search 汉化 --page 1 --all
```


## 其它说明

#### cookies使用说明

- 下载付费内容需要cookies，Toomics、qootoon站点下载R18内容也需要cookies
- 最好保证脚本与在浏览器导出的cookies在同一个网络环境（如果浏览器使用代理，脚本也要使用同样的代理环境）
- 若使用了cookies还是下载不了，需检查账号在站点浏览是否正常，若正常浏览则重新导出一份新的cookies文件再做尝试
- 若还是下载不了，请加群反馈。付费内容的下载问题还请提供cookies或账号（私聊群主），不提供大概率会被无视


#### 关于cocomanhua的下载

1. 安装nodejs环境
2. 安装crypto-js依赖，命令：`npm install crypto-js`，默认在当前目录下生成`node_modules`目录
3. 下载 `onecomic -s cocomanhua -id 12187` 或者 `onecomic -s cocomanhua --node-modules ./node_modules`
