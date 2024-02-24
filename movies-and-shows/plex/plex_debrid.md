---
description: The final part of the trifecta
---

# Plex\_Debrid

## First Steps

1. `cd /opt`

Install pip.

1. `wget -q https://bootstrap.pypa.io/get-pip.py`
2. `python3 get-pip.py`
3. `rm get-pip.py`

Once that's done, we can set up Plex\_Debrid

1. `git clone https://github.com/itsToggle/plex_debrid`
2. `cd plex_debrid/`
3. `pip install -r ./plex_debrid/requirements.txt`
4. `python3 main.py`

Once here, follow the interactive shell to have a basic setup.

## Editing settings.json

Edit the settings according to your needs, mine looks for french movies in 1080p & 2160p.\
I also use Prowlarr for additional trackers as `FRENCH 2160p` is still pretty scarce on public trackers.

```json
{
    "Content Services": [
        "Plex",
        "Trakt",
        "Overseerr"
    ],
    "Plex users": [
        [
            "deuspi",
            "YourPlexUserToken"
        ]
    ],
    "Plex auto remove": "movie",
    "Trakt users": [],
    "Trakt lists": [],
    "Trakt auto remove": "movie",
    "Trakt early movie releases": "false",
    "Overseerr users": [
        "all"
    ],
    "Overseerr API Key": "",
    "Overseerr Base URL": "",
    "Library collection service": [
        "Plex Library"
    ],
    "Library update services": [
        "Plex Libraries"
    ],
    "Library ignore services": [
        "Local Ignore List"
    ],
    "Trakt library user": [],
    "Trakt refresh user": [],
    "Plex library refresh": [
        "1",
        "2"
    ],
    "Plex library partial scan": "true",
    "Plex library refresh delay": "2",
    "Plex server address": "http://localhost:32400",
    "Plex library check": [],
    "Plex ignore user": "",
    "Trakt ignore user": "",
    "Local ignore list path": "",
    "Jellyfin API Key": "",
    "Jellyfin server address": "http://localhost:8096",
    "Sources": [
        "torrentio",
        "prowlarr"
    ],
    "Versions": [
        [
            "1080p SDR",
            [
                [
                    "retries",
                    "<=",
                    "48"
                ],
                [
                    "media type",
                    "all",
                    ""
                ]
            ],
            "fr",
            [
                [
                    "cache status",
                    "requirement",
                    "cached",
                    ""
                ],
                [
                    "resolution",
                    "requirement",
                    "<=",
                    "1080"
                ],
                [
                    "resolution",
                    "preference",
                    "highest",
                    ""
                ],
                [
                    "title",
                    "requirement",
                    "exclude",
                    "([^A-Z0-9]|HD|HQ)(CAM|T(ELE)?(S(YNC)?|C(INE)?)|ADS|HINDI)([^A-Z0-9]|RIP|$)"
                ],
                [
                    "title",
                    "requirement",
                    "exclude",
                    "(3D)"
                ],
                [
                    "title",
                    "requirement",
                    "exclude",
                    "(DO?VI?)"
                ],
                [
                    "title",
                    "requirement",
                    "exclude",
                    "(HDR)"
                ],
                [
                    "title",
                    "preference",
                    "include",
                    "(EXTENDED|REMASTERED|DIRECTORS|THEATRICAL|UNRATED|UNCUT|CRITERION|ANNIVERSARY|COLLECTORS|LIMITED|SPECIAL|DELUXE|SUPERBIT|RESTORED|REPACK)"
                ],
                [
                    "size",
                    "preference",
                    "highest",
                    ""
                ],
                [
                    "seeders",
                    "preference",
                    "highest",
                    ""
                ],
                [
                    "size",
                    "requirement",
                    ">=",
                    "0.1"
                ]
            ]
        ],
        [
            "2160p",
            [
                [
                    "retries",
                    "<=",
                    "48"
                ],
                [
                    "media type",
                    "all",
                    ""
                ]
            ],
            "fr",
            [
                [
                    "cache status",
                    "requirement",
                    "cached",
                    ""
                ],
                [
                    "resolution",
                    "requirement",
                    "<=",
                    "2160"
                ],
                [
                    "resolution",
                    "preference",
                    "highest",
                    ""
                ],
                [
                    "title",
                    "requirement",
                    "exclude",
                    "([^A-Z0-9]|HD|HQ)(CAM|T(ELE)?(S(YNC)?|C(INE)?)|ADS|HINDI)([^A-Z0-9]|RIP|$)"
                ],
                [
                    "title",
                    "requirement",
                    "exclude",
                    "(3D)"
                ],
                [
                    "title",
                    "requirement",
                    "exclude",
                    "(DO?VI?)"
                ],
                [
                    "title",
                    "preference",
                    "include",
                    "(EXTENDED|REMASTERED|DIRECTORS|THEATRICAL|UNRATED|UNCUT|CRITERION|ANNIVERSARY|COLLECTORS|LIMITED|SPECIAL|DELUXE|SUPERBIT|RESTORED|REPACK)"
                ],
                [
                    "size",
                    "preference",
                    "highest",
                    ""
                ],
                [
                    "seeders",
                    "preference",
                    "highest",
                    ""
                ],
                [
                    "size",
                    "requirement",
                    ">=",
                    "0.1"
                ]
            ]
        ]
    ],
    "Special character renaming": [
        [
            "&",
            "and"
        ],
        [
            "\u00fc",
            "ue"
        ],
        [
            "\u00e4",
            "ae"
        ],
        [
            "\u00e2",
            "a"
        ],
        [
            "\u00e1",
            "a"
        ],
        [
            "\u00e0",
            "a"
        ],
        [
            "\u00f6",
            "oe"
        ],
        [
            "\u00f4",
            "o"
        ],
        [
            "\u00df",
            "ss"
        ],
        [
            "\u00e9",
            "e"
        ],
        [
            "\u00e8",
            "e"
        ],
        [
            "\u00ee",
            "i"
        ],
        [
            "sh!t",
            "shit"
        ],
        [
            "f**k",
            "fuck"
        ],
        [
            "f**king",
            "fucking"
        ],
        [
            ":",
            ""
        ],
        [
            "(",
            ""
        ],
        [
            ")",
            ""
        ],
        [
            "`",
            ""
        ],
        [
            "\u00b4",
            ""
        ],
        [
            ",",
            ""
        ],
        [
            "!",
            ""
        ],
        [
            "?",
            ""
        ],
        [
            " - ",
            " "
        ],
        [
            "'",
            ""
        ],
        [
            "\u200b",
            ""
        ],
        [
            "*",
            ""
        ],
        [
            " ",
            "."
        ]
    ],
    "Rarbg API Key": "",
    "Jackett Base URL": "http://127.0.0.1:9117",
    "Jackett API Key": "",
    "Jackett resolver timeout": "1",
    "Jackett indexer filter": "!status:failing,test:passed",
    "Prowlarr Base URL": "http://192.168.0.10:49696",
    "Prowlarr API Key": "YourProwlarrAPIKey",
    "Orionoid API Key": "",
    "Orionoid Scraper Parameters": [
        [
            "limitcount",
            "5"
        ],
        [
            "sortvalue",
            "popularity"
        ],
        [
            "streamtype",
            "torrent"
        ],
        [
            "filename",
            "true"
        ]
    ],
    "Nyaa parameters": "&c=1_0&s=seeders&o=desc",
    "Nyaa sleep time": "5",
    "Nyaa proxy": "nyaa.si",
    "Torrentio Scraper Parameters": "https://torrentio.strem.fun/providers=yts,eztv,rarbg,1337x,thepiratebay,kickasstorrents,torrentgalaxy,magnetdl,nyaasi,rutor,rutracker,torrent9|language=french,turkish|qualityfilter=720p,480p,other,scr,cam|limit=6/manifest.json",
    "Debrid Services": [
        "Real Debrid"
    ],
    "Tracker specific Debrid Services": [],
    "Real Debrid API Key": "YourRealDebridAPIKey",
    "All Debrid API Key": "",
    "Premiumize API Key": "",
    "Debrid Link API Key": "",
    "Put.io API Key": "",
    "Show Menu on Startup": "true",
    "Debug printing": "false",
    "Log to file": "false",
    "version": [
        "2.95",
        "Settings compatible update",
        []
    ]
}
```

## Testing

Once you've configured `plex_debrid` test it by adding a movie or tv show to your watchlist, whether it's through Plex Discover or Trakt (based on your settings).

Check if there are any error messages, if not: GG :tada:, but that's just the first step.

The second step is to make sure the releases found by plex\_debrid are actually downloaded.\
_For that, simply login to_ [_Real-Debrid_](https://real-debrid.com/) _and look for the latest downloads in the `Torrents` tab._

If not, there's an issue with your settings. Go back and fix that :poop:.

If everything's good then **Congratulations** :tada:
