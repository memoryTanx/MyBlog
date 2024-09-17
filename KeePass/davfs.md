# Ubuntu 22.04 & jianguoyun

## 安装

```bash
apt-get install davfs2

mkdir /mnt/webdav/jianguoyun -p

# davfs 帮助
mount.davfs

# to allow mounting by non-root users.
sudo dpkg-reconfigure davfs2
```

## 非root账户挂载,把 pc_username 账户加入 davfs2 组,不用root权限也可以挂载.
```bash
# 添加到 davfs2 组，注销再登录才会生效
usermod -a -G davfs2 pc_username
```

## 把用户名和密码写入secrets文件,以便自动登录.
```bash
echo "https://dav.jianguoyun.com/dav/ {username} {password}" >> /etc/davfs2/secrets
```

## 将davfs2.conf配置文件中的use_locks的默认值1修改为0
```bash
sed -i 's/# use_locks          1/# use_locks          0/g' /etc/davfs2/davfs2.conf


# 修改项
use_locks       0
ignore_dav_header 1
```

## 挂载到fstab(文件管理器自动能显示出来)
```bash
echo "https://dav.jianguoyun.com/dav/ /mnt/webdav/jianguoyun davfs uid=1000,gid=1000,_netdev,auto,user,rw 0 0" >> /etc/fstab
```

# 参考，帮助
- https://askubuntu.com/questions/498492/mounting-a-webdav-share-for-all-users
- https://en.wikipedia.org/wiki/Fstab
- https://discourse.osmc.tv/t/systemd-automount-using-davfs2-not-working/94200
- https://vircloud.net/operations/linux-webdav.html
- https://github.com/alist-org/alist/discussions/5470
- https://wenku.csdn.net/answer/3be2f21b182444a49c5942ea70b70302
- https://www.yunieebk.com/davfs2/

