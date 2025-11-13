---
layout:     post   				    # 使用的布局（不需要改）
title:      SSH + VS Code远程连接：从账号密码到免密登录的攻略			 
subtitle:   vscode免密登录 #副标题
date:       2025-11-13				# 时间
author:     wuxia						# 作者
header-img: img/post-bg-2015.jpg	#这篇文章标题背景图片
catalog: true 						# 是否归档
tags:								#标签

  - vscode
  - ssh
---

一、账号密码登录服务器
以下是通过 SSH 使用账号密码登录到远程 Linux 服务器的详细步骤。

1. 打开终端
Windows 用户：你可以使用 PowerShell、cmd 或者 Git Bash。如果需要使用 Bash，可以安装 Git for Windows 或者启用 Windows Subsystem for Linux（WSL）。
Linux/Mac 用户：直接打开终端（Terminal）。
2. 输入 SSH 命令
  在终端中输入 ssh 命令来连接到远程服务器。一般格式如下：

  ```
  ssh -p 端口号 root@xxxx.com
  ```

  `ssh`：表示通过 SSH 协议登录远程服务器。

  `-p 端口号`：指定服务器的 SSH 端口号（默认是 22，如果服务器使用的是自定义端口号，需要指定正确的端口）。

  `root`：登录到服务器的用户名（例如：`root`、`user1` 等）。

  `xxxx.com`：服务器的 IP 地址或域名。

#### 3. 输入密码并登录

运行命令后，系统会提示你输入登录密码。直接在终端中输入服务器的密码并回车：

```
root@xxxx.com's password:
```

输入密码时，密码不会显示在屏幕上（出于安全性考虑），但仍然会记录输入。按下回车后，服务器验证密码是否正确。

##### 登录成功后的输出

如果密码正确，你会看到类似以下的输出，表示你已经成功登录到远程服务器：

```
Last login: Sun Sep 22 14:33:27 2024 from 192.168.x.x
[root@server ~]# 
```

#### 可能的提示和错误

**首次登录提示**： 如果是首次登录到该服务器，你会看到类似如下的提示，表示 SSH 客户端无法确认服务器的身份：

```
The authenticity of host 'xxxx.xxx.xxxxx.com (xx.xx.xx.xx)' can't be established.
RSA key fingerprint is SHA256:xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx.
Are you sure you want to continue connecting (yes/no)?
```

输入 `yes` 并回车，系统会将服务器的指纹保存到本地 `~/.ssh/known_hosts` 文件中。

二、免密登录服务器
1. 创建 SSH 密钥的公钥和私钥
首先，需要在本地生成一对 SSH 密钥。公钥将被放置在远程服务器上，而私钥保存在本地，用于认证登录。

1.1 生成 SSH 密钥对
打开命令行终端（Windows 用户可以使用 Git Bash、PowerShell 或 Windows Subsystem for Linux，Linux/Mac 用户使用终端），运行以下命令来生成 RSA 密钥对：

```
ssh-keygen -t rsa -C "your_email@example.com"
```

- `-t rsa`：指定生成 RSA 类型的密钥对。
- `-C "your_email@example.com"`：为密钥添加注释，通常是你的邮箱地址，方便识别。

##### 1.2 输入密钥存储位置

系统会提示你选择存储私钥的位置。默认存储在 `~/.ssh/id_rsa`，直接按 **Enter** 使用默认路径：

```
Generating public/private rsa key pair.
Enter file in which to save the key (/home/your_user/.ssh/id_rsa):
```

##### 1.3 设置密码（可选）

系统会询问你是否为私钥设置密码短语，可以选择设置以增加安全性。如果不需要，直接按 **Enter** 跳过：

```
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
```

完成后，你会在终端看到类似以下的输出，表示密钥已经成功生成：

```
Your identification has been saved in /home/your_user/.ssh/id_rsa.
Your public key has been saved in /home/your_user/.ssh/id_rsa.pub.
```

现在你有了一个私钥文件 id_rsa 和一个公钥文件 id_rsa.pub。

2. 发送公钥到远程服务器
将生成的公钥文件发送到远程服务器的 ~/.ssh/authorized_keys 文件中，允许你通过私钥登录远程服务器。

2.1 使用 ssh-copy-id 将公钥传到服务器
执行以下命令，将你的公钥复制到服务器（-p 参数指定端口号，默认为 22）：

```
ssh-copy-id -p 22 root@xxxx.com
```

##### 2.2 过程说明

首次运行 `ssh-copy-id` 时，需要输入服务器的密码来完成公钥的传输：

```
root@xxxx.com's password:
```

输入密码后，`ssh-copy-id` 会将公钥上传到服务器的 `~/.ssh/authorized_keys` 文件中。如果成功，你会看到类似以下输出：

```
Number of key(s) added: 1

Now try logging into the machine, with:   "ssh -p 12803 root@xxxx.com"
and check to make sure that only the key(s) you wanted were added.
```

#### 3. 验证无密码登录

你现在应该能够通过 SSH 无需密码直接登录到远程服务器。使用以下命令登录：

```
ssh -p 12803 root@xxxx.com
```

如果一切正常，你将无需输入密码，直接登录到远程服务器。

------

#### 4. 手动上传公钥（如果 `ssh-copy-id` 不可用）

如果 `ssh-copy-id` 命令不可用，你可以手动将公钥复制到服务器。

##### 4.1 显示本地公钥内容

首先，查看你的公钥内容：

```
cat ~/.ssh/id_rsa.pub
```

将输出的内容复制下来。

##### 4.2 连接服务器并手动粘贴公钥

登录到远程服务器，并将公钥粘贴到 `~/.ssh/authorized_keys` 文件中：

```
ssh -p 12803 root@xxxx.com
```

进入服务器后，执行以下命令：

```
mkdir -p ~/.ssh
echo "your_public_key_contents" >> ~/.ssh/authorized_keys
chmod 600 ~/.ssh/authorized_keys
chmod 700 ~/.ssh
```

替换 `your_public_key_contents` 为你复制的公钥内容。这样公钥也会正确添加到服务器上。

### 三、vscode免密登录服务器

#### 1. 安装 Remote-SSH 插件

在 VS Code 中安装 **Remote-SSH** 插件

![img](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/caa54db415af4cdcb4d5703e776982c1.png)

2. 添加 SSH 配置
在 Remote-SSH 插件中，添加新的 SSH 连接配置。

点击 VS Code 左侧栏中的 Remote Explorer 图标（通常是一个计算机图标），然后在顶部找到 Remote-SSH 的部分。

点击右上角的 “+” 按钮，输入完整的 SSH 命令,按回车键确认添加。
![img](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/5d8a249fea604b548ba18692f4d473ed.png)

#### 3. 选择配置文件并更新 `config` 文件

在你添加 SSH 命令后，VS Code 会询问你保存 SSH 配置的文件位置。

##### 3.1 选择 `config` 文件

选择本地用户目录的 `~/.ssh/config` 文件，用于存储 SSH 连接的配置信息。

![img](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/722f55f06c6941a68dfa39b9d7cd1f1b.png)

##### 3.2 编辑 `config` 文件

VS Code 会自动打开并编辑 `~/.ssh/config` 文件。确保该文件格式正确，并添加如下配置：

```
Host myserver
    HostName xxxx.com
    User root
    Port 12803
    IdentityFile ~/.ssh/id_rsa
```

- Host myserver：自定义的名称，你可以用它在后续的 Remote-SSH 界面中快捷选择服务器。
- HostName：服务器的 IP 地址或域名。
- User：远程服务器的用户名。
- Port：SSH 连接的端口号。
- IdentityFile：本地私钥文件路径，确保你已经生成了密钥对并进行了免密登录配置。

#### 4. 通过箭头或新建窗口连接服务器

完成 SSH 配置后，你可以通过 Remote-SSH 插件直接连接到服务器。

如果你按照之前的教程设置了 SSH 免密登录（将公钥上传到服务器），这时连接时将不需要输入密码。如果没有设置免密登录，VS Code 会提示你输入密码。

![img](https://gitee.com/thanatos4/wuxia_imag/raw/master/img/c4c14db182754a67b4accdb9bbdbfd57.png)

**5.注意事项**

- 防火墙或杀毒软件：有时防火墙或杀毒软件（如火绒）可能会阻止 VS Code 与服务器的连接，导致 XHR failed 错误。建议在使用 Remote-SSH 插件时暂时关闭杀毒软件，或者在防火墙中允许 VS Code 访问网络（未出现该问题可忽略，当初踩坑花了很久才发现原因）。

  

##### 建议

通过 VS Code 的 Remote-SSH 插件，你可以轻松地远程连接到服务器，并通过设置 SSH 免密登录，避免每次都输入密码。

**注意事项**

- 防火墙或杀毒软件：有时防火墙或杀毒软件（如火绒）可能会阻止 VS Code 与服务器的连接，导致 XHR failed 错误。建议在使用 Remote-SSH 插件时暂时关闭杀毒软件，或者在防火墙中允许 VS Code 访问网络（未出现该问题可忽略，当初踩坑花了很久才发现原因）。

  

**建议**

通过 VS Code 的 Remote-SSH 插件，你可以轻松地远程连接到服务器，并通过设置 SSH 免密登录，避免每次都输入密码。