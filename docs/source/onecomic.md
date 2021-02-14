# 一本漫画

**尊重版权，请支持正版**

**该项目仅供技术研究使用，请勿用于非法用途，否则后果自负**

**通过本工具下载或生成的资源禁止传播分享！禁止利用该项目从事营利性活动！**

项目地址： [https://github.com/hardwarecode/onecomic](https://github.com/hardwarecode/onecomic)

## 安装/升级步骤

自己找安装Python的教程（Python版本大于等于3.6）

Windows需要先安装git [https://gitforwindows.org/](https://gitforwindows.org/)

```sh
# 检查python版本
python --version
```

```sh
# 在线安装/升级（最新版本）
python -m pip install -U onecomic

# 查看帮助
python -m onecomic --help

# 安装指定版本
python -m pip install onecomic==0.1.1
```

## 常规使用

```sh
# 注意参数里的 - 和 -- 的区别
# 从章节列表页面的URL 下载漫画的最新一集
python -m onecomic --url "http://ac.qq.com/Comic/ComicInfo/id/505430"

# 下载漫画 id=505430 最新一集 注意不同站点的漫画id区别
python -m onecomic -s qq -id=505430

# 下载所有章节
python -m onecomic -s qq -id 505430 --all

# 下载第800集
python -m onecomic -s qq -id 505430 -c 800

# 下载倒数第二集
python -m onecomic -s qq -id 505430 -c -2

# 下载1到5集,7集，9到10集
python -m onecomic -s qq -id 505430 -c 1-5,7,9-10

# 拼接成长图
python -m onecomic -s qq -id 505430 --single-image --quality 95 --max-height 20000

# 压缩成zip文件
python -m onecomic -s qq -id=505430 --zip

# 设置代理
python -m onecomic -s qq -id 505430 --proxy "socks5://127.0.0.1:1080"

# 自定义保存目录
python -m onecomic -s qq -id=505430 --output MyComicBook

# 将多话合并到单个文件夹和zip文件
python -m onecomic -s manhuagui -id 1128 -c 320-322 --merge --merge-zip

# 下载单行本
python -m onecomic -s manhuagui -id 1128 --ext-name 单行本 -c -1

# 跟据名字搜索comicid
python -m onecomic -s qq --name 海贼

# 生成pdf文件
# 注意: 生成pdf文件需要额外安装依赖，需要先执行 python -m pip install img2pdf 或 python -m pip install reportlab
python -m onecomic -s qq -id 505430 --pdf

# 推送到邮箱
# 注意: 发送到邮箱需预先配置好信息 配样例参照 https://onecomic-doc.readthedocs.io/en/latest/onecomic-config.html
# 并根据实际情况调整，将配置文件保存为 config.ini
python -m onecomic -s qq -id 505430 --pdf --mail --config config.ini
```

从其它站点下载，注意不同站点的comicid区别
```sh
# 从哔哩哔哩漫画下载
python -m onecomic -s bilibili -id mc24742 -c 1

# 从有妖气漫画下载
python -m onecomic -s u17 -id 195 -c 1

# 从章节列表页面的URL下载
python -m onecomic --url "https://manga.bilibili.com/detail/mc28603" -c 1
```

## 关于登录

1. [安装EditThisCookie插件](https://chrome.google.com/webstore/detail/editthiscookie/fngmhnnpilhplaeedifhccceomclgfbg)
2. 在浏览器上登录某个站点，然后通过插件导出某个站点的cookies，并保存到本地文件 如`qq.json`
```sh
python -m onecomic -s qq -id=505430 -c -1 --cookies-path="qq.json"
```


## 高级批量下载

```sh
# 通过指定的URL文件列表批量下载
python -m onecomic --url-file test/test-url-file.txt
```

文件示例`test-url-file.txt`
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
python -m onecomic -s nvshens --latest-all --latest-page 1-10

# 展示支持的标签
python -m onecomic -s nvshens --show-tags

# 下载标签搜索结果页面的1到10页 所有漫画的全集
python -m onecomic -s nvshens --tag-all --tag 女神 --tag-page 1-10 --all

# 下载搜索结果的所有漫画的全集
python -m onecomic -s nhentai --search-all --search-name 汉化 --search-page 1 --all
```
