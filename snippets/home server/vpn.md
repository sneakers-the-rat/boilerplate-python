# Check status of [[Wireguard]]
https://github.com/pia-foss/manual-connections/

``wg show``

look for `last handshake time`, eg

```
>>> wg show
interface: wg0
  public key: qZ7+xNeXCjKdRNM33Diohj2Y/KSOXwvFfgTS1LRx+EE=
  private key: (hidden)
  listening port: 49785

peer: 6lf4SymMbY+WboI4jEsM+P9DhogzebSULrkFowDTt0M=
  endpoint: 3.133.147.235:51820
  allowed ips: 10.100.100.1/32
  latest handshake: 14 seconds ago
  transfer: 732 B received, 820 B sent
  persistent keepalive: every 21 seconds
```

