# linux设置相关

## ubuntu中文语言环境

在docker里使用ubuntu设置中文locale时可能会不存在`/etc/locale.gen`，需要安装字符集：

```sh
apt install language-pack-zh-hans
```

## systemd设置开机启动

- 系统目录结构：
    - /etc/systemd/system/：用户自定义的系统级别的unit文件目录。
    - /usr/lib/systemd/system/：软件包提供的系统级别的unit文件目录。
- 单位文件：
    - .service：定义一个服务。
    - .target：定义一个运行级别，指定了要启动的一组服务。

要在Arch Linux中创建一个新的启动项，您需要创建一个新的systemd服务，具体步骤如下：

1. 在/etc/systemd/system/目录下创建一个新的Unit文件，比如your_service.service：

    ```
    sudo touch /etc/systemd/system/your_service.service
    ```

2. 打开该文件并添加以下内容：

    ```bash
    [Unit]
    Description=Your Service
    After=network.target

    [Service]
    ExecStart=/usr/bin/your_service
    Restart=always

    [Install]
    WantedBy=multi-user.target
    ```

    其中，`Description`是描述该服务的信息，`After`表示该服务在network.target之后启动，`ExecStart`指定要运行的命令，`Restart`表示该服务在异常退出时重启，`WantedBy`指定该服务会被加入到哪个target中。

3. 启动与设置开机启动服务

    ```sh
    # 启动服务
    systemctl start your_service.service
    # 设置开机启动
    systemctl enable your_service.service
    ```