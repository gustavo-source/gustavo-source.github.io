---
layout: post
title: Linux速查手册
category: 资源
keywords: 速查，Linux
---

[toc]
## 文件相关
### 文件查看
```
显示隐藏文件
ls -al
显示包含数字的文件名和目录名
ls *[0-9]* 
查看文件有多少行
wc -l filename  
cat xxx|wc -i
查看文件夹内的文件数目
ls -l | grep '^-' | wc -l
```

### 文件操作
```
复制文件

cp source dest  

递归复制整个文件夹

cp -r sourceFolder targetFolder  

远程拷贝

scp sourecFile name@ip:addr  

```
### 文件查找
```
精确查找
find ~ -name "target.java"
模糊查找
find ~ -name "target*"
递归查找所有的xml文件
find . -name "*.xml"  
不区分文件名去查找文件
find ~ -iname "target*"
找出七天前的文件
find / -type f -mtime +7 -print
递归查找所有文件内容中包含hello world的xml文件
find . -name "*" |xargs grep "hello"  
删除文件大小为零的文件
find ./ -size 0 | xargs rm -f &  
```

### 压缩解压
```
单个目录压缩
tar -czvf my.tar dir1
解压文件
tar -xvzf test.tar.gz
```

## 内存进程
### 进程相关
```
查看java进程
ps aux|grep java 
终止线程号位19979的进程
kill -9 19979 
检查一个程序是否运行
ps –ef|grep tomcate
```

### 系统信息
```
显示机器的处理器架构
arch 
uname -m
显示内核的版本
cat /proc/version 
显示CPU的信息
cat /proc/cpuinfo
lscpu
显示已载入系统的模块
lsmod  
查看系统IO
iostat
查询红帽版本
cat /etc/redhat-release
```

### 磁盘信息
```
显示已经挂载的分区列表
df -h 
查看内存占用
top 
显示当前文件下 Top 10 空间占用的文件/目录，
s 表示不显示每个子目录或文件的大小
h 表示用更加自然的方式显示（比如 K/M/G 这样）
du -sh * | sort -nr | head
```

## 日志相关
### 日志处理
```
查询日志尾部最后300行的日志
tail -300 catalina.log
截取以$分隔符的1和4位置的内容
cat catalina.out |grep '223.71.90.122'|grep '/iBrand/evaluate/add' |awk -F '$' '{print $1,$4}'|more
搜索2019-（1）-（1-29） 匹配路径loginByPassword （忽略-v之后的关键字） 排序|去重 并导出csv (>为覆盖输出 >>为持续输出)
cat catalina.out |grep '2019-1[0-1]-[0-2][0-9]'|grep 'loginByPassword'|grep -v 'ibrand\|test\|Mapped\|lj\|somthing'|sort |uniq > /tmp/loginByPassword.csv
清空日志
echo "" > filename
查询关键字
more logfile.log.2018-12-20 | grep "Exception"
cat Server1-info.log Server1_kvm_73-info.log |grep " 11:02"|grep "106.12.146.87"
定位行数
cat -n test.log |grep "地形"
查询某行后的100行
cat -n catalina.out |tail -n +2224544|head -n 100
从后向前查看定位
tac catalina.out | grep 'Initializing c3p0 pool... com.mchange.v2.c3p0.ComboPooledDataSource'
tac catalina.out | grep '缓存加载完毕'
查询多个文件
cat Server1-info.log Server1_kvm_73-info.log Server1-info.log Server2_kvm_74-info.log Server1-info.log Server3_kvm_131-info.log |grep "106.12.148.198"
匹配 file.txt 中包含 word1 或 word2 或 word3 的行。
满足其中任意条件（word1、word2和word3之一）就会匹配。
grep -E "word1|word2|word3" file.txt
必须同时满足三个条件（word1、word2和word3）才匹配。
grep word1 file.txt | grep word2 |grep word3
sort 文件 | uniq -c sort排序 uniq去重 查询出现的次数
访问量前10的ip
cat access.log|cut -f1 -d " " | sort | uniq -c | sort -k l -n -r | head -10
访问量前10的url
cat access.log|cut -f4 -d " " | sort | uniq -c | sort -k l -n -r | head -10
统计日志某行出现次数
cat **.log | grep "2019-12-11 09" |grep "AccessWebVerifyFilter" |wc -l
```

## 其他
### 其他操作
```
查看系统的定时任务
crontab -l
编辑定时任务
crontab -e
ip查询
curl https://ip.cn 
后台启动jar
nohup java -jar name.jar --server.port=17076 >> log.out 2>&1 &
nohup $JRE_HOME/bin/java -Xms256m -Xmx512m -jar $JAR_NAME >/dev/null 2>&1 &
```