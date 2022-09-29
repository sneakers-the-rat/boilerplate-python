## Mounting [[ext4]] on [[macOS]] using [[ext4fuse]]
```
sudo ext4fuse /dev/disk<n>s<n> <mountpoint> -o allow_other
```