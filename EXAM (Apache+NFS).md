#### Request
Web1 與 Web2 同時負責相同的網站，其網站資料放在 NFS 中，現需要它們串連起來完成此一網站服務。使用者不論連到 Web1 或 Web2 都能看得到內容。

#### NFS Server 目錄
```
/web
```

#### Web1 & Web2 目錄
將 NFS 之分享目錄掛載在 /var/www/html`

#### Verify
在 NFS Server, Web1, Web2 中可以看到相同之網頁

```
root# curl http://web1/web.htm
root# curl http://web2/web.htm
```

#### Solutions  

@NFS Server, Web1, Web2
```
root# echo 10.6.1.1 nfs >> /etc/hosts
root# echo 10.6.1.11 web1 >> /etc/hosts
root# echo 10.6.1.12 web2 >> /etc/hosts
```

@NFS Server

1. Install packages.
```
root# yum install -y rpcbind nfs-utils
root# systemctl enable rpcbind
root# systemctl enable nfs-server
root# systemctl disable firewalld
root# reboot
```

2. Create web file folder.
```
root# mkdir /web
root# echo hello world > /web/web.htm
root# chown -Rf nfsnobody /web/
```

3. Setup NFS
```root# vi /etc/exports```
```/web 10.6.X.0/24(rw)```

4. Verify NFS exports
```
root# showmount -e localhost
root# systemctl reload nfs-server
root# showmount -e localhost
```

@Web1, Web2
```
root# yum install -y rpcbind nfs-utils httpd

root# systemctl enable --now httpd
root# systemctl status httpd
```

```
root# firewall-cmd --list-all
root# firewall-cmd --permanent --add-service=http
root# firewall-cmd --reload
root# firewall-cmd --list-all
```

```root# showmount -e nfs```
```root# mount -t nfs nfs:/web /var/www/html```

### Verify
@NFS Server, Web1, Web2
```
root# curl http://web1/web.htm
root# curl http://web2/web.htm
```

@Web1, Web2

```root# setsebool httpd_use_nfs 1```
> Ref: https://linux.die.net/man/8/httpd_selinux

@NFS Server, Web1, Web2

```
root# curl http://web1/web.htm
root# curl http://web2/web.htm
```
