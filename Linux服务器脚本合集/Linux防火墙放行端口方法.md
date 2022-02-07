# Linux防火墙放行端口方法

# CentOS

```bash
firewall-cmd --zone=public --add-port=9091/tcp --permanent

--zone                #作用域
--add-port=80/tcp     #添加端口，格式：端口/通讯协议
--permanent           #使操作永久生效，没有此参数重启后失效
```

# Debian/Ubuntu

## 安装iptables（若系统未预装）

```bash
apt-get update
apt-get install iptables
apt-get install iptables-persistent
```

## 放行端口

```bash
iptables -I INPUT -p tcp --dport 9091 -j ACCEPT
#保存规则（重启后失效）
iptables-save
#保存规则（重启后仍然生效）
netfilter-persistent save
netfilter-persistent reload
```

## 查看当前防火墙规则

```bash
iptables -L
```