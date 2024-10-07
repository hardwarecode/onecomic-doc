# 一本漫画

**尊重版权，请支持正版**

**该项目仅供技术研究使用，请勿用于非法用途，否则后果自负**

**通过本工具下载或生成的资源禁止传播分享！禁止利用该项目从事营利性活动！**

项目地址： [https://github.com/hardwarecode/onecomic](https://github.com/hardwarecode/onecomic)

## 安装/升级步骤

自己找安装Python的教程（Python版本大于等于3.6，小于3.10）

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

[更新日志](https://github.com/hardwarecode/onecomic/blob/main/CHANGELOG.md)

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

# 下载倒数第2集
onecomic -s qq -id 505430 -c r2

# 下载倒数第1集至倒数第5集
onecomic -s qq -id 505430 -c r1-5


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

# 下载单行本 番外篇 xxx
onecomic -s manhuagui -id 1128 --ext-name 单行本 -c -1
onecomic -s xxx -id xxx --ext-name 番外篇 -c -1
onecomic -s xxx -id xxx --ext-name xxx -c -1


# 跟据名字搜索漫画comicid 打印搜索结果
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


# 跟据名字搜索漫画comicid 打印搜索结果
onecomic -s nhentai --name 汉化

# 下载搜索结果的所有漫画的全集
onecomic -s nhentai --search 汉化 --page 1 --all
```


## 常见问题

### 怎么下载有登陆限制/需要付费漫画

下载付费漫画的前提是，你的账号要**先购买**漫画

1. [安装EditThisCookie插件](https://chrome.google.com/webstore/detail/editthiscookie/fngmhnnpilhplaeedifhccceomclgfbg)
2. 在浏览器上登录某个站点，然后通过插件导出某个站点的cookie，并保存到本地文件 如`qq.json`
3. 最好保证运行的脚本与在浏览器导出的cookie在同一个网络环境（如果浏览器使用代理，脚本也要使用同样的代理环境）

```sh
onecomic -s qq -id=505430 -c -1 --cookies-path="qq.json"
```

若使用了cookie还是下载不了，需检查账号在站点浏览是否正常，若正常浏览则重新导出一份新的cookies文件再做尝试

若还是下载不了，请加群反馈，随缘修复

### Toomics、qootoon站点下载R18内容需要配置cookie

### 站点域名修改了，样式没有变化

可以通过`--site-index`参数指定新域名，或参考配置文件修改

```sh
onecomic -s gufengmh --site-index="https://www.gufengmh9.com/"
```

### 运行报错

运行的时候报错

```
Traceback (most recent call last):
  File "/usr/lib/python3.10/runpy.py", line 196, in _run_module_as_main
    return _run_code(code, main_globals, None,
  File "/usr/lib/python3.10/runpy.py", line 86, in _run_code
    exec(code, run_globals)
  File "/home/xxxx/.local/lib/python3.10/site-packages/onecomic/__main__.py", line 3, in <module>
    from .cli import main
  File "/home/xxxx/.local/lib/python3.10/site-packages/onecomic/cli.py", line 6, in <module>
    from .comicbook import ComicBook
  File "/home/xxxx/.local/
  lib/python3.10/site-packages/onecomic/comicbook.py", line 19, in <module>
    from .crawlerbase import CrawlerBase
  File "/home/xxxx/.local/lib/python3.10/site-packages/onecomic/crawlerbase.py", line 12, in <module>
    from .session import CrawlerSession
  File "/home/xxxx/.local/lib/python3.10/site-packages/onecomic/session.py", line 4, in <module>
    import httpx
  File "/home/xxxx/.local/lib/python3.10/site-packages/httpx/__init__.py", line 2, in <module>
    from ._api import delete, get, head, options, patch, post, put, request, stream
  File "/home/xxxx/.local/lib/python3.10/site-packages/httpx/_api.py", line 4, in <module>
    from ._client import Client
  File "/home/xxxx/.local/lib/python3.10/site-packages/httpx/_client.py", line 29, in <module>
    from ._transports.default import AsyncHTTPTransport, HTTPTransport
  File "/home/xxxx/.local/lib/python3.10/site-packages/httpx/_transports/default.py", line 30, in <module>
    import httpcore
  File "/home/xxxx/.local/lib/python3.10/site-packages/httpcore/__init__.py", line 1, in <module>
    from ._api import request, stream
  File "/home/xxxx/.local/lib/python3.10/site-packages/httpcore/_api.py", line 5, in <module>
    from ._sync.connection_pool import ConnectionPool
  File "/home/xxxx/.local/lib/python3.10/site-packages/httpcore/_sync/__init__.py", line 8, in <module>
    from .http2 import HTTP2Connection
  File "/home/xxxx/.local/lib/python3.10/site-packages/httpcore/_sync/http2.py", line 7, in <module>
    import h2.connection
  File "/home/xxxx/.local/lib/python3.10/site-packages/h2/connection.py", line 13, in <module>
    from hyperframe.frame import (
  File "/home/xxxx/.local/lib/python3.10/site-packages/hyperframe/frame.py", line 17, in <module>
    from .flags import Flag, Flags
  File "/home/xxxx/.local/lib/python3.10/site-packages/hyperframe/flags.py", line 14, in <module>
    class Flags(collections.MutableSet):
AttributeError: module 'collections' has no attribute 'MutableSet'
```
或者
```
Traceback (most recent call last):
  File "/home/xxxx/anaconda3/lib/python3.11/site-packages/onecomic/crawlerbase.py", line 257, in send_request
    response = session.request(method=method, url=url, **kwargs)
  File "/home/xxxx/anaconda3/lib/python3.11/site-packages/httpx/_client.py", line 827, in request
    return self.send(request, auth=auth, follow_redirects=follow_redirects)
  File "/home/xxxx/anaconda3/lib/python3.11/site-packages/httpx/_client.py", line 914, in send
    response = self._send_handling_auth(
  File "/home/xxxx/anaconda3/lib/python3.11/site-packages/httpx/_client.py", line 942, in _send_handling_auth
    response = self._send_handling_redirects(
  File "/home/xxxx/anaconda3/lib/python3.11/site-packages/httpx/_client.py", line 979, in _send_handling_redirects
    response = self._send_single_request(request)
  File "/home/xxxx/anaconda3/lib/python3.11/site-packages/httpx/_client.py", line 1015, in _send_single_request
    response = transport.handle_request(request)
  File "/home/xxxx/anaconda3/lib/python3.11/site-packages/httpx/_transports/default.py", line 233, in handle_request
    resp = self._pool.handle_request(req)
  File "/home/xxxx/anaconda3/lib/python3.11/site-packages/httpcore/_sync/connection_pool.py", line 216, in handle_request
    raise exc from None
  File "/home/xxxx/anaconda3/lib/python3.11/site-packages/httpcore/_sync/connection_pool.py", line 196, in handle_request
    response = connection.handle_request(
  File "/home/xxxx/anaconda3/lib/python3.11/site-packages/httpcore/_sync/connection.py", line 101, in handle_request
    return self._connection.handle_request(request)
  File "/home/xxxx/anaconda3/lib/python3.11/site-packages/httpcore/_sync/http2.py", line 113, in handle_request
    raise exc
  File "/home/xxxx/anaconda3/lib/python3.11/site-packages/httpcore/_sync/http2.py", line 109, in handle_request
    self._send_connection_init(**kwargs)
  File "/home/xxxx/anaconda3/lib/python3.11/site-packages/httpcore/_sync/http2.py", line 211, in _send_connection_init
    h2.settings.SettingCodes.ENABLE_CONNECT_PROTOCOL
  File "/home/xxxx/anaconda3/lib/python3.11/enum.py", line 784, in __getattr__
    raise AttributeError(name) from None
AttributeError: ENABLE_CONNECT_PROTOCOL

The above exception was the direct cause of the following exception:

Traceback (most recent call last):
  File "/home/xxxx/anaconda3/bin/onecomic", line 4, in <module>
    main()
  File "/home/xxxx/anaconda3/lib/python3.11/site-packages/onecomic/cli.py", line 446, in main
    comicbook.start_crawler()
  File "/home/xxxx/anaconda3/lib/python3.11/site-packages/onecomic/comicbook.py", line 97, in start_crawler
    self.refresh()
  File "/home/xxxx/anaconda3/lib/python3.11/site-packages/onecomic/comicbook.py", line 100, in refresh
    self.comicbook_item = self.crawler.get_comicbook_item()
  File "/home/xxxx/anaconda3/lib/python3.11/site-packages/onecomic/site/bilibili.py", line 124, in get_comicbook_item
    api_data = self.get_api_data()
  File "/home/xxxx/anaconda3/lib/python3.11/site-packages/onecomic/site/bilibili.py", line 115, in get_api_data
    response = self.send_request("POST", url=self.COMICBOOK_API, data=data)
  File "/home/xxxx/anaconda3/lib/python3.11/site-packages/onecomic/crawlerbase.py", line 267, in send_request
    raise URLException(msg) from e
onecomic.exceptions.URLException: NETWORK ERROR. can not open url: https://manga.bilibili.com/twirp/comic.v1.Comic/ComicDetail?device=pc&platform=web
```

如遇到以上报错，可以尝试升级一下这个依赖包解决
```
python3 -m pip install -U h2
```
