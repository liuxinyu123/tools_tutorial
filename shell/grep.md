# grep操作   
- grep "aa"  file   file文件中包含aa的行   
- grep -c "aa" file   file文件中包含aa的有多少行   
- grep -n "aa" file  file文件中包含aa的是第几行  
- grep -i "aa" file  file文件中包含aa的行(忽略大小写)   
- grep -v "aa" file   file文件中不包含aa的行   
- grep -E "^aa" file  file文件中以aa开头的行   
- grep -E "aa$" file  file文件中以aa结尾的行   
- grep -E ".+aa.+" file   file文件中aa在中间的行   
- grep -E "^$" file   file文件中是空行的行  
- grep -E "[0-9]+\.[0-9]+\.[0-9]+\.[0-9]+" file  查找ip地址   

 
