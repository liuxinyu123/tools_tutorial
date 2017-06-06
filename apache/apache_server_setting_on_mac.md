# apache 命令    
1. 开启apache服务器命令    
> `sudo apachectl start`     
2. 关闭apache服务器命令    
> `sudo apachectl stop`     
3. 重启apache服务器命令   
> `sudo apachectl restart`    

# mac配置apache服务器    
1. 先启动一下apache服务器，在浏览器中输入`http://localhost`,应该出现`It works`提示     
2. 在home目录下建立一个`Sites`的文件夹
3. 将目录切换到`/etc/apache2`下   
4. 找到`httpd.conf`文件，将文件拷贝一个副本    
5. 更改`httpd.conf`文件    
- 通过查找`DocumentRoot`关键字，将`DocumentRoot`设置为刚刚建立的文件夹路径`/User/usr_name/Sites`    
- 通过查找`php`关键字，将`LoadModule`前面的注释去掉  
- 通过查找`Options`关键字，在`Options FollowSymLinks`中间加上`Indexes`     
- 保存退出     
6. 在刚刚建立的`Sites`文件夹中建立一个php文件,在浏览器中输入`http://localhost`进行测试     
```  
<?php phpinfo();?>  
```  

# apache服务器配置cgi     
1. 在`Sites`下新建目录`cgi`     
2. 修改`httpd.conf`文件    
- 添加一行`ScriptAlias /cgi-bin/ "/User/usr_name/Sites/cgi/"`    
- 取消下面的注释行    
```
AddType text/html .shtml     
AddOutputFilter INCLUDES .shtml    
```   
- 在文件最后加上下面几行    
```
LoadModule cgi_module /usr/libexec/apache2/mod_cgi.so    
AddHandler cgi-script .cgi .sh .py .pl   
<Directory "/User/usr_name/Sites/cgi/"> 
	Options ExecCGI
	AllowOverride None   
	Order deny,allow
	Allow from all
</Directory>   
```
3. 在cgi目录下，新建cgi文件(demo.py)，修改权限为755    
```
#!/usr/bin/python
# -*- coding: UTF-8 -*-

print "Content-type:text/html"
print                               # 空行，告诉服务器结束头部
print '<html>'
print '<head>'
print '<meta charset="utf-8">'
print '<title>Hello World - 我的第一个 CGI 程序！</title>'
print '</head>'
print '<body>'
print '<h2>Hello World!</h2>'
print '</body>'
print '</html>'
```
4. 在浏览器中输入`http://localhost/cgi/demo.cgi"测试   
    
