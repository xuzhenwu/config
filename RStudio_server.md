# RStudio Server

====================================================

**Visit**  http://10.168.71.190:8787/   (site+8787 port)

**Log in with your user name and password**

====================================================

**Everyone** can visit the website and useR in linux server !!!

Suggest using it with **FileZilla** for file management and **Terminal** in windows

====================================================

## If your want to configure

https://posit.co/download/rstudio-server/

**Install R**

R is installed in:  **/opt/R/4.3.1/bin/R** (maybe should be migrated to the conda environment, rspatial)

```
# CentOS 7
sudo yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
sudo subscription-manager repos --enable "rhel-*-optional-rpms"

export R_VERSION=4.3.1

curl -O https://cdn.rstudio.com/r/centos-7/pkgs/R-${R_VERSION}-1-1.x86_64.rpm
sudo yum install R-${R_VERSION}-1-1.x86_64.rpm
```
R in the paths

```
# remove previous paths
sudo rm /usr/local/bin/R
sudo rm /usr/local/bin/Rscript
# link R to the paths
sudo ln -s /opt/R/${R_VERSION}/bin/R /usr/local/bin/R
sudo ln -s /opt/R/${R_VERSION}/bin/Rscript /usr/local/bin/Rscript
```

R ld-library 

```
sudo vim /opt/R/${R_VERSION}/etc/ldpaths
# add these 
export LD_LIBRARY_PATH=/share/users/zwxu/.conda/envs/rspatial/lib:$LD_LIBRARY_PATH
export R_LD_LIBRARY_PATH=/share/users/zwxu/.conda/envs/rspatial/lib
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
rsession-ld-library-path=/share/users/zwxu/.conda/envs/rspatial/lib
# restart rserver
rstudio-server restart
# kill specific apps for 8787 (if needed)
sudo netstat -anp | grep 8787
sudo kill -9 <pid>
```

## Install packages

**Create environment**

```
# I put the rspatil environment in the share library
# So that everyone can load it
# here in /share/users/zwxu/.conda/envs/rspatial
conda create -n rspatial
conda activate rspatial
```

**Install mamba to speed up** 

```
conda install -c conda-forge mamba
```

**Install basic packages by mamba** 

```
# mamba install -c conda-forge r-PKGS
# basic packages
mamba install -c conda-forge r-raster r-terra
mamba install -c conda-forge r-tidyverse
mamba install -c conda-forge r-data.table

mamba install -c conda-forge r-airGR r-changepoint r-exactextractr r-Evapotranspiration r-ggExtra r-lattice r-pracma r-shiny r-SPEI r-trend r-xlsx
```

**Install packages in R** only if packages is **not available in conda**

```
# firstly set lib paths in R
.libPaths("/share/users/zwxu/.conda/envs/rspatial/lib/R/library")
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
R_LIBS_USER='/share/users/zwxu/.conda/envs/rspatial'
R_LIBS_SITE='/share/users/zwxu/.conda/envs/rspatial'

# add this, which is essential for rspatial packages such as raster, rgdal, terra, sf
PROJ_LIB='/share/users/zwxu/.conda/envs/rspatial/share/proj'
GDAL_DATA='/share/users/zwxu/.conda/envs/rspatial/share/'

```

=====================================================



