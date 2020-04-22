# 环境搭建

### WEB（PHP）

* 运行环境
  * PHP Study（某些版本中存在后门，不推荐使用。（[PHPStudy 后门分析](https://paper.seebug.org/1044/)））
  * PHP
  * MySQL
  * Apache/Nginx
* 代码阅读
  * VSCode
  * Sublime
  * Atom
  * Vim
* 调试
  * xdebug
  * pdb
  * gdb

### 类 Unix 环境（Ubuntu Linux）

* 系统环境
  * 双系统
  * 虚拟机
    * Virtual Box
    * VMWare
* 工具
  * Docker
  * Docker-Compose

### 其他工具

* Python
* Chrome/Firefox
* BurpSuite



Ubuntu 环境搭建

```text
# switch to root user
sudo su

# update source
wget https://mirrors.ustc.edu.cn/repogen/conf/ubuntu-https-4-bionic -O /etc/apt/source.list

# upgrade
apt update && apt upgrade -y && apt dist-upgrade -y && apt clean -y && apt autoclean -y && apt remove -y && apt autoremve -y

# devops
apt install \
    openssh-server \
    vim \
    zsh \
    tmux \
    curl \
    unar \
    lrzsz \
    python \
    python-pip \
    python3 \
    python3-pip

# build
apt install \
    build-essential \
    gdb

# docker
apt install \
    docker.io \
    docker-compose

# scanner
apt install \
    nmap \
    masscan \
    zmap

# oh my zsh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

