# R-code
R code

## 批量读取指定文件夹中的 Excel 文件

以下示例展示如何在 Windows 环境下使用 `readxl` 从指定目录批量读取 Excel 文件，并合并为一个数据框。将路径替换为实际的文件夹，例如 `"E:/课程材料/数据分析/期末作业数据"`（在 R 中使用 `/` 作为分隔符或用双反斜杠 `\\`）。

```r
library(tidyverse)
library(readxl)

excel_dir <- "E:/课程材料/数据分析/期末作业数据"

files <- list.files(excel_dir, pattern = "\\.xlsx?$", full.names = TRUE)

data_all <- files %>%
  set_names() %>%
  map_dfr(~ readxl::read_excel(.x, sheet = 1), .id = "source_file")
```

- `excel_dir` 指向包含 Excel 文件的目标目录。
- `full.names = TRUE` 确保返回完整路径以便直接读取。
- `.id = "source_file"` 在合并后保留文件来源，方便追踪。
