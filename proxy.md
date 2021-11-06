Please be careful about proxy port, since most issues happen because of it.

***powershell***

```
$Env:HTTP_PROXY = "http://127.0.0.1:10810"
$Env:HTTPS_PROXY = "http://127.0.0.1:10810"
```

***cmd***

```
# socks5
set http_proxy=http://127.0.0.1:10810
set https_proxy=https://127.0.0.1:10810
```

***linux***

```
export HTTP_PROXY=http://127.0.0.1:10810
export HTTPS_PROXY=http://127.0.0.1:10810
```

***R***

```
Sys.setenv("https_proxy" = "https://127.0.0.1:10810") 
```

***python***

```
import socket
import socks
socks.set_default_proxy(socks.SOCKS5, "127.0.0.1", 10808)
socket.socket = socks.socksocket
```

