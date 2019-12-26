# c++期末大作业报告
姓名：蒋袁旭 
学号：18071116

## 简述 
这次作业的主要内容是nebula进行测试，并且利用git提交到github上。 

## 步骤 
### 1.安装git
```
yum install git 
```
![](https://github.com/piajiguai/report/blob/master/p1.png)

### 2.对git进行环境配置
```
git config --global user.name "piajiguai"
git config --global user.email "502833539@qq.com"
```
![](https://github.com/piajiguai/report/blob/master/p2.png)

### 3.用SSH生成密钥：
```
ssh-keygen -t rsa -C "502833539@qq.com""
```
![](https://github.com/piajiguai/report/blob/master/p3.png)
 
### 4.添加 私密钥 到ssh：ssh-add id_rsa
 
### 5.在github上添加ssh密钥
![](https://github.com/piajiguai/report/blob/master/p4.png)

### 6.git连接github
```
ssh -T git@github.com
```
![](https://github.com/piajiguai/report/blob/master/p5.png)

### 7.把已经fork的nebula拷贝到本地
```
git clone https://github.com/piajiguai/nebula.git
```
![](https://github.com/piajiguai/report/blob/master/p6.png)

### 8.配置nebula
```
cd nebula
./build_dep.sh
source ~/.zshrc  //如果是bash，则为source ~/.bashrc,这里试了好久才发现...
mkdir build
cd build

cmake ..
make             //由于磁盘空间不够，安装失败，于是查阅网络扩充了根目录的磁盘空间再重新操作。

yum make install
cd /usr/local/nebula
cp etc/nebula-graphd.conf.default etc/nebula-graphd.conf
cp etc/nebula-metad.conf.default etc/nebula-metad.conf
cp etc/nebula-storaged.conf.default etc/nebula-storaged.conf
```

### 9.启动nebula
```
./scripts/nebula.service start all
./bin/nebula -u user -p password --port 3699 --addr "127.0.0.1"
```
![]()

### (前期工作宣告完成)
### 以下对在console上返回的耗时单位进行配置






