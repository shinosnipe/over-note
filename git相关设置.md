# git相关设置

## 添加用户信息

在安装git后，如果需要提交和使用github,就需要添加`name`和`email`。

```
git config --global user.name <用户名>
git config --global user.email <邮箱>
```

## git中文显示数字乱码问题

修改git的全局配置即可，如下：

```sh
git config --global core.quotepath false
git config --global gui.encoding utf-8
git config --global i18n.commitencoding utf-8
git config --global i18n.logoutputencoding utf-8
```

## git设置代理

设置代理

```sh
git config --global https.proxy <代理地址>:<端口号>
```

取消代理

```sh
git config --global --unset https.proxy
```

设置仅github代理

```sh
git config --global http.https://github.com.proxy http://<代理地址>:<端口号>
```

### ssh代理

git的ssh代理不在git内部设置，而是在ssh的配置文件里设置。

linux配置：

```sh
Host github.com
  User git
  HostName ssh.github.com
  Port 443
  # 走 HTTP 代理， ubuntu 先 apt install -y socat
  ProxyCommand socat - PROXY:127.0.0.1:%h:%p,proxyport=<端口号>
  # 走 socks5 代理（如 Shadowsocks）
  # ProxyCommand nc -v -x 127.0.0.1:<端口号> %h %p
```

windows配置：

```sh
ProxyCommand connect -S 127.0.0.1:10801 -a none %h %p

Host github.com
  User git
  Port 22
  Hostname github.com
  # 注意修改路径为你的路径
  IdentityFile "C:\Users\One\.ssh\id_rsa"
  TCPKeepAlive yes

Host ssh.github.com
  User git
  Port 443
  Hostname ssh.github.com
  # 注意修改路径为你的路径
  IdentityFile "C:\Users\One\.ssh\id_rsa"
  TCPKeepAlive yes
  ```