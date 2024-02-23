# Zurg

## First steps

1. `mkdir /mnt/zurg /mnt/cache`
2. `cd /opt`
3. `git clone https://github.com/debridmediamanager/zurg-testing`
4. `cd zurg-testing/`
5. `mv releases/v0.9.3-hotfix.6/zurg-v0.9.3-hotfix.6-darwin-amd64.zip zurg.zip unzip ./zurg.zip`
6. `sudo chmod +x ./zurg`

## Edit config.yml

```yaml
zurg: v1
token: YOURTOKEN
# host: "[::]"
# port: 9999
# username:
# password:
# proxy:
# concurrent_workers: 20
check_for_changes_every_secs: 30
# repair_every_mins: 60
# ignore_renames: false
# retain_rd_torrent_name: false
# retain_folder_name_extension: false
enable_repair: true
auto_delete_rar_torrents: true
# api_timeout_secs: 15
# download_timeout_secs: 10
# enable_download_mount: false
# rate_limit_sleep_secs: 6
# retries_until_failed: 2
# network_buffer_size: 4194304 # 4MB
# serve_from_rclone: false
# verify_download_link: false
# force_ipv6: false
# on_library_update: sh plex_update.sh "$@"

directories:
  anime:
    group_order: 10
    group: media
    filters:
      - regex: /\b[a-fA-F0-9]{8}\b/
      - any_file_inside_regex: /\b[a-fA-F0-9]{8}\b/

  shows:
    group_order: 20
    group: media
    filters:
      - has_episodes: true

  movies:
    group_order: 30
    group: media
    only_show_the_biggest_file: true
    filters:
      - regex: /.*/
```

## Testing

Test everything manually to make sure each soft works properly:

Simply run the binary and check the standard output for any errors.

* `./zurg`

## Systemd Service

Put this into `/etc/systemd/system/zurg.service`

```
[Unit]
Description=zurg
After=network-online.target

[Service]
Type=simple
ExecStart=/opt/zurg-testing/zurg
WorkingDirectory=/opt/zurg-testing
StandardOutput=file:/var/log/zurg.log
StandardError=file:/var/log/zurg.log
Restart=on-abort
RestartSec=1
StartLimitInterval=600s
StartLimitBurst=5

[Install]
WantedBy=multi-user.target

```
