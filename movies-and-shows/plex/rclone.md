# RClone

## First steps

1. `cd /opt`
2. `wget -q- https://downloads.rclone.org/rclone-current-linux-amd64.zip`
3. `unzip rclone-current-linux-amd64.zip`
4. `mv rclone-v{x.yy.zz}-linux-amd64/rclone /opt/zurg-testing/`
5. `cd zurg-testing; sudo chmod +x ./rclone`

## Testing

Test everything manually to make sure it works properly:

* `./rclone mount zurg: /mnt/zurg --config=/opt/zurg-testing/rclone.conf --log-level=INFO --log-file=/opt/zurg-testing/zurg.log --allow-other --cache-dir=/mnt/cache/ --dir-cache-time=30s`

## Rclone Service

Put this into `/etc/systemd/system/rclone.service`

```
[Unit]
Description=Rclone mount for zurg
After=network-online.target

[Service]
Type=notify
ExecStart=/opt/zurg-testing/rclone mount \
  zurg: /mnt/zurg \
  --allow-other \
  --allow-non-empty \
  --async-read \
  --cache-dir=/mnt/cache/ \
  --config=/opt/zurg-testing/rclone.conf \
  --dir-cache-time=30s \
  --log-level=INFO \
  --log-file=/opt/zurg-testing/zurg.log \
  --vfs-cache-mode full \
  --vfs-cache-max-age 24h \
  --vfs-cache-max-size 50G
ExecStop=/bin/bash -c '/bin/fusermount -uz /mnt/zurg; umount /mnt/zurg'
Restart=on-abort
RestartSec=1
StartLimitInterval=60s
StartLimitBurst=3

[Install]
WantedBy=multi-user.target
```

Run `systemctl enable rclone`
