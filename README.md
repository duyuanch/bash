# 终端设置

## 设置终端走代理

``` bash
export http_proxy="127.0.0.1:7890"
export https_proxy="127.0.0.1:7890"
```

# curl 网络传输工具

## 查看网页内容

``` bash
curl https://www.baidu.com
```

## 显示版本号

``` bash
curl -V
```

## 显示详细请求过程

``` bash
curl -v https://www.baidu.com
```



# git 版本控制工具

## 查看全局配置

``` bash
git config --global --list
```

## 设置代理

```bash
git config --global http.proxy socks5://127.0.0.1:1080
git config --global https.proxy socks5://127.0.0.1:1080
```

## 取消代理

``` bash
git config --global --unset http.proxy
git config --global --unset https.proxy
```



# 进程管理

## 

## kill 终止进程

``` bash
kill 142 # 终止PID为142的进程
kill 142 157 # 终止PID为142 157的进程
```



## Mac 终止进程

``` bash
lsof -n -i4TCP:8080 
kill PID
```

# Shadowsocks 代理

## 安装 Shadowsocks 代理

``` bash
yum install python3
pip3 install https://github.com/shadowsocks/shadowsocks/archive/master.zip -U # 安装python版本ss
ssserver -m aes-256-cfb -p 15251 -k abc@123 # 前台运行
sed -i 's/cleanup/reset/' /usr/local/lib/python3.6/site-packages/shadowsocks/crypto/openssl.py # 如果报错执行
screen -S ss -dm ssserver -m aes-256-cfb -p 15251 -k abc@123 # 后台运行
```



## libsodium加密安装

``` bash
yum -y groupinstall "Development Tools" # 安装依赖库文
wget https://download.libsodium.org/libsodium/releases/LATEST.tar.gz # 下载源文件
tar zxvf LATEST.tar.gz # 解压
cd libsodium-stable/ # 进入源代码目录
./configure && make -j4 && make install # 编译安装
echo /usr/local/lib > /etc/ld.so.conf.d/usr_local_lib.conf # 最终配置
ldconfig
```



# SSH远程登录

## 允许以root的方式登录

``` bash
vim /etc/ssh/sshd_config
# 修改如下
PermitRootLogin yes           #允许root认证登录 
PasswordAuthentication yes   #允许密码认证
service sshd restart # 重启SSH服务
```

## 私密形式登录

``` bash
chmod 400 private.key
ssh -i private.key username@ip_address
```



# BBR加速器

## 开启Centos 8+自带BBR

``` bash
# 添加并启用Google BBR模块到内核
echo "net.core.default_qdisc=fq" >> /etc/sysctl.conf
echo "net.ipv4.tcp_congestion_control=bbr" >> /etc/sysctl.conf
sysctl -p

sysctl net.ipv4.tcp_available_congestion_control # 可选
lsmod | grep bbr # 验证是否启用了Google BBR
```



# 文件操作

## 按照文件名查找文件

``` bash
find / -name 'filename' # 在根目录及子目录中查找文件
```



