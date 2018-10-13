# Gluster Docs
-------------
## Restart command
1. 开启gluster容器，如果已经启动了则不必再执行
`sudo docker start gluster-4.0.2`
2. mount路径，正确执行后会出现一个warning，如果没有，代表没有成功执行. 此时，需要 sudo umount /mnt/gluster. 之后再重新执行下面的命令
`sudo docker exec gluster-4.0.2 gluster-mount.sh`
