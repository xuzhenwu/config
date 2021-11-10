# R

## Environmental variables

set these in **Rprofile.site** [C:\Program Files\R\R-4.0.2\etc\Rprofile.site]

```
# set EN environment
.InitEnv <- function() {
    Sys.getenv()
    Sys.setenv(LANG = "en")
    Sys.setlocale("LC_TIME", "C")
    }
```

## R packages

all packages locates in [C:\Users\Administrator\Documents\R\win-library\4.0]

copy them to your backup folder, and paste back when you try to use R in a new machine