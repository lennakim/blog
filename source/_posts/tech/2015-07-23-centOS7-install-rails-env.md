title: centOS7 配置 rails 环境
date: 2015-07-23 16:35:48
tags: [centOS, rails]
---

最近使用 centOS系统安装rails环境, 相较与我经常用的ubuntu, 有很多区别.

## 基本命令

`lsb_release -a` 显示系统的详细信息

```
# centOS
LSB Version:  :core-4.1-amd64:core-4.1-noarch
Distributor ID: CentOS
Description:  CentOS Linux release 7.1.1503 (Core)
Release:  7.1.1503
Codename: Core

# ubuntu
No LSB modules are available.
Distributor ID: Ubuntu
Description:  Ubuntu 14.04.1 LTS
Release:  14.04
Codename: trusty
```

`yum` 是centOS的包管理工具 , 比 ubuntu的 `apt-get` 简洁多了.

---

## 配置环境

### 添加普通用户

  `sudo adduser <username>`

  在 **ubuntu** 下是交互命令, 会一步步提示你 输入密码, 电话 地址等, 还会创建 home directory, 系统 Shell

  在 **centOS** 下, 没什么反应.

  ### 创建用户密码

  既然 centOS 没反应, 使用 `sudo passd <username>` 创建密码, 在密码存在的情况下, 可以修改密码

### 赋予普通用户 sudo 权限
  **ubuntu**
  `sudo usermod -a -G sudo <username>`

  **centOS**
  ```
  ll /etc/sudoers
  # -r--r-----

  # /etc/sudoers 在 root用户下 没有写权限

  chmod +w /etc/sudoers # 添加写权限

  sudo vim /etc/sudoers # 修改文件

  # 找到 root ALL=(ALL) ALL, 在下一行加上
  <username> ALL=(ALL) ALL

  ```

  OK, 普通用户也可以之行 sudo 命令了

### ssh登录

  ```
  mkdir  ~/.ssh

  vim ~/.ssh/authorized_keys
  # 把公钥加入到 authorized_keys 中即可
  ```

### 关闭 ssh 密码登录

  ```
  vim /etc/ssh/ssh_config

  PubkeyAuthentication yes # 去掉注释
  PasswordAuthentication no # 去掉注释, yes 改成 no
  ChallengeResponseAuthentication no #  去掉注释, yes 改成 no

  # 重启 sshd 服务
  sudo service ssh  restart # ubuntu
  sudo service sshd restart # centOS
  ```

### 安装 rails

  ```
  # 安装依赖
  sudo yum install -y git-core zlib zlib-devel gcc-c++ patch readline readline-devel libyaml-devel libffi-devel openssl-devel make bzip2 autoconf automake libtool bison curl sqlite-devel

  # 安装 rvm
  curl -L get.rvm.io | bash -s stable
  source ~/.bashrc
  source ~/.bash_profile

  # 安装 ruby
  rvm list known          # 列出已知的 ruby 版本
  rvm install 2.2.2       # 安装 ruby 版本
  rvm use 2.2.0 --default # 切换并设置默认ruby 版本

  # 安装 bundler rails
  gem install -V bundler rails

  ```

### 安装 nodejs

  `sudo yum install nodejs`

### 安装 nginx

  ```
  sudo yum install http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm
  ```

### 安装 mysql

```
sudo yum install mysql # 只安装 mysql-client

sudo yum install mysql mysql-server # 安装 mysql-client  mysql-server

sudo  yum install mysql-devel # 不安装, gem mysql2 本地编译出问题

```

PS: 在杭州好闷好热啊
