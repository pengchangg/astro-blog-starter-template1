---
title: "进阶 Bash 技巧大全（实战向）"
description: "Linux UNIX BASH"
pubDate: "Jun 01 2026"
heroImage: "/wallhaven-qrjmgl.jpg"
---

## 进阶 Bash 技巧大全（实战向）

> 面向日常开发、运维、自动化脚本的 Bash 进阶技巧合集\n目标：**高效 / 稳定 / 可维护**


---

## 一、严格模式（Strongly Recommended）

### 1. Bash Strict Mode

``` bash
set -Eeuo pipefail
IFS=$'\n\t'
```

* `-e`：命令失败立即退出\\
* `-u`：使用未定义变量直接报错\\
* `-o pipefail`：管道中任一命令失败即失败\\
* `-E`：让 `trap ERR` 在函数中生效

### 2. 错误定位

``` bash
trap 'echo "Error at line $LINENO"' ERR
```


---

## 二、变量与参数展开

``` bash
file="archive.tar.gz"
${file%.gz}
${file%%.*}
${file##*.}
${file#*.}
```


---

## 三、数组与关联数组

``` bash
arr=(a b c)
declare -A status
status[nginx]=running
```


---

## 四、循环与批量处理

``` bash
find . -type f | while IFS= read -r f; do
  echo "$f"
done
```


---

## 五、函数规范

``` bash
func() {
  local v="value"
  echo "$v"
}
```


---

## 六、文件描述符

``` bash
exec 3>out.log
echo hello >&3
exec 3>&-
```


---

## 七、调试技巧

``` bash
bash -x script.sh
```


---

## 八、条件判断

``` bash
[[ -f file && -r file ]]
```


---

## 九、信号处理

``` bash
trap cleanup EXIT INT TERM
```


---

## 十、效率工具

``` bash
rg TODO | fzf
```


---

## 十一、Here Document

``` bash
cat <<EOF > file
text
EOF
```


---

## 十二、最佳实践

``` bash
#!/usr/bin/env bash
```


## 十三、快捷键

| 快捷键 | 作用 |
|----|----|
| `Ctrl + A` | 光标跳到行首 |
| `Ctrl + E` | 光标跳到行尾 |
| `Ctrl + B` | 向左移动一个字符 |
| `Ctrl + F` | 向右移动一个字符 |
| `Ctrl + P` | 上一条命令 |
| `Ctrl + N` | 下一条命令 |
| `Ctrl + R` | 反向历史搜索 |
| `Ctrl + L` | 清屏（`clear-screen`） |
| `Ctrl + C` | 中断当前命令 |
| `Ctrl + D` | EOF（空行时退出 shell） |

| 快捷键 | 作用 |
|----|----|
| `Alt + B` | 向左跳一个单词 |
| `Alt + F` | 向右跳一个单词 |
| `Ctrl + W` | 删除光标前的一个单词 |
| `Alt + D` | 删除光标后的一个单词 |
| `Ctrl + U` | 删除光标前的所有内容 |
| `Ctrl + K` | 删除光标后的所有内容 |
| `Ctrl + Y` | 粘贴（yank） |
| `Alt + .` | 插入上一条命令的最后一个参数 |

| 快捷键 | 作用 |
|----|----|
| `Ctrl + R` | 反向搜索历史 |
| `Ctrl + G` | 退出搜索 |
| `!!` | 执行上一条命令 |
| `!$` | 上一条命令的最后参数 |
| `!*` | 上一条命令的所有参数 |
| `!^` | 上一条命令的第一个参数 |
| `!:n` | 上一条命令的第 n 个参数 |
| `!command` | 最近以 command开头的命令 |

