## Install up-to-date qbittorrent versions on [[Ubuntu]]
Using the stable [[PPA]] https://launchpad.net/~qbittorrent-team/+archive/ubuntu/qbittorrent-stable
```bash
sudo add-apt-repository ppa:qbittorrent-team/qbittorrent-stable
sudo apt-get update
sudo apt install qbittorrent
```

### Set up headless daemon
[qbittorrent docs](https://github.com/qbittorrent/qBittorrent/wiki/Running-qBittorrent-without-X-server-(WebUI-only,-systemd-service-set-up,-Ubuntu-15.04-or-newer))

make qbtuser, then do first run
```bash
sudo adduser qbtuser
sudo su qbtuser
qbittorrent-nox
```

Then go to the webui at port 8080 and configure it, most importantly change the password!

Make the [[systemd]] service:
`/etc/systemd/system/qbittorrent.service`

```toml
[Unit]
Description=qBittorrent-nox service
Documentation=man:qbittorrent-nox(1)
Wants=network-online.target
After=network-online.target nss-lookup.target

[Service]
# if you have systemd < 240 (Ubuntu 18.10 and earlier, for example), you probably want to use Type=simple instead
Type=exec
# change user as needed
User=qbtuser
# The -d flag should not be used in this setup
ExecStart=/usr/bin/qbittorrent-nox
# uncomment this for versions of qBittorrent < 4.2.0 to set the maximum number of open files to unlimited
#LimitNOFILE=infinity
# uncomment this to use "Network interface" and/or "Optional IP address to bind to" options
# without this binding will fail and qBittorrent's traffic will go through the default route
# AmbientCapabilities=CAP_NET_RAW

[Install]
WantedBy=multi-user.target
```

Enable and start the service!

```bash
sudo systemctl daemon-reload
sudo systemctl enable qbittorrent
sudo systemctl start qbittorrent
```

Then you probably need to make a download directory with the correct [[Permissions]], and disable [[SSH]] login for the qbtuser:

```bash
sudo usermod -s /usr/sbin/nologin qbtuser
```
