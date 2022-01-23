## Guestorrents
Allow guests to be able to drop .torrent files to download in a public folder and then pick them up when they're done without giving direct access to the torrent client or other parts of the filesystem.

Uses [[netatalk]], [[afpd]], and [[qbittorrent]]

- Set up a [[netatalk]] share that gives guests read/write access 
```
[global]
guest account = "guest"

[guestorrent]
path = /base/path/guestorrent
rwlist = "user1", "guest"
browseable = yes
file perm = 0776
directory perm = 0776
```
* set [[qbittorrent]] to automatically download torrents in a `to_download` folder and then output them to a `completed folder`
* make a directory structure like this so that others can drag files that they want to be moved to the target location for eg. use with [[plex]] or whatever
	* `move_to`
		* `Movies`
		* `Music`
		* etc.
* [[todo]] : figure out how to watch files and automatically move them!