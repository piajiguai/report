# c++期末大作业报告
姓名：蒋袁旭
学号18071116

## 简述 
这次作业的主要内容是nebula进行测试，并且利用git提交到github上。 

## 步骤 
1.安装git
```
yum install git 
```
![](https://github.com/piajiguai/report/blob/master/p1.png)

2.对git进行环境配置
```
git config --global user.name "piajiguai"
git config --global user.email "502833539@qq.com"
```
![](https://github.com/piajiguai/report/blob/master/p2.png)

3.用SSH生成密钥：
```
ssh-keygen -t rsa -C "502833539@qq.com""
```
![](https://github.com/piajiguai/report/blob/master/p3.png)
 
3.添加 私密钥 到ssh：ssh-add id_rsa
 
4.在github上添加ssh密钥
![](https://github.com/piajiguai/report/blob/master/p4.png)

5.git连接github
```
ssh -T git@github.com
```
![](https://github.com/piajiguai/report/blob/master/p5.png)

6.把已经fork的nebula拷贝到本地
```
git clone https://github.com/piajiguai/nebula.git
```
![](https://github.com/piajiguai/report/blob/master/p6.png)


