# R

## Environmental variables

set these in **Rprofile.site** in [C:\Program Files\R\R-4.0.2\etc\Rprofile.site], which is default setting

```
# set EN environment
.InitEnv <- function() {
    Sys.getenv()
    Sys.setenv(LANG = "en")
    Sys.setlocale("LC_TIME", "C")
    }
```

## Backup R packages

all packages locates in [C:\Users\Administrator\Documents\R\win-library\4.0]

copy them to your backup folder, and paste back when you try to use R in a new machine

## High-res Figure Output

save images as '.pdf' format, and edit it in Adobe Illustrator, export as a high-resolution 'jpg' figure.

meanwhile, to support Helvetica font in R figures, please install them in your machine 