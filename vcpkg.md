# VCPKG相关
目前，C++工程的第三方库全部使用vcpkg.json进行管理。    

## Windows
需要提前安装vs2022, cmake, vcpkg。    

### 现有工程使用
1.设置vcpkg环境变量：    
CMAKE_TOOLCHAIN_FILE C:\dev\vcpkg\scripts\buildsystems\vcpkg.cmake (视vcpkg目录不同自行修改)

在工程目录下，直接执行：    
cmake . -B build    
vcpkg会根据vcpkg.json中的内容自动下载对应的包，并引用相关头文件。    


## Linux
### 环境准备
CentOS7因为环境比较老旧，需要先安装运行环境：
```
yum update  
yum install centos-release-scl  
yum install devtoolset-7  
scl enable devtoolset-7 bash  
```    
1. 安装cmake(版本：3.25+)  
2. 安装vcpkg（本例安装在：/root/vcpkg目录下，其他目录需要修改cmake指令） 
3. 设置环境变量：    
```CMAKE_TOOLCHAIN_FILE /root/vcpkg/scripts/buildsystems/vcpkg.cmake```

或者，不设置环境变量，也可以通过参数指定：    
```cmake -B build -S . "-DCMAKE_TOOLCHAIN_FILE=/root/vcpkg/scripts/buildsystems/vcpkg.cmake"  ```    
其他用户:    
```cmake -B build -S . "-DCMAKE_TOOLCHAIN_FILE=/home/cloudforce/vcpkg/scripts/buildsystems/vcpkg.cmake"  ````    
4. 在工程目录下执行：    
```cmake . -B build```    
    
5. 进入build目录，运行：    
make编译工程    

## 工程配置
在需要引入C++的第三方库时，可以使用vcpkg search 库名，查询是否有对应的库。

vcpkg.json文件格式：    
```
{
  "name": "app-name",
  "version": "1.0.0",
  "dependencies": [
    "boost-filesystem",
    "boost-json",
    "boost-log",
    "boost-beast",
    "boost-thread",
    "sqlite3",
    "openssl"
  ]
}
```

指定引用库的版本：
```
{
  "name": "app-name",
  "version": "1.0.0",
  "dependencies": [
    "boost-filesystem",
    "boost-json",
    "boost-log",
    "boost-beast",
    "boost-thread",
    "sqlite3",
    "openssl"
  ],
  "overrides": [
    {"name": "openssl", "version-string": "1.1.1n"},
    {"name": "boost-filesystem", "version": "1.81.0"},
    {"name": "boost-json", "version": "1.81.0"},
    {"name": "boost-log", "version": "1.81.0"},
    {"name": "boost-beast", "version": "1.81.0"},
    {"name": "boost-thread", "version": "1.81.0"},
  ],
  "builtin-baseline": "cfaeb75bb67fee375b517a2f85d8f93f2b46bdb4"
}
```






