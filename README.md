
```
sudo apt update && upgrade -y


curl -O https://raw.githubusercontent.com/angristan/openvpn-install/master/openvpn-install.sh


chmod +x openvpn-install.sh


./openvpn-install.sh



cd ~
curl -sL https://deb.nodesource.com/setup_16.x -o /tmp/nodesource_setup.sh
nano /tmp/nodesource_setup.sh
sudo bash /tmp/nodesource_setup.sh
sudo apt install nodejs

sudo npm install pm2 -g

git clone https://gitlab.com/loki_dv/ovpn.git
mv ovpn/ /home
cd /home
mkdir bvpn
mv ovpn/* bvpn/
rm -r ovpn/


cd bvpn/
npm i
mv /root/openvpn-install.sh /home/bvpn/

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


or


pm2 start main.js
pm2 list
```
for crontab

```
export VISUAL=nano; crontab -e

* 12 * * * reboot


```
