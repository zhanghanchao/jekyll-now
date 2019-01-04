---
layout: post
title: shell学习笔记
---

## 数组
```bash
定义数组 array=(1 2 3 4)
打印数组 echo ${array[@]} =>1 2 3 4
打印数组长度 echo ${#array[@]} =>4
```

## 查看路径
```bash
查看python 路径 which python => /usr/bin/python  需要配置环境变量
```
## 反引号``
```bash
a=`ls`
$a => 相当于执行ls 命令
echo -e “a\nab”开启转义
```
## 变量操作：
```bash
a=1;b=2
echo $((a+b)) =>3
```
## 布尔判断
判断上次执行是否正确echo $?  正确显示0 错误显示非0
## 浮点数计算
* shell不支持浮点数计算  如echo $((2/3))
* 可使用awk 'BEGIN{print 2/3}' =>0.66667 
## 切片
```bash
s="hello world"
echo "${s:3}" =>lo world
echo "${s:3:2}" => lo
echo "${s#he}" => llo world
echo "${s#*e}" =>llo world 
```
## 贪婪匹配，最后一个开始切片
```bash
echo "$(s##*l)" =>d
```
## 去尾
```bash
echo "${s%l*}" => hello wor
echo "${s%%l*}" => he
```
## 替换
```bash
echo "${s/hel/aaa}" => aaalo world
```
## 算术判断在中括号[]进行
```bash
是否相等判断[ 2 -eq 2 ];echo $? =>0 空格不能少
小于[ 2 -lt 3];echo $? =>0
大于[2 -gt 1 -a 3 -ge 2];echo $? =>0  逻辑非-a
大于[2 -gt 1 -o 3 -ge 2];echo $? =>0   逻辑或-o
大于等于ge=great equal  小于等于le=low equal
```
## shell内置
* [ -e note.txt ] 判断文件是否存在
## if语句
```bash
if [ -e test ];then echo exist;else echo not exist;fi;判断文件是否存在
简化写法：[ -e test ]&&echo exist||echo not exist
echo "1" && echo "2" || echo "3" && echo "4" || echo "5" || echo "6" && echo "7" && echo "8" || echo "9"=>1,2,4,7,8
```
## for循环：
```bash
array=(1 2 3 4 5)
for ((i=1;i<${#array[@]};i++));do echo $i;done 
```
## 遍历循环：
```bash
for i in ${array[@];i++};do echo $i;done
for x in `ls`;do echo $x;done输出ls结果
```
## while循环：
```bash
i=1;[ $i -lt 3];do echo $i;((i=i+1));done
while read x;echo $x;done < 3;打印文件3的内容
```
## 重定向：
```bash
echo "hello" > hello.txt 
echo "hello" >> hello.txt追加一行，不覆盖
```
* ()在sub_shell环境执行，{}在当前环境执行
* ps -e 查看系统全部进程
* sleep 10& 后台运行任务
* jobs查看正在运行的任务
* bg 2将一个在后台暂停的命令，变成继续执行
* fg 2 将进程搬到前台运行
## 环境变量
.bash_profile里面的环境变量改变后，执行source ~/.bash_profile初始化文档
## linux三大剑客之grep 文本搜索命令
```bash
grep “hello” text.txt
grep -i 忽略大小写
cat text.txt | grep “hello"
while read k;do echo $k;curl -s http://www.baidu.com/s?wd=$k;done < baidu.keyword | grep -o "结果约[0-9,]*" 
```
## linux三大剑客之awk 文本分析工具 默认空格为分隔符
```bash
echo "123|456|789" | awk -F '|' '{print $1}'
echo "123+456-789" | awk -F '+|-' '{print $1,$2}'
curl -s http://www.baidu.com/s?wd=mp3 | grep -o "结果约[0-9,]*" | awk -F '个|约' '{print $0}
获取百度mp3的评价数：
curl -s http://www.baidu.com/s?wd=mp3 | grep "条评价" | awk -F 'data-from="ps_pc4">' '{print $2}' | awk -F "条" '{print $1}'
```
## linux三大剑客之sed 处理，编辑文本文件
```bash
echo "cat dog fish cat" | sed 's/cat/bears/' => bears dog fish cat
echo "cat dog fish cat" | sed 's/cat/bears/g' => bears dog fish bears
sed -i 's/hello/A' text.txt
备份：sed -i.bak 's/hello/A' text.txt
```
## BEGIN END语句
awk BEGIN{}  是在文件开始扫描前进行的操作  END {} 是扫描结束后 进行的操作  ;一般的操作都是需要在BEGIN 设置一个初始的量
打印/etc/passwd文件的所有用户名  NR表示读取的行数
```bash
cat /etc/passwd | awk -F ':' 'BEGIN{count=0} {name[count]=$1;count++}END{for(i=0;i<NR;i++)print i,name[i]}'
bash
## 获取本地IP:
```bash
curl -s http://www.baidu.com/s?wd=ip | grep "本机IP:&nbsp;" | awk -F '本机IP:&nbsp;|</span>上海' '{print $2}’
a=`curl -s https://testerhome.com/topics|grep -o 'href="/topics/[0-9]*"'|awk -F '/|"' '{print $4}'`;for id in $a;do url='https://testerhome.com/topics/'$id;zan=`curl -s $url | grep -o -m1 '<span>[0-9]*' | awk -F '>' '{print $2}'`;if [ -n "$zan" ];then echo $url '点赞人数' $zan;else echo $url '点赞人数' 0;fi;done|awk -F '/' '{print $NF}'
```
## 提取对外链接IP数量：
```bash
提取列表：netstat -tnp | sed 1,2d | awk '{print $5}' | awk -F ':' '{print $1}' 
统计：netstat -tnp | sed 1,2d | awk '{print $5}' | awk -F ':' '{print $1}' | sort | uniq -c| sort
```
## 从ngix log中提取数据并可视化：
```bash
cat 1206_2.log | sed -n '/07:48:00/,/07:52:00/p' | gnuplot -e "set terminal dumb; set datafile separator ' ';set timefmt '[%d/%b/%Y:%H:%M:%S'; set ydata time; set format y '%H:%M:%S';plot '<cat' using 8:4 with lines"
```
