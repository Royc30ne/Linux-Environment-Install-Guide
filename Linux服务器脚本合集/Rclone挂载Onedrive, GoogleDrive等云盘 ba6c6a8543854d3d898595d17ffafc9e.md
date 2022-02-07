# Rclone挂载Onedrive, GoogleDrive等云盘

## 安装rclone依赖fuse

```bash
# Debian/Ubantu
apt-get update && apt-get install -y fuse

# CentOS
yum install -y fuse
```

## 安装rclone

### · 脚本安装rclone

```bash
#Linux/macOs/BSD
curl https://rclone.org/install.sh | sudo bash

#beta版本
curl https://rclone.org/install.sh | sudo bash -s beta
```

### · 编译安装rclone

```bash
#下载解压文件
curl -O https://downloads.rclone.org/rclone-current-linux-amd64.zip
unzip rclone-current-linux-amd64.zip
cd rclone-*-linux-amd64

#复制二进制文件
sudo cp rclone /usr/bin/
sudo chown root:root /usr/bin/rclone
sudo chmod 755 /usr/bin/rclone

#安装manpage
sudo mkdir -p /usr/local/share/man/man1
sudo cp rclone.1 /usr/local/share/man/man1/
sudo mandb
```

## 设置rclone配置文件

```bash
./rclone config
```

## 挂载指令

```bash
./rclone mount "添加时云盘名称":"云盘指定目录" "挂载至本地的目录" [--添加参数]
```

```bash
--allow-other：允许非当前 rclone 用户外其它用户进行访问
--attr-timeout 5m：文件属性缓存，（大小，修改时间等）的时间。如果 VPS 配置比较低，建议适当提高这个值，避免过多内核交互，降低资源占用。
--vfs-cache-mode full：开启 VFS 文件缓存，可减少 rclone 与 API 交互，同时可提高文件读写效率
--vfs-cache-max-age 24h：VFS 文件缓存时间，这里设置 24 小时，如果文件很少更改，建议设置更长时间
--vfs-cache-max-size 10G：VFS文件缓存上限大小，请根据服务器剩余磁盘自行调节
--vfs-read-chunk-size-limit 100M：分块读取大小，这里设置的是100M，可提高文件读的效率，比如1G的文件，大致分为10个块进行读取，但与此同时API请求次数也会增多
--buffer-size 100M：设置内存缓存，请根据服务器内存大小自行设置
--daemon：后台运行程序
```

### 案例

```bash
./rclone mount GoogleDrive:GoIndex /www/wwwroot/drive --copy-links --allow-other --allow-non-empty --umask 000 --attr-timeout 5m --vfs-cache-mode full --vfs-cache-max-age 3h --vfs-cache-max-size 30G --buffer-size 300M --daemon
```

## 设置开机自动挂载

### 新建rclone.service文件

```bash
vim /usr/lib/systemd/system/rclone.service
```

### 写入内容

```bash
[Unit]
Description = rclone
    
[Service]
User = root
ExecStart = "此处自行填写挂载指令"
Restart = on-abort
    
[Install]
WantedBy = multi-user.target

#：wq 保存并退出
```

```bash
#重载daemon
systemctl daemon-reload

#启动rclone
systemctl start rclone

#设置开机启动
systemctl enable rclone

#停止rclone
systemctl stop rclone

#查看rclone运行状态
systemctl status rclone

#查看挂载状况
df -h

#取消挂载
fusermount -qzu /GoogleDrive
```