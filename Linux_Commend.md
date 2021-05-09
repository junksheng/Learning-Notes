cat >> Linux_Commend.md
ls /usr/bin | tee ls.txt | grep zip
tee 把输入流复制一份到ls.txt中, 但原本的输入流还会继续传输
echo "your words" >> file 可以帮你追加一句话到文件里面
$可以表示最后一个的意思
sed 'Nd' file 可以删除文件中的某一行, 如果要对文件直接修改需要加上-i
可用0表示算术表达式
echo Number_{1..5}
Number_1 Number_2 Number_3 Number_4 Number_5
花括号可以嵌套,运用好创建和删除一系列文件很方便
printenv | less 可以查单当前变量列表
echo 加上-e可以使\n这些反斜杠转义字符序列生效
umask 可以设置掩码值, 为1的位表示没有相应的权限
chown -更改文件所有者和用户组
Ubuntu不允许用户登录到root账号,不能为root账号设置密码,只能用sudo赋予超级用户权限
top & 添加&可以让命令放置在后台执行
jobs 可以列出后台运行的任务
fg %n 可以让任务返回前台
ctrl-z 可以让任务暂停, 然后用 bg %n移到后台执行
diff 和 patch 可以快速比对和更新文件
sed功能很强大, 但是有些复杂
