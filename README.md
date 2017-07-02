# build-spark2.1-with-jupyter-4.3-on-ubuntu16.04
build spark2.1 with jupyter 4.3 on ubuntu16.04

记录花费两天时间搭建的spark学习环境

## 在vmware上安装ubuntu16.04 
1.典型安装时,可以跳过下载语言包的步骤,等进入系统了,更改镜像为阿里云,安装过程会快一倍以上;  
2.步骤1完成后,需要安装vmware tools ,本来他自己会自动安装的,  
有时候发现还是不能拖拉文件复制,那么就多重启几遍 , 然后多拖拉几遍 , 然后就行了;

## 安装jdk-1.8 , anaconda3-4.3 , spark-2.1
### 安装好后记得配置全局环境变量
编辑 /etc/profile , 最后加入以下(路径得自己调整,software是我自己建的目录):  

    #added jdk env
    export JAVA_HOME=/home/lancelot/Software/jdk
    export PATH=$JAVA_HOME/bin:$PATH 
    export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar 

    #added spark env
    export SPARK_HOME=/home/lancelot/Software/spark
    export PATH=$PATH:/home/lancelot/Software/spark/bin

    #added Anaconda3 env
    export PATH="/home/lancelot/Software/anaconda3/bin:$PATH"

## 安装toree  
toree是连接spark与jupyter的一个中间人,是本文的重要所在;  
由于pypi上的是toree0.1.0版本,只支持spark1.6,所以这里不直接pip install了;  
去toree的git上,最后会说明这个问题,好好阅读他的readme.md文档很重要,特别是最后Version部分;
然后还是pip大法好:  

    pip install https://dist.apache.org/repos/dist/dev/incubator/toree/0.2.0/snapshots/dev1/toree-pip/toree-0.2.0.dev1.tar.gz
    
## 安装kernels
各个参数google说明,需要特别提醒的是--user的设置,不加上这个就需要root权限,因为kenerls会安装到系统全局环境下,加上了只安装在当前用户环境下;

    jupyter toree install --kernel_name=Toree --spark_home=$SPARK_HOME --interpreter=PySpark,Scala,SQL --user

## 安装nbextentions;
只有安装了插件,才是完整的notebook,使用起来更舒服;
这里要想快,可以用客户机通过宿主机翻墙上网,详情google;  
需要注意的是,就算是宿主机翻墙了,客户机的firefox和terminal也还要分别折腾,  
比如terminal访问网络都是用http/https的,所以需要转换shadowsocks的socks5代理;  
工具: firefox用Pan插件 ; terminnal用privoxy,proxychain等;  
最好是在宿主机上用下载工具下载sh文件或者tar文件或者whl文件,拉到客户机上安装;


可以愉快地开始spark了;

