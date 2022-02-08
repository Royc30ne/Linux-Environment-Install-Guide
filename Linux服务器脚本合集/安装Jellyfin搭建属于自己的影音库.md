# 安装Jellyfin搭建属于自己的影音库

# 安装解码依赖ffmeg

## 安装yasm供编译安装ffmeg使用

```bash
wget http://www.tortall.net/projects/yasm/releases/yasm-1.3.0.tar.gz
tar -zxvf yasm-1.3.0.tar.gz
cd yasm-1.3.0
./configure
make && make install
```

## 编译安装ffmpeg

### 下载并解压缩

```bash
wget http://www.ffmpeg.org/releases/ffmpeg-3.1.tar.gz
tar -zxvf ffmpeg-3.1.tar.gz
```

### 进入解压后目录,这里指定/usr/local/ffmpeg为安装目录

```bash
cd ffmpeg-3.1
./configure --prefix=/usr/local/ffmpeg
make && make install
```

### 添加环境变量

```bash
vi /etc/profile
#在最后一行添加
export PATH=$PATH:/usr/local/ffmpeg/bin
#：wq保存并退出
source /etc/profile
```

### 查看是否生效

```bash
ffmpeg -version

ffmpeg version 3.1 Copyright (c) 2000-2016 the FFmpeg developers
built with gcc 8 (Debian 8.3.0-6)
configuration: --prefix=/usr/local/ffmpeg
libavutil      55. 27.100 / 55. 27.100
libavcodec     57. 48.101 / 57. 48.101
libavformat    57. 40.101 / 57. 40.101
libavdevice    57.  0.101 / 57.  0.101
libavfilter     6. 46.102 /  6. 46.102
libswscale      4.  1.100 /  4.  1.100
libswresample   2.  1.100 /  2.  1.100
```

# 安装Jellyfin

## 下载

```bash
#Debian
wget -O - https://repo.jellyfin.org/debian/jellyfin_team.gpg.key | apt-key add -
#Ubuntu
wget -O - https://repo.jellyfin.org/ubuntu/jellyfin_team.gpg.key | sudo apt-key add -
```

## 配置存储库

```bash
#Debian
echo "deb https://repo.jellyfin.org/debian <release> main" | tee /etc/apt/sources.list.d/jellyfin.list
#Ubuntu
echo "deb https://repo.jellyfin.org/ubuntu <release> main" | sudo tee /etc/apt/sources.list.d/jellyfin.list

#<release>中根据系统版本替换
Debian 8:     jessie
Debian 9:     stretch
Debian 10:    buster
Ubuntu 14:    trusty
Ubuntu 16:    xenial
Ubuntu 18.04: bionic
Ubuntu 18.10: cosmic
```

## 安装Jellyfin

```bash
#更新存储库
apt update
#安装依赖
apt install apt-transport-https -y
#安装jellyfin
apt install jellyfin -y

#启动jellyfin
systemctl start jellyfin
#停止jellyfin
systemctl stop jellyfin
#重启jellyfin
systemctl start jellyfin
#开机自启jellyfin
systemctl enable jellyfin
#取消自启jellyfin
systemctl disable jellyfin
```

防火墙中放行8096端口，具体放行方法可见前文

完成后通过ip:8096访问Jellyfin网页自行进行相关媒体库配置