## 阿里云ECS CentOS 7 图形化桌面安装
1. 登录服务器，执行命令 yum groups install "MATE Desktop"安装 MATE Desktop。
2. 执行命令 yum groups install "X Window System"安装 X Window System。
3. 执行命令 systemctl set-default graphical.target 设置默认通过桌面环境启动服务器。
4. 执行命令 reboot 重启服务器，您也可以在云服务器 ECS 控制台重启服务器。
5. 通过云服务器 ECS 控制台管理终端连接服务器，测试验证安装情况。

## centos7切换图形界面
    ls -ltr /lib/systemd/system/runlevel*.target #查看目前支持的运行级别  

    ln -svf /lib/systemd/system/runlevel5.target /etc/systemd/system/default.target  #图像界面模式  

    ln -svf /lib/systemd/system/runlevel3.target /etc/systemd/system/default.target  #命令行界面模式  

    systemctl set-default graphical.target  #效果同上


## 阿里云ECS CentOS 7 安装vnc-server
1. 安装vnc
yum install tigervnc-server -y  

2. 修改配置文件
vim /lib/systemd/system/vncserver@.service

编辑修改这两行的内容设置用户名

    ExecStart=/sbin/runuser -l root -c "/usr/bin/vncserver %i -geometry 800x600"  

    PIDFile=/root/.vnc/%H%i.pid
mv /lib/systemd/system/vncserver@.service /lib/systemd/system/vncserver@:1.service  

3. 重启systemd 
systemctl daemon-reload  

4. 设置vnc密码  
vncpasswd  

5. 启动服务
systemctl enable  vncserver@:1.service #设置开机启动
systemctl start vncserver@:1.service #启动服务  

6. 修改阿里云服务器安全测试，添加5901端口  

7. 查看vnc状态  
netstat -lp|grep -i vnc  

8. 修改xstart配置文件支持MATE桌面

vim /root/.vnc/xstartup  

    `#`Uncomment the following two lines for normal desktop:  

    unset SESSION_MANAGER  

    unset DBUS_SESSION_BUS_ADDRESS  

    `#`/etc/X11/xinit/xinitrc  

    /usr/bin/mate-session  

    [ -x /etc/vnc/xstartup ] && exec /etc/vnc/xstartup  

    [ -r $HOME/.Xresources ] && xrdb $HOME/.Xresources  

    xsetroot -solid grey  

    vncconfig -iconic &  

    x-terminal-emulator -geometry 80x24+10+10 -ls -title "$VNCDESKTOP Desktop" &  

    x-window-manager &
