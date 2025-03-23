# Zurg

## Clone & Extract

[This section is currently obsolete](#user-content-fn-1)[^1]

```bash
mkdir /mnt/zurg /mnt/cache
```

```bash
apt-get install libxml2-utils
```

```bash
git clone https://github.com/debridmediamanager/zurg-testing /opt/zurg-testing/ ; cd /opt/zurg-testing/
```

```bash
mv releases/v0.9.3-hotfix.6/zurg-v0.9.3-hotfix.6-darwin-amd64.zip ../zurg.zip ;
unzip ../zurg.zip ;
mv ../zurg/zurg . ;
sudo chmod +x ./zurg
```

## Edit <mark style="color:purple;">config.yml</mark>

```yaml
zurg: v1
token: yourToken
concurrent_workers: 20
check_for_changes_every_secs: 60
repair_every_mins: 60
ignore_renames: false
retain_rd_torrent_name: false
retain_folder_name_extension: false
enable_repair: true
auto_delete_rar_torrents: true
# api_timeout_secs: 15
# download_timeout_secs: 10
# enable_download_mount: false
# network_buffer_size: 4194304 # 4MB
# serve_from_rclone: false
# verify_download_link: false
# force_ipv6: false
rate_limit_sleep_secs: 6
retries_until_failed: 2
use_download_cache: true
on_library_update: sh plex_update.sh "$@"

directories:
  # We start by filtering out TV Shows, excluding some false positives
  # Configuration for anime needs too much tuning, ain't nobody got time for that.
  shows:
    group_order: 10
    group: media
    filters:
      - any_file_inside_regex: /(S\d{1,2}E\d{2}|S\d{1,2}|season|shogun|kingstown|severance)/i
      - any_file_inside_not_regex: /.*(?:wakfu|one[\s._-]?piece|loser[\s._-]?ranger|full[\s._-]?metal|mushoku[\s._-]?tensei|solo[\s._-]?leveling|frieren|kid[\s._-]?paddle).*/i

  anime:
  # Whatever folder has episodes but hasn't been classified as a TV show
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

## Edit <mark style="color:orange;">plex\_update.sh</mark>

Two lines to update: Plex token and `zurg` mounting point.

## Testing

Test everything manually to make sure it works properly:

Simply run the binary and check the standard output for any errors.

* `./zurg`

## Systemd Service

Put this into `/etc/systemd/system/zurg.service`

```systemd
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

Run `systemctl enable zurg`

[^1]: Zurg's developer changed the repo's structure and how binaries are delivered.
