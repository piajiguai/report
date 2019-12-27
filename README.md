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
make             //由于磁盘空间不够，安装失败，于是查阅网络扩充了根目录的磁盘空间再重新编译。 

yum make install 
cd /usr/local/nebula

//配置文件
sudo cp etc/nebula-graphd.conf.default etc/nebula-graphd.conf
sudo cp etc/nebula-metad.conf.default etc/nebula-metad.conf
sudo cp etc/nebula-storaged.conf.default etc/nebula-storaged.conf
```

### 9.启动nebula
```
sudo ./scripts/nebula.service start all
sudo ./bin/nebula -u user -p password --port 3699 --addr "127.0.0.1"
```

### (前期工作宣告完成)
### 以下对在console上返回的耗时单位(us)进行调整:当耗时大于1000us时，将其转换为ms。

对路径nebula/src/console中的CmdProcessor.cpp进行修改 

![](https://github.com/piajiguai/report/blob/master/p7.png)

![](https://github.com/piajiguai/report/blob/master/p8.png)

以下是源码：
```cpp
if (res == cpp2::ErrorCode::SUCCEEDED) {
    // Succeeded
    auto *spaceName = resp.get_space_name();
    if (spaceName && !spaceName->empty()) {
        curSpaceName_ = std::move(*spaceName);
    } else {
        curSpaceName_ = "(none)";
    }
    if (resp.get_rows() && !resp.get_rows()->empty()) {
        printResult(resp);
        std::cout << "Got " << resp.get_rows()->size()
                  << " rows (Time spent: "
                  << resp.get_latency_in_us() << "/"
                  << dur.elapsedInUSec() << " us)\n";
    } else if (resp.get_rows()) {
        std::cout << "Empty set (Time spent: "
                  << resp.get_latency_in_us() << "/"
                  << dur.elapsedInUSec() << " us)\n";
    } else {
        std::cout << "Execution succeeded (Time spent: "
                  << resp.get_latency_in_us() << "/"
                  << dur.elapsedInUSec() << " us)\n";
    }
    std::cout << std::endl;
}
```

以下是修改后的代码：
```cpp
if (res == cpp2::ErrorCode::SUCCEEDED) {
    // Succeeded
    auto *spaceName = resp.get_space_name();
    if (spaceName && !spaceName->empty()) {
        curSpaceName_ = std::move(*spaceName);
    } else {
        curSpaceName_ = "(none)";
    }
if (resp.get_rows() && !resp.get_rows()->empty()) {
    printResult(resp);
    std::cout << "Got " << resp.get_rows()->size()
              << " rows (Time spent: ";
} else if (resp.get_rows()) {
    std::cout << "Empty set (Time spent: ";
} else {
    std::cout << "Execution succeeded (Time spent: ";
}
if (resp.get_latency_in_us() < 1000 || dur.elapsedInUSec() < 1000) {
    std::cout << resp.get_latency_in_us() << "/"
              << dur.elapsedInUSec() << " us)\n";
} else {
    std::cout << resp.get_latency_in_us() / 1000.0 << "/"
              << dur.elapsedInUSec() / 1000.0 << " ms)\n";
} 
std::cout << std::endl;
}
```


### 重新编译并将代码上传至github






