### intellij2020.1.2 版本使用spring initilizr 导入spring boot报错. 

#### 报错一: Error:(3, 32) java: 程序包org.springframework.boot不存在

![1593937516894](springframework标红和不存在报错/1593937516894-1593937517024.png)

打开setting->maven->runner, 把这个勾起, 再运行, 就能运行成功. 

![1593761605656](springframework标红和不存在报错/1593761605656-1593761605802.png)



#### 报错二: springframework 依赖会标红. 原因未知: 

#### 解决办法: 

![1593761853037](springframework标红和不存在报错/1593761853037-1593761853140.png)

![1593761875995](springframework标红和不存在报错/1593761875995-1593761876105.png)

运行此命令...就不会再标红. 





