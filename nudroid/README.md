sudo apt-get update

sudo apt-get install git maven openjdk-6-jdk libstdc++6:i386
sudo apt-get install lib32z1  

wget http://dl.google.com/android/android-sdk_r24.4.1-linux.tgz

tar zxf android-sdk_r24.4.1-linux.tgz 

#建议 添加android_home环境变量到 .bashrc文件，用nano 打开 .bashrc文件把 export ANDROID_HOME=/home/sherlock/android-sdk-linux 放到文件尾部
export ANDROID_HOME=/home/sherlock/android-sdk-linux

cd /home/sherlock/android-sdk-linux

# make sure tools are at the newest version
#执行完这条命令会缺build-tools 主要是最新版本build_tools的Dex不兼容jdk1.6  tools/android update sdk --no-ui --force --filter tools

#更新sdk
build-tools tools/android update sdk --no-ui --force --filter tools

#手动下载 稳定版本的build-tools
wget https://dl-ssl.google.com/android/repository/build-tools_r23.0.2-linux.zip
mkdir /home/sherlock/android-sdk-linux/build-tools
mv build-tools_r23.0.2-linux.zip /home/sherlock/android-sdk-linux/build-tools
cd /home/sherlock/android-sdk-linux/build-tools
unzip build-tools_r23.0.2-linux.zip 


# fetch required android dependencies
tools/android update sdk --no-ui --force --filter build-tools-20.0.0,android-10,android-16,extra-android-m2repository

#确认两次 “ Y ” 同意开源协议 开始30分钟的下载依赖库，api16,api10,Maven库。

#返回根目录
cd ~

# first time only
#克隆代码
git clone https://github.com/Cybnate/NuBitsj.git

#变小写
mv NuBitsj nubitsj

#编译
mvn  package -D maven.javadoc.skip=true 

#安装入.m2目录为后续nudroid编译服务
mvn install -D  maven.javadoc.skip=true 

#克隆代码
git clone https://github.com/Cybnate/NuDroid.git

#变小写
mv NuDroid nudroid

#编译
mvn  package -D maven.javadoc.skip=true 
