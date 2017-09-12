# find的用法  
- find . -name "*.txt"  在当前目录查找.txt后缀的文件    
- find . -perm 755   在当前目录下查找权限是755的文件   
- find . -user root  在当前目录下查找用户为root的文件
- find . -mtime -5   在当前目录下查找更改时间5天以内的文件
- find . -mtime +3  在当前目录下查找更改时间3天以前的文件   
- find . -type d   在当前目录下查找文件类型是目录的文件 l(链接) f(文件)   
- find . -size +1000c  在当前目录下查找文件大小大于1k的文件   
- find . -perm 700 | xargs chmod 777  xargs 相当于前面的结果   

   

