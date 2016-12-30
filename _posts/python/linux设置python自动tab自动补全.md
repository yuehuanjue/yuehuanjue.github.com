# Linux设置python自动tab自动补全

来源：http://blog.csdn.net/apache0554/article/details/44830003


## 1.安装readline模块。

指令： sudo apt-get install readline*  

## 2.创建文件~/.pythonstartup,内容如下

```
# python startup file  
import sys  
import readline  
import rlcompleter  
import atexit  
import os  
# tab completion  
readline.parse_and_bind('tab: complete')  
# history file  
histfile = os.path.join(os.environ['HOME'], '.pythonhistory')  
try:  
    readline.read_history_file(histfile)  
except IOError:  
    pass  
atexit.register(readline.write_history_file, histfile)  

  
del os, histfile, readline, rlcompleter   
```

## 3.在~/.bash_profile中添加环境变量
```
export PYTHONSTARTUP=~/.pythonstartup  
```
## 4.刷新配置

source .bash_profile