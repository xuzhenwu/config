# GEE

## Setup

***command line tool*** https://developers.google.com/earth-engine/guides/command_line

```Py
# powershell
pip install earthengine-api --upgrade
```

before authenticating, please ***set proxy***

***powershell &cmd***

```
# in powershell
# http
$Env:HTTP_PROXY = "http://127.0.0.1:10810"
$Env:HTTPS_PROXY = "http://127.0.0.1:10810"
```

***authenticate***

```
# in powershell
earthengine authenticate --auth_mode=notebook
```

***python***

```
# in powershell
pip install pysocks

# set proxy
import socket
import socks
socks.set_default_proxy(socks.SOCKS5, "127.0.0.1", 10808)
socket.socket = socks.socksocket

# authenticate ee
import ee
print(ee.__version__)
ee.Authenticate()
ee.Initialize()
```

## Extensions

***gee_asset_manager_addon*** https://github.com/samapriya/gee_asset_manager_addon

```
# install
pip install geeadd --user
geeadd readme

# currently used 
geeadd delete --id <assetID>


```

## 初定的命名规范

一些建议如下

**1 符号和名字**

文件名应有一定意义，尽可能简洁，最好不超过两个单词，并在顺序执行时添加数字前缀，最终以.js结尾

```
fit_model.R
1-main_chess.R
```

变量名和函数名同理，非必要时最好不超过两个单词，以“_”分隔单词，不采用任何大写

```
rearrange_files
trans_month_day
```

单词是否缩写以及顺序请慎重斟酌，最好以能连成句子的顺序排列为准，如果GEE API的函数示意

```
Map.addLayer
ee.ImageCollection.filterBounds
```

调用参数化较复杂的函数请根据需求换行

目前已纳入的缩写如下

```
pkg				packages
imgcol			ImageCollection
movmean			Moving mean


```





