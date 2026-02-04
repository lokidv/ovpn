
```
sudo apt update && sudo apt upgrade -y

sudo apt-get install -y ca-certificates curl gnupg
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://deb.nodesource.com/gpgkey/nodesource-repo.gpg.key | sudo gpg --dearmor -o /etc/apt/keyrings/nodesource.gpg
NODE_MAJOR=20
echo "deb [signed-by=/etc/apt/keyrings/nodesource.gpg] https://deb.nodesource.com/node_$NODE_MAJOR.x nodistro main" | sudo tee /etc/apt/sources.list.d/nodesource.list
sudo apt-get update
sudo apt-get install nodejs -y


git clone https://github.com/lokidv/ovpn.git
mv ovpn/ /home
cd /home
mkdir bvpn
mv ovpn/* bvpn/
rm -r ovpn/


cd bvpn/
rm openvpn-install.sh
wget https://raw.githubusercontent.com/angristan/openvpn-install/648fe1ee0bb16f1ff9ce4e9957007bbec480ef76/openvpn-install.sh
chmod +x openvpn-install.sh
./openvpn-install.sh
npm i


nano /etc/systemd/system/bvpn.service

[Unit]
Description=Tunnel WireGuard with udp2raw
After=network.target

[Service]
Type=simple
User=root
ExecStart=sudo node /home/bvpn/main.js
Restart=no

[Install]
WantedBy=multi-user.target

systemctl enable --now bvpn.service 

rm /home/bvpn/openvpn-install.sh  && wget https://raw.githubusercontent.com/lokidv/ovpn/main/openvpn-install.sh -O /home/bvpn/openvpn-install.sh && chmod +x /home/bvpn/openvpn-install.sh && sudo systemctl restart bvpn.service

crontab -e
* * * * * /bin/systemctl is-active --quiet udp2raw.service || /bin/systemctl restart udp2raw.service
*/10 * * * * /bin/systemctl restart bvpn.service
or



```
for crontab

```
export VISUAL=nano; crontab -e

* 12 * * * reboot


```

for transfer
```
cd /
tar czvf openvpn_backup.tar.gz /etc/openvpn/ /etc/openvpn/easy-rsa/
scp openvpn_backup.tar.gz root@ip:/root
tar xzvf openvpn_backup.tar.gz
sudo systemctl stop openvpn@server.service
rm -r /etc/openvpn/
mv etc/openvpn /etc
nano /etc/systemd/system/udp2raw.service
```

