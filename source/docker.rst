###########################
docker
###########################

***************************
docker引擎
***************************

===========================
概述
===========================

docker引擎是一种client-server模式。

* server是后台进程dockerd
* CLI通过APIs与server交互


============================
安装
============================

* 卸载旧版本

    1. `sudo apt-get remove docker docker-engine docker.io containerd runc`

* 设置仓库
   
   .. code-block::

        apt update
        apt upgrade -y
        apt install curl vim wget gnupg apt-transport-https lsb-release ca-certificates
        wget -O /usr/share/keyrings/docker.asc https://download.docker.com/linux/debian/gpg
        echo "deb [signed-by=/usr/share/keyrings/docker.asc] https://mirrors.tuna.tsinghua.edu.cn/docker-ce/linux/debian $(lsb_release -sc) stable" > /etc/apt/sources.list.d/docker.list

   
* 安装引擎
 
    .. code-block::

        apt update
        apt-get install docker-ce docker-ce-cli containerd.io

* 验证

    `docker version`

=========================
docker compose
=========================

.. code-block:: 

    curl -L https://github.com/docker/compose/releases/latest/download/docker-compose-Linux-x86_64 > /usr/local/bin/docker-compose
    chmod +x /usr/local/bin/docker-compose    


======================
 修改 Docker 配置
======================

以下配置会增加一段自定义内网 IPv6 地址，开启容器的 IPv6 功能，以及限制日志文件大小，防止 Docker 日志塞满硬盘（泪的教训）：

.. code-block::

    cat > /etc/docker/daemon.json <<EOF
    {
        "log-driver": "json-file",
        "log-opts": {
            "max-size": "20m",
            "max-file": "3"
        },
        "ipv6": true,
        "fixed-cidr-v6": "fd00:dead:beef:c0::/80",
        "experimental":true,
        "ip6tables":true
    }
    EOF


========================
非root用户管理docker
========================

1. `sudo groupadd docker`
2. `sudo usermod -aG docker $USER`
3. `sudo systemctl enable docker.service`
4. `sudo systemctl enable containerd.service`

