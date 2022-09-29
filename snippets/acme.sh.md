## Issue a cert for cpanel

```shell
acme.sh --issue -d open-behavior.auto-pi-lot.com -w /home/nod3bp3usey4/public_html/open-behavior.auto-pi-lot.com/ --deploy-hook cpanel_uapi
```

Deploy

```shell
~/.acme.sh/acme.sh --deploy -d open-behavior.auto-pi-lot.com --deploy-hook cpanel_uapi
```

## Issue a cert with [[nginx]]
```shell
acme.sh --issue --nginx -d example.com
```