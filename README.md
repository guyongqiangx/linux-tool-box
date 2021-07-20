软件工程师常用的 linux 命令行工具速查表

Table of Contents
=================

* [1. 一般工具](#1-一般工具)
   * [grep](#grep)
   * [find](#find)
   * [sed](#sed)
   * [awk](#awk)
* [2. 二进制工具](#2-二进制工具)
   * [hexdump](#hexdump)
   * [xxd](#xxd)
   * [od](#od)
* [3. 网络工具](#3-网络工具)

# 1. 一般工具
## grep
```shell
grep --help | grep '\-c'                  # 搜索中带有'-'字符, 容易被当做'-c'选项, 使用'\'字符转义
grep -n "root" /etc/{passwd,group}        # '-n' 显示行号
grep -r "grep" .                          # '-r' 递归查找, 但不跟踪符号链接文件和目录
grep -R "grep" .                          # '-R' 递归查找, 跟踪符号链接文件和目录
grep -i "grep"                            # '-i' 忽略大小写
grep -w "grep"                            # '-w' 匹配完整单次
grep -A 5 "grep"                          # '-A', after-contect, 显示后面的行数
grep -B 5 "grep"                          # '-B', before-context, 显示前面的行数
grep -C 5 "grep"                          # '-C', context, 显示上下文的行数(相当于 '-A' 和 '-B' 指定同样的参数)

grep -R otp . --exclude=*.{s,i,o,a}       # '--exclude', 排除搜索的文件 (忽略文件 *.s, *.i, *.o 和 *.a )
grep -R otp . --exclude-dir={objs,doc}    # '--exclude-dir', 排除搜索的文件夹 (忽略目录 objs 和 doc)
grep -R otp . --include=*.{c,s}           # '--include', 指定搜索的文件 (在 *.c 和 *.s 中搜索)
grep -RI otp .                            # '-I' 不搜索二进制文件

grep -R  rocky /etc 2>/dev/null           # 不显示错误消息, 将错误重定向到 /dev/null 设备
grep -Rs rocky /etc                       # '-s' 抑制错误消息, 相当于将错误重定向到 /dev/null
grep -Rh "^root" /etc                     # '-h' 搜索结果不显示文件名
grep -Rl "^root" /etc                     # '-l' 搜索结果只显示文件名
grep -RL "^root" /etc                     # '-L' 搜索结果显示不匹配的文件名

# 以下较少使用
grep -v "^#" /etc/passwd                  # '-v' 反向查找不匹配的结果
grep -Rq "^root" /etc                     # '-q' 安静模式, 不显示匹配结果

grep -E -c "([0-9]{1,3}\.){3}[0-9]{1,3}" /etc/network/interfaces # '-c' 显示匹配数量
grep -E -o "([0-9]{1,3}\.){3}[0-9]{1,3}" /etc/network/interfaces # '-o' 只显示匹配内容

# 综合示例
# 搜索字符串 V2, 排除 *.h *.c, *.cpp 文件和 obj.* 目录
grep -rnI V2 . --exclude=*.{h,c,cpp} --exclude-dir=obj.*

# 在 device 和 build 下搜索 CMDLINE, 忽略 docs 目录
grep -rn CMDLINE device build --exclude-dir=docs

```
## find
## sed
## awk

# 2. 二进制工具
## hexdump
## xxd
## od

# 3. 网络工具
