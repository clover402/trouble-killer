## problem1:
Filezilla连接ftp服务器：“服务器发回了不可路由的地址。使用服务器地址代替。”
## resolve1: 
1. 编辑-设置-连接-FTP-被动模式，将“使用服务器的外部ip地址来代替”改为“回到主动模式”即可。
2. 站点配置-传输设置-传输模式选“主动”
3. 如果还不行，站点配置-常规-加密-只使用明文FTP（不安全）
  
## problem2：
FileZilla文件传输乱码问题
## resolve2：
传输-传输类型-二进制 
