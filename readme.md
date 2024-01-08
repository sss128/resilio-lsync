### 命令
- 安装完lsync
- 创建 /etc/lsyncd/lsyncd.conf.lua
- 执行 systemctl start lsyncd
### 流程
resilio同步目录 在本地通过lsync同步到 emby媒体库目录，在同步的过程中可以执行 sed -i 操作从而替换ip
