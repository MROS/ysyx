本作業要求閱讀 [计算机教育中缺失的一课](https://missing-semester-cn.github.io/) ，並完成

- 课程概览与shell
- Shell工具和脚本
- 编辑器 (Vim)
- 数据整理
- 命令行环境
- 版本控制(Git)

這幾章的習題。我個人使用 Linux（主要是 Debian 系） 做筆電或桌機的系統已經長達十年，所以對這個作業的態度是查缺補漏，本文件將羅列這份資料中，老手仍能受益之處。


## 课程概览与shell

所有已註冊設備都能在 `/sys/class` 找到，但各個設備有哪些資訊各不相同了。

### 練習 10

```
# 對比兩者，此處 temp 需除以 1000 方爲攝氏
cat /sys/class/thermal/thermal_zone*/type
cat /sys/class/thermal/thermal_zone*/temp
```

## Shell工具和脚本

> <( CMD ) 会执行 CMD 并将结果输出到一个临时文件中，并将 <( CMD ) 替换成临时文件名。这在我们希望返回值通过文件而不是STDIN传递时很有用。例如， diff <(ls foo) <(ls bar) 会显示文件夹 foo 和 bar 中文件的区别。

`?` 可以匹配任意一個字元。

[ShellCheck](https://github.com/koalaman/shellcheck)：shell script linter。

`find` 接 `-exec 命令` 可以對每個找到的檔案執行`命令`，fd 則是接 `-x` 或 `--exec`。

[autojump](https://github.com/wting/autojump) : 更強的 `cd` ，可以寫部分路徑就跳躍到曾經去過的目錄、跳躍到孫目錄。

### 練習 1
`ls -alh --color`
### 練習 2
```
#!/bin/bash

TEMP_DIR="."
marco () {
    TEMP_DIR=$(pwd)
}

polo () {
    cd $TEMP_DIR || exit
}
```

### 練習 3
```
#!/usr/bin/env bash

RESULT=0
TMP=$(mktemp)
echo "$TMP"

count=0
while [ $RESULT -eq 0 ]; do
    ./may_fail.sh > "$TMP" 2> "$TMP";
    RESULT=$?
    count=$((count + 1))
done

cat "$TMP"
echo "第 $count 時失敗"
```

### 練習 4
`fd -e html | xargs -d "\n" zip html.zip`

### 練習 5
`fd --exec stat --format "%Y %n" | sort -n -r | awk '{print $2}'`

## 编辑器 (Vim)
無

## 数据整理
## 命令行环境
## 版本控制(Git)
