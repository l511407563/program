##### mysql安装 
    http://www.linuxidc.com/Linux/2016-09/135288.htm
    
#### mysql安装报错 部分rpm包查找不到无法安装服务，重新卸载安装
    https://www.jianshu.com/p/7b8c4dea6829

##### 启动和关闭mysqld服务器
    查看mysql是否启动
        ps aux | grep mysqld
        或  
        service mysqld status
        或
        service mysql status
    
    启动
        service mysql start
    
    关闭
        service mysql stop
        
    重启
        service mysql restart
        或
        systemctl restart mysqld
        
    
##### 登录mysql客户端
    登录mysql客户端
        mysql -u root -p 密码
    
##### 修改密码
    set password for root@localhost=password('你的密码');