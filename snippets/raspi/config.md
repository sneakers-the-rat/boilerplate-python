# Headless

## [[Raspberry Pi]] connect to [[wifi]]on first boot with [[WPA Supplicant]]

Make a `wpa_supplicant.conf` file in the root "boot" directory when first flashing the drive that looks like this

```
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
country=US

network={
 ssid="NETWORK_NAME"
 psk="NETWORK_PASS"
}
```

## Enable [[SSH]] on first boot

Make an empty file `SSH` in root "boot" directory when first flashing.