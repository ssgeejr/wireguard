# wireguard
Simple instructions for wireguard

from: https://www.freecodecamp.org/news/how-to-set-up-a-vpn-server-at-home/

### SERVER
@root

apt-get install -y wireguard


try this: https://www.stavros.io/posts/how-to-configure-wireguard/



cd ~
mkdir .wireguard
cd .wireguard
umask 077; wg genkey | tee privatekey | wg pubkey > publickey

vi /etc/wireguard/wg0.conf

```
[Interface]
Address = 10.0.0.1/24
ListenPort = 51820
# use the server PrivateKey
PrivateKey = GPAtRSECRETLONGPRIVATEKEYB0J/GDbNQg6V0s=

# you can have as many peers as you wish
# remember to replace the values below with the PublicKey of the peer

[Peer]
PublicKey = NwsVexamples4sBURwFl6HVchellou6o63r2B0s=
AllowedIPs = 10.0.0.2/32
```

sample 2: 
```
[Interface]
Address = 192.168.2.1
PrivateKey = <server's privatekey>
ListenPort = 51820

[Peer]
PublicKey = <client's publickey>
AllowedIPs = 192.168.2.2/32
```

sudo systemctl start wg-quick@wg0

issues for: Cannot find device "wg0"
apt-get install linux-headers-$(uname -r)
(this worked, but if it continues to fail, try the following) 

resolution 1: try to install, wireguard-dkms (failed)


To stop wireguard: systemctl stop wg-quick@wg0

to check if the client is up:
	`ip a show wg0`

ifconfig wg0
wg show

### Alternate configuration site:
https://www.wireguard.com/quickstart/


### Alternate ... 

https://www.ckn.io/blog/2017/11/14/wireguard-vpn-typical-setup/



### CLIENT


https://www.wireguard.com/install/

https://www.linode.com/docs/guides/set-up-wireguard-vpn-on-debian/#configure-wireguard-server

sudo wg set wg0 peer <Client Public Key> allowed-ips 10.0.0.2/24,fd86:ea04:1115::5/64


k
