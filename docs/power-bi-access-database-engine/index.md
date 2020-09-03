# Power bi导入数据出现:microsoft.ACE.oledb.12.0无法连接解决办法

###问题描述:
用powerbi的powerquery导入数据的时候出现下图:
本错误是由于你使用了ACCESS2007版本建立的数据库,但服务器中没有相配合使用的程序,所以出错.

未在本地计算机上注册“microsoft.ACE.oledb.12.0”提供程序。
![powerbi报错](https://img.ibolee.com/git_blog/powerbi.png)

###解决办法:

下载安装一个AccessDatabaseEngine,注意选择自己需要的位数,比如上图报错是64位.

下载地址:https://www.microsoft.com/zh-cn/download/confirmation.aspx?id=13255
