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

***geeadd*** 

https://github.com/samapriya/gee_asset_manager_addon

https://pypi.org/project/geeadd/

```
# install
pip install geeadd --user
geeadd readme

# currently used 
geeadd delete --id <assetID>
```

***geeup*** 

https://github.com/samapriya/geeup#geeup-tabup

Example - upload SILO_d8

```
# 1 - create meta data 
geeup getmeta --input "I:\projects\fire\ETau\SILO_d8" --metadata "I:\projects\fire\ETau\SILO_d8\meta.csv"

# 2 - add system_time in R
library(magrittr)
ofn <- 'I:/projects/fire/ETau/SILO_d8/meta.csv'
dt <- data.table::fread(ofn)
dt[['system::time_start']] <- NULL
dt[['system:time_start']] <- stringr::str_extract(dt$id_no, '\\d*-\\d*-\\d*') %>% 
  paste0(' 00:00:00') %>%
  lubridate::ymd_hms %>% as.integer()
fwrite(dt, ofn)

# 3 - upload files to GEE with system_time in each tile
geeup upload --source "I:\projects\fire\ETau\SILO_d8" --metadata "I:\projects\fire\ETau\SILO_d8\meta.csv" --dest "projects/pml_evapotranspiration/test/fire/SEAU/SILO_d8_SEAU" --user "xuzhw5@mail2.sysu.edu.cn" --nodata -9999 --pyramids MODE
```







