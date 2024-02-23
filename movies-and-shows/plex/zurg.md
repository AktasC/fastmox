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
token: YOURTOKEN
# host: "[::]"
# port: 9999
# username:
# password:
# proxy:

# concurrent_workers: 20
check_for_changes_every_secs: 30
retain_rd_torrent_name: false
retain_folder_name_extension: false
expose_full_path: true
enable_repair: true
auto_delete_rar_torrents: true
# on_library_update: sh plex_update.sh "$@"

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
