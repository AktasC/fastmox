# Zurg

## First steps

1. `mkdir /mnt/zurg /mnt/cache`
2. `cd /opt`
3. `git clone https://github.com/debridmediamanager/zurg-testing`
4. `cd zurg-testing/`
5. `mv releases/v0.9.3-hotfix.6/zurg-v0.9.3-hotfix.6-darwin-amd64.zip zurg.zip unzip ./zurg.zip`
6. `sudo chmod +x ./zurg`

## Edit config.yaml

```yaml
zurg: v1
token: YourRealDebridToken
auto_delete_rar_torrents: true
# concurrent_workers: 20
check_for_changes_every_secs: 30
enable_repair: true
# repair_every_mins: 60
ignore_renames: false
on_library_update: sh plex_update.sh "$@"

# to check your fastest hosts, run ./zurg network-test
preferred_hosts:
  - 65.download.real-debrid.com
  - 68.download.real-debrid.com
  - 50.download.real-debrid.com
  - 67.download.real-debrid.com
  - 66.download.real-debrid.com
  - 91.download.real-debrid.com
  - 70.download.real-debrid.com
  - 78.download.real-debrid.com
  - 84.download.real-debrid.com
  - 77.download.real-debrid.com
rate_limit_sleep_secs: 6
realdebrid_timeout_secs: 60
retain_folder_name_extension: false
retain_rd_torrent_name: false
retries_until_failed: 2
use_download_cache: true

# List of directory definitions and their filtering rules
directories:
  # Configuration for anime shows
  anime:
    group: media # directories on different groups have duplicates of the same torrent
    group_order: 10 # group order = priority, it defines who eats first on a group
    filters:
      - and: # you can use nested 'and' & 'or' conditions
        - has_episodes: true # intelligent detection of episode files inside a torrent
        - any_file_inside_regex: /^\[/ # usually anime starts with [ e.g. [SubsPlease]
        - any_file_inside_not_regex: /s\d\de\d\d/i # and usually anime doesn't use SxxExx
  shows:
    group: media
    group_order: 20
    filters:
      - has_episodes: true  # intelligent detection of episode files inside a torrent
  movies:
    group: media  # because anime, shows and movies are in the same group,
    group_order: 30 # and anime and shows has a lower group_order number than movies, all torrents that doesn't fall into the previous 2 will fall into movies
    only_show_the_biggest_file: true # let's not show the other files besides the movie itself
    filters:
      - regex: /.*/
```

## Edit plex\_update.sh

Two lines to update: Plex token and `zurg` mounting point.

## Testing

Test everything manually to make sure it works properly:

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

Run `systemctl enable zurg`
