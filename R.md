# R

## Environmental variables

set these in $R_HOME

```
.InitEnv <- function() {
    Sys.getenv()
    Sys.setenv(LANG = "en")
    Sys.setlocale("LC_TIME", "C")
    }
```

