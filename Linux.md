# **linux常用命令**



## **问题记录:**

注:(很多资源在国外,需要翻墙,否则无法通过shell命令拉取,osx推荐安装oh my zsh + oh my tmux)

1.ps命令无法找到: yum install -y procps

2.chsh命令无法找到:yum install util-linux-user

3.nohup无法执行多条指令: nohup zsh -c "command1 | command2 | command3"

4.shell命令太长,用'\回车'

5.osx shell无法代理,git下载项目超时: 通过手动配置代理文件,进行处理.(需翻墙)  

6.TMX OSX 无法复制问题

```
1. `brew install reattach-to-user-namespace`
2. 在 `~/.tmux.conf.loacl`中增加`set-option -g default-command "reattach-to-user-namespace -l zsh"`
3. 设置`tmux_conf_copy_to_os_clipboard=true`
4. 重启tmux.(tmux kill-server)
```



## 学习网站:

> #### Linux命令行快捷方式:
>
> https://gist.github.com/zhulianhua/befb8f61db8c72b4763d
>
> #### Linux命令:
>
> https://www.runoob.com/linux/linux-command-manual.html
>
> #### Tmux教程:
>
> https://www.ruanyifeng.com/blog/2019/10/tmux.html

## **1.文件管理**

>cat:打印文件到输出设备
>
>chmod:修改文件权限
>
>cmp:比较两个文件是否相同  diff
>
>more:翻滚查看文件 less head tail
>
>find:文件查找 \**\*
>
>grep:文件内容匹配查找 \**\*
>
>head:取内容前某一部分,可以是文件里的内容,也可以是文件取前几. \*
>
>ln:软链接 \*
>
>less:以页的方式阅读文件,可以配合find使用,比如find xxx | less \**
>
>mv:移动文件
>
>rm -rf \*:删除目录和文件
>
>mkdir:创建目录
>
>touch:可用来创建当前文件
>
>sort -nr:对结果集进行排序,r表示反排序 \*
>
>wc:统计文件的行数,单词,字数 ps -ef| wc -l
>
>pwd:显示当前工作路径
>
>stat:显示文件inode节点信息



```linux
grep 更适合单纯的查找或匹配文本
sed 更适合编辑匹配到的文本
awk 更适合格式化文本，对文本进行较复杂格式处理
```



## **2.磁盘管理**

> Df -h:查看整体磁盘使用情况
>
> du -ah /\*
>
> free -h:查看内存使用情况



### 高级命令

> swapon:虚拟内存信息,对应swapoff
>
> sync:将文件缓存数据刷新到硬盘保存



## **3.网络通讯**

> curl:基于应用层,以http协议请求服务器,可模拟各种http请求方式.  ****
>
> https://www.ruanyifeng.com/blog/2019/09/curl-reference.html
>
> ping:基于网络层icmp协议请求服务器,测试网络情况.(与端口无关)
>
> telnet:远程连接服务器(可测试服务器端口是否可连接)
>
> ifconfig:查看网络状态和设备
>
> netstat -a:查看网络连接情况,比如socket



## **4.系统管理**

> ps:查询进程(ps -aux)
>
> top:进程使用cpu情况
>
> kill:无条件退出进程
>
> nice:优先执行某条指令
>
> top: 查看用户空间程序和cpu使用率\**
>
> sudo:以管理者身份执行命令.
>
> w/who:查看登录用户信息
>
> time:执行某条指令时所需要的时间
>
> set/export:查看当前shell环境变量

## **5.其他命令**

> xargs:将标准输入转为命令行参数. 比如 find /path -type f | xargs -p  grep 'abc'
>
> 参考链接:https://www.ruanyifeng.com/blog/2019/08/xargs-tutorial.html
>
> nohup:不挂断执行命令,一般配合&进行后台永久执行.



## **常用命令**

> **find / -type f -size +1M -print0|xargs -0 du -h|sort -nr // 查找大文件**
>
> **tail -n 50 -f file_name // 实时查看日志**
>
> **du -sh /\* | sort -nr // 查看根目录下各个目录大小**
>
> **grep -r “text_content\*” path // 查找某个目录下所包含内容的文件**
>
> **ps -ef | grep xxx // 查询进程**
>
> **top -c // 查询进程使用cpu情况**
>
> **free -h  //查看内存使用情况**
>
> **nohup command>file_name 2>&1 & // 非挂起后台运行脚本**



## **Tmux**

> 直接github上安装oh my tmux,相当于tpm的升级版,对于快捷键和操作更加方便.
>
> 注:开启鼠标模式,<prefix> + m.
>
> ##### frequent commands and shorcuts(personal experiences) 
>
> ###### session:
>
> | commands/shortcuts                     | description                  |
> | -------------------------------------- | ---------------------------- |
> | tmux new -s session_name               | 创建session                  |
> | tmux a -t session_name(a指attach)      | 选择session                  |
> | tmux ls                                | 查看session列表              |
> | ctrl + d                               | 关闭session                  |
> | ctrl + b + d (dettach)                 | 暂时断开当前session.(还存在) |
> | ctrl + b + s (switch)                  | 切换session                  |
> | tmux list-key\|less  或者 ctrl + b + ? | 查看当前tmux所有快捷键       |
>
> ###### window:
>
> | commands/shortcuts | description  |
> | ------------------ | ------------ |
> | ctrl + b + c       | 创建窗口     |
> | ctrl + b + w       | 切换窗口     |
> | ctrl + b + &       | 关闭当前窗口 |
>
> ###### panel:(可用鼠标操作,无需记)
>
> | commands/shortcuts | description  |
> | ------------------ | ------------ |
> | ctrl + b + "       | 上下切割面板 |
> | ctrl + b + %       | 左右切割面板 |
> | ctrl + b + x       | 关闭当前面板 |
> | ctrl + b + 方向键  | 切换面板     |