# RStudio Server

====================================================

**Visit**  http://10.168.71.79:8787/   (site+8787 port)

**Log in with your user name and password**

====================================================

**Everyone** can visit the website and useR in linux server !!!

Suggest using it with **FileZilla** for file management and **Terminal** in windows

====================================================

## If your want to configure

https://posit.co/download/rstudio-server/

**Install R**

R is installed in:  **/opt/R/4.3.1/bin/R** (maybe should be migrated to the conda environment, r-4.3)

```
# CentOS 7
sudo yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm

sudo subscription-manager repos --enable "rhel-*-optional-rpms"

export R_VERSION=4.3.1

curl -O https://cdn.rstudio.com/r/centos-7/pkgs/R-${R_VERSION}-1-1.x86_64.rpm
sudo yum install R-${R_VERSION}-1-1.x86_64.rpm

# sudo yum remove R-${R_VERSION}
```
**R to the paths**

```
# remove previous paths
sudo rm /usr/local/bin/R
sudo rm /usr/local/bin/Rscript
# link R to the paths
sudo ln -s /opt/R/${R_VERSION}/bin/R /usr/local/bin/R
sudo ln -s /opt/R/${R_VERSION}/bin/Rscript /usr/local/bin/Rscript
```

**Set R ld-library (after the environment)**

```
sudo vim /opt/R/${R_VERSION}/lib/R/etc/ldpaths
# add these 
export LD_LIBRARY_PATH=/share/users/zwxu/.conda/envs/r-4.3/lib:$LD_LIBRARY_PATH
export R_LD_LIBRARY_PATH=/share/users/zwxu/.conda/envs/r-4.3/lib
```

**Install RStudio Server**

```
wget https://download2.rstudio.org/server/centos7/x86_64/rstudio-server-rhel-2023.06.2-561-x86_64.rpm
sudo yum install rstudio-server-rhel-2023.06.2-561-x86_64.rpm
```

**Configure server**

https://zhuanlan.zhihu.com/p/509471495

```
# set up r location
sudo vim /etc/rstudio/rserver.conf

# in vim
rsession-which-r=/opt/R/4.3.1/bin/R
rsession-ld-library-path=/share/users/zwxu/.conda/envs/r-4.3/lib

# restart rserver
rstudio-server restart

# kill specific apps for 8787 (if needed)
sudo netstat -anp | grep 8787
sudo kill -9 <pid>

# change firewall to allow access.. 
sudo firewall-cmd --add-port 8787/tcp
```

## Install packages

**Create environment**

```
# I put the r-4.3 environment in the share library
# So that everyone can load it
# here in /share/users/zwxu/.conda/envs/r-4.3
conda create -n r-4.3
conda activate r-4.3

# or activate by the loacl path
conda activate /share/users/zwxu/.conda/envs/r-4.3

# if you want to install packages here, but have no access
# we need to add you to the SharedUsers
sudo usermod -a -G SharedUsers your_user_name
```

**Install mamba to speed up** 

```
conda install -c conda-forge mamba
```

**Install spatial packages by mamba** 

```
# 2025-04-05
# sf and terra being harder to install
# this is from chatgpt and proves effective 

vim r-4.3.yml

# save this as r-4.3.yml and run in another environment
# mamba env create -f r-4.3.yml
name: r-4.3
channels:
  - conda-forge
dependencies:
  - conda=4.10  # specify a compatible version of conda
  - mamba=0.24.0  # try an older version of mamba 
  - r-base=4.3.1
  - r-terra
  - r-sf
  - gdal
  - libgdal
  - sqlite>=3.35
  - libsqlite
  - libtiff
  - xerces-c

conda env create -f r-4.3.yml
# mamba env create -f r-4.3.yml

conda activate r-4.3

# check and update packages 
R
library(terra)
install.packages('terra') # update terra
install.packages('raster') # raster not supported in conda-forge, but can be installed here.

library(terra)
library(sf)
library(raster)
```

**Install basic packages by mamba** 

```
conda install -c conda-forge mamba

# mamba install -c conda-forge r-PKGS

# 1. basic packages
mamba install -c conda-forge r-raster r-exactextractr r-tidyverse r-data.table r-ncdf4 r-devtools

# 2. machine learning
mamba install -c conda-forge \
  r-tidymodels \
  r-randomforest \
  r-vip \
  r-caret \
  r-xgboost \
  r-e1071 \
  r-ranger
  
# 3. statistical and extra packages 
mamba install -c conda-forge r-airGR r-changepoint r-exactextractr r-Evapotranspiration r-ggExtra r-lattice r-pracma r-shiny r-SPEI r-trend r-xlsx r-lubridate r-zoo r-REddyProc
```

**Backup my environment**

```conda env export -n r-4.3 --no-build > r-4.3_backup.yml
# export
conda env export -n r-4.3 --no-build > r-4.3_backup.yml

# rebuild if needed
mamba env create -n r-4.3_backup -f r-4.3_backup.yml
```

**Install packages in R** only if packages is **not available in conda**

```
# firstly set lib paths in R
.libPaths("/share/users/zwxu/.conda/envs/r-4.3/lib/R/library")
# install packages
install.packages('PKGS')
# such as rtop and other packages 
```

## Load environment in R

**Configure Renviron file** to set the paths 

```
# vim the Renviron file
# note that this is lib, rather than bin
sudo vim /opt/R/4.3.1/lib/R/etc/Renviron 

# change it as 
R_LIBS_USER='/share/users/zwxu/.conda/envs/r-4.3/lib/R/library'
R_LIBS_SITE='/share/users/zwxu/.conda/envs/r-4.3/lib/R/library'

# add this, which is essential for r-4.3 packages such as raster, rgdal, terra, sf
PROJ_LIB='/share/users/zwxu/.conda/envs/r-4.3/share/proj'
GDAL_DATA='/share/users/zwxu/.conda/envs/r-4.3/share/'

```

=====================================================



