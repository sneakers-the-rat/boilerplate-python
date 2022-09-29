[ INFO ] WireGuard client setup has been chosen                       
│ Please follow the instructions of your VPN provider to configure WireGuard.                                         │

│ If no WireGuard (auto)start is included, but you require it, please do the following:

 1. Check for the created config file/interface name:                 `ls -Al /etc/wireguard/`
   It has a ".conf" file ending, lets assume "wg0-client.conf".          
2. To start the VPN interface, run:                                                `systemctl start wg-quick@wg0-client`

3. To autostart the VPN interface on boot, run:                  `systemctl enable wg-quick@wg0-client`  

4. To disable autostart again, run:                                           `systemctl disable wg-quick@wg0-client`