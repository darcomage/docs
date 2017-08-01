# Software Systems

Our [Superdoc](https://docs.google.com/document/d/1ZqDp1sfxVkDEsVfQ0Fsqpa6n7totzh_2IA4IrXp5i_4/edit) 
is currently our main source of information; that will slowly be migrated here.

## Comms Interfaces

- Arduino-Electrical interface: [Pinout](https://docs.google.com/spreadsheets/d/18PZNkgs89I_vvb521Zw7m2bll4Fvnhqy8EalrwVd7fA/edit#gid=1787642201)

- Raspberry Pi-Arduino interface: [Serial Comms Spec](http://htmlpreview.github.io/?https://github.com/teamwaterloop/communication-system/blob/master/communication_format.html)

- Dashboard-Raspberry Pi interface: WebSocket Comms Spec???

## Raspberry Pi setup tutorial and configurations

> Initial Note: We are using a RPI3, so we have wifi module built in. If you are using and older RPI, then you might have to adjust certain things like the name of your wireless device

1. [Flush an OS on your RPI](https://www.raspberrypi.org/documentation/installation/installing-images/). We are using raspbian os because it has GUI, which could be helpful when resolving problems in networking
2. [Enable SSH on RPI](https://www.raspberrypi.org/documentation/remote-access/ssh/)
3. Node should come pre-installed, you can check if it is installed by running `node -v` any version above 4.2 should be suitable
* If your version is below 4.2, then you should update node 
```
sudo npm cache clean -f 
sudo npm install -g n 
sudo n stable
```
4. Make sure you have npm installed `npm -v`
5. Install pm2 `sudo npm install -g pm2`
- Configure pm2 to start `server.js` on boot
```
> pm2 startup systemd
Output
[PM2] Init System found: systemd
[PM2] You have to run this command as root. Execute the following command:
sudo env PATH=$PATH:/usr/bin /usr/lib/node_modules/pm2/bin/pm2 startup systemd -u sammy --hp /home/sammy
``` 
- You have to run the command as directed in the output
- Run server with PM2 
```
pm2 start server.js
pm2 save
```
> Now server will start on boot you can check logs from the server `pm2 logs`
    
6. Set static ip on rpi:
- Configure `sudo nano /etc/dhcpcd.conf`
- At the very bottom of the file, add the following lines:
```
interface wlan0

static ip_address=192.168.0.200/24
static routers=192.168.0.1
static domain_name_servers=192.168.0.1
```
- Reboot `sudo reboot` and check that it worked `ifconfig` under wlan0 interface you should see your specified IP address
```
 wlan0     Link encap:Ethernet  HWaddr 00:0F:20:CF:8B:42
           inet addr:192.168.0.1  Bcast:217.149.127.63  Mask:255.255.255.192
           UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
           RX packets:2472694671 errors:1 dropped:0 overruns:0 frame:0
           TX packets:44641779 errors:0 dropped:0 overruns:0 carrier:0
           collisions:0 txqueuelen:1000
```   
    