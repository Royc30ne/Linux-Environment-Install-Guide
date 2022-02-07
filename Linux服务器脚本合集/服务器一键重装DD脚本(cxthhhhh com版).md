# 服务器一键重装DD脚本(cxthhhhh.com版)

## 下载地址

```bash
wget --no-check-certificate -qO ~/Network-Reinstall-System-Modify.sh '[https://www.cxthhhhh.com/CXT-Library/Network-Reinstall-System-Modify/Network-Reinstall-System-Modify.sh](https://www.cxthhhhh.com/CXT-Library/Network-Reinstall-System-Modify/Network-Reinstall-System-Modify.sh)' && chmod a+x ~/Network-Reinstall-System-Modify.sh
```

## 裸机部署平台

```bash
bash ~/Network-Reinstall-System-Modify.sh -CXT_Bare-metal_System_Deployment_Platform
```

## 默认账号密码

### Windows

**用户名:** Administrator

**密码:** cxthhhhh.com

### Linux:

**用户名:** root

**密码:** cxthhhhh.com

## 推荐系统镜像：

### Windows:

```bash
bash ~/Network-Reinstall-System-Modify.sh -Windows_Server_2019
```

### Linux:

```bash
#Debian 10
bash ~/Network-Reinstall-System-Modify.sh -Debian_10

#Centos 8
bash ~/Network-Reinstall-System-Modify.sh -CentOS_8

#Ubuntu 20.04
bash ~/Network-Reinstall-System-Modify.sh -Ubuntu_20.04
```

### 自定义镜像:

```bash
bash ~/Network-Reinstall-System-Modify.sh  -DD "%URL%"
```