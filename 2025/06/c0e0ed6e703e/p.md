---
title: 配置静态ip
date: '2025-6-14 22:00'
categories:
  - Ubuntu
---
sudo -i #root用户
 ls -l /etc/netplan
![](/images/Pastedimage20250601205045.png)
sudo chmod 600 /etc/netplan/01-network-manager-all.yaml  #修改文件权限
sudo nano /etc/netplan/01-network-manager-all.yaml  #更新配置文件内容
```
network:
  version: 2
  renderer: NetworkManager
  ethernets:
    ens33:
      addresses: [192.168.142.132/24]         # 设置静态IP地址和掩码
      routes:
        - to: default
          via: 192.168.142.2
      nameservers:
        addresses: [114.114.114.114,8.8.8.8]  # 设置主、备DNS
      dhcp4: false                            # 禁用dhcp
```
sudo netplan apply  #应用更改
```
#验证配置
ip a show ens33
ping -c 4 8.8.8.8   
```

```
#确保SSH服务正常运行
sudo apt install openssh-server
sudo systemctl start ssh
sudo systemctl enable ssh
```
![](/images/Pastedimage20250601213334.png)
#### **使用 SSH 密钥登录（最安全）**

1. 在物理机生成密钥对：
    ssh-keygen  # 默认保存到 ~/.ssh/id_rsa==(空密码)==
   ![](/images/Pastedimage20250601214315.png)）
2. 将公钥复制到虚拟机：
    scp C:\Users\Rhea\.ssh\id_rsa.pub rhea@192.168.142.132:~/
   ![](/images/Pastedimage20250601214846.png)）
3. 直接免密登录：
   ![](/images/Pastedimage20250601221831.png)）
