msfvenom -l encoders

The default login for all OVA images is: root:blackarch

sudo apt install build-essential dkms linux-headers-$(uname -r)


### ACTIVE DIRECTORY 

Domain = SnowWorksDev => snowworksdev.local

Network = 192.168.10.0/24

Domain Controller = 192.169.10.5

Host 1 = 192.168.10.3 (DHCP)

Host 2 = 192.168.10.4 (DHCP)

Splunk Server = 192.168.10.10 (Splunk Enterprise)

Parrot OS = DHCP = parrot X2

### Additionals

PfSense= Firewall

-------------------------------------------------------------------------

#### DC USERS  

Administrator ====  Local@dmin - shelbycompany\administrator

John-HR = Password01 - User

ITDept = Tech@100 - Admin - thorne

Lisa-Sales = P@ssword2002 - User

SQLService = DataB1001


-------------------------------------------------------------------------

### NESSUS VM 

https://machine-ip:8834/


root-user == wizard

root-password === admin


username = nessusd

key = tryhackme

ip a - check ip address

Activating Your Nessus Essentials License

Your activation code for Nessus Essentials is:

LK2D-STNU-AT8L-D36K-D5G2

-------------------------------------------------------------------------

### SPLUNK SERVER VM

Splunk is a software platform used for searching, monitoring, and analyzing machine-generated data.

Ubuntu Server 20.04.6 LTS = To install Splunk

http://192.168.1.115:8000/ 		(Browser)


sudo /opt/splunk/bin/splunk start



username =sysadmin

password = hireme


admin = sysadmin

password = hiremeplease

-------------------------------------------------------------------------

### OpenVAS

OpenVAS is a full-featured vulnerability scanner.

username:

password:


`sudo gvm-check-setup` --- check installation


`sudo gvm-start`  --- start openVas




-------------------------------------------------------------------------
### WAZUH VM


Wazuh is a free and open-source platform that provides both XDR (Extended Detection and Response) and SIEM (Security Information and Event Management) capabilities. 




user: wazuh-user
password: wazuh

Root privilege escalation can be achieved by executing the following command:

`sudo -i`

Access the Wazuh dashboard:

ip a

```
URL: https://192.168.5.124
user: admin
password: admin
```

username: admin
password: IxQmb4xrj5+jNi6nXNa2+vK*qHnQ?j*j


sudo systemctl start wazuh-manager



-------------------------------------------------------------------------

### T-POT HONEYPOT

user = rocky
key = potadmin

sudo apt install net-tools


sudo systemctl restart tpot

ip a

https://127.0.0.1:64297

sudo docker ps

8GB ++ RAM = 20 containers running

T-Pot recommends at least:

4 vCPUs

8 GB RAM (ideally 16 GB or more)

Fast SSD storage

-------------------------------------------------------------------------



### SecureBank Docker

Admin=admin@ssrd.io
AdminPassword=admin


docker run -d -p 80:80 -p 5000:5000 -p 1080:1080 -e 'SeedingSettings:Admin=admin@ssrd.io' -e 'SeedingSettings:AdminPassword=admin' ssrd/securebank

http://127.0.0.1

docker ps -a



-------------------------------------------------------------------------

### DVWA Docker 


docker run -d -p 80:80 vulnerables/web-dvwa


172.17.0.2

user = admin
key = password

docker exec -it "image-id" /bin/bash  --- Obtain image shell

cat  /etc/php/8.4/apache2/php.ini | grep allow_url_include


http://192.168.1.40:8000/rfi

-------------------------------------------------------------------------


### Juice Shop Docker

docker run -d -p 3000:3000 --name juice-shop bkimminich/juice-shop


ip -bc -c a


http://172.17.0.2/vulnerabilities/csrf/?password_new=hacker&password_conf=hacker&Change=Change&user_token=74bb3729208bc9275b941239fc4477d4#


arp -a


-------------------------------------------------------------------------------


### bWAPP-Docker

This is a simple Docker image for the OWASP bWAPP application designed to teach and demonstrate various web app vulnerabilities.


docker run -d -p 80:80 hackersploit/bwapp-docker





-------------------------------------------------------------------------

### Mobile Security Framework (MobSF)


docker run -it --rm -p 8000:8000 opensecurity/mobile-security-framework-mobsf:latest

# Default username and password: mobsf/mobsf



-------------------------------------------------------------------------

### SPLUNK SERVER  INSTALLATION



Splunk Universal forwarder = The universal forwarder (UF) collects data securely from remote sources, including other forwarders, and sends it into Splunk.

Sysmon = Windows system monitor tool from Microsoft that logs system activity to the Windows event log, offering detailed information about process creations, network connections, and other system events

IDS = Intrution Detection System

EDR - End-point Detection and Response


###### Prepare Splunk Env ######

sudo apt-get update

sudo apt-get install virtualbox-guest-additional-iso 	(help with shared folder)

sudo apt install virtualbox-guest-utils 	(if vboxsf not available)

sudo adduser username vboxsf 	(add user to vboxsf group)

sudo reboot




sudo nano /etc/netplan/00-installer-config.yaml 	(config routes & static ips & dns)

sudo netplan apply




sudo reboot

mkdir share

sudo mount -t vboxsf -o uid=1000,gid=1000 Programs share/ 	(mount shared folder)

cd share

sudo dpkg -i splunk-installer.deb 		(install splunk)

cd /opt/splunk (where its intalled)

ls -la 		(check if user is splunk)

sudo -u splunk bash 	(switch to splunk user)

cd /opt/splunk/bin (binaries splunk can use)


./splunk start 		(run installer)


exit 		(exit splunk user)

cd bin

sudo ./splunk enable boot-start -user splunk 		(to start on boot)





#### install symon and Splunk Universal Forwarder (UF)	$$	(target + server)

`Splunk Universal Forwarder (UF)`

sudo dpkg -i splunkforwarder-<version>-linux-2.6-amd64.deb



sudo /opt/splunkforwarder/bin/splunk start --accept-license



sudo /opt/splunkforwarder/bin/splunk enable boot-start  (UF start on boot)



### Targets

sudo /opt/splunkforwarder/bin/splunk add forward-server 192.168.5.115:9997 -auth admin:changeme  (Forward logs to Splunk server) (127.0.0.1 - used ip)


sudo /opt/splunkforwarder/bin/splunk add monitor /var/log/auth.log  (Add logs to monitor)




sudo /opt/splunkforwarder/bin/splunk status (start, status, stop)


sudo /opt/splunkforwarder/bin/splunk list forward-server



sudo ufw allow 9997/tcp (if firewall is enabled)
sudo ufw reload


`SYMon (Linux version)`


### Windows install

Install Splunk Universal Forwarder (UF) windows

sysmon olaf config (sysmon config.xml)

copy Sysmon folder location

open powershell as admin

cd sysmon folder

.\Sysmon64.exe -i .\sysmonconfig.xml


C:\ProgramFiles\SplunkUniversal\etc\system\default\inputs.config  (we need to copy this config file  paste it in local folder) (the one in default is a backup)


Or just use this one `https://github.com/MyDFIR/Active-Directory-Project` (paste in local folder)


Start splunk services (Services run as admin) look for splunk foward services.

Change log on as from NTLM to local system, restart the service by right clicking on it.


add endpoint index in the splunk server

go to fowarding and receiving , receive data add new port (9997)



---


