---
homepage: "http://netatalk.sourceforge.net/"
docs: "http://netatalk.sourceforge.net/3.1/htmldocs/"
config: "/etc/netatalk/afp.conf"
---


## config

 basic local-only global settings with a juiced up buffer and limited connections

 ```
[Global]
tcprcvbuf = 262144
tcpsndbuf = 262144
dsireadbuf = 256
dircachesize = 65536
max connections = 5
hosts allow = 192.168.1.0/24
guest account = "guest"
```


## time machine

```
[timemachine]
path = /path/to/dir
time machine = yes
rwlist = "username"
valid users = "username"
file perm = 0770
directory perm = 0774
use splice = 0
acls = no
search db = yes
```

