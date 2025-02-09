---
title: ubuntu安装rabbitMQ
date: 2025-02-09 16:54:51
tags:
  - ubuntu
  - rabbitMQ
categories:
  - 服务器部署
---

> ubuntu安装rabbitMQ

<!-- more -->

### 安装RabbitMQ

#### 更新软件包列表
首先，确保系统包列表是最新的
```shell
sudo apt update
```

#### 安装 Erlang（RabbitMQ 的依赖项）
RabbitMQ 是使用 Erlang 编写的，因此需要安装 Erlang
```shell
sudo apt install erlang
```

#### 添加 RabbitMQ 仓库
```shell
echo "deb https://dl.bintray.com/rabbitmq/debian bionic main" | sudo tee /etc/apt/sources.list.d/bintray.rabbitmq.list
```

添加 RabbitMQ 公钥  
```shell
wget -O- https://www.rabbitmq.com/rabbitmq-release-signing-key.asc | sudo apt-key add -
```
再次更新软件包列表  
```shell
sudo apt update
```
#### 安装 RabbitMQ
使用以下命令安装 RabbitMQ  
```shell
sudo apt install rabbitmq-server
```

#### 启用并启动 RabbitMQ 服务
启用 RabbitMQ 服务并在系统启动时启动它  
```shell
sudo systemctl enable rabbitmq-server
sudo systemctl start rabbitmq-server
```

#### 检查 RabbitMQ 的状态  
```shell
sudo systemctl status rabbitmq-server
```
通过以上步骤，您将在 Ubuntu 系统上安装并运行 RabbitMQ。