时间服务 `timedatectl` 命令

```shell
# 获取时间信息
timedatectl
timedatectl status
# 设置时间
sudo timedatectl set-time "yyyy-MM-dd hh:mm:ss"
# 显示可用时区
timedatectl list-timezones
# 修改时区
timedatectl set-timezone <Zone>/<SubZone>
# 修改时区为上海
timedatectl set-timezone Asia/Shanghai
# 手动设置时区为上海
ln -sf /usr/share/zoneinfo/_Zone_/_SubZone_ /etc/localtime
```

> `timedatectltimedatectl set-timezone <Zone>/<SubZone>`的本质便是创建文件软链接，也就是`ln -sf /usr/share/zoneinfo/_Zone_/_SubZone_ /etc/localtime`
