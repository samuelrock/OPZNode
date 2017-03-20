# Orange Pi Zero Asterisk Radio Node
## Instructions for installing AllStar node on Orange Pi

Install Armbian on SD Card
```
- Win32 Disk Imager  
- Image file: Armbian_5.25_Orangepizero_Debian_jessie_default_3.4.113.img  
- default login is root/1234  
- create new password and admin user  
- nmtui-hostname modify hostname of device  
- reboot
```  	
Follow these instructions: https://github.com/N4IRS/AllStar
```
cd /tmp  
wget --no-check-certificate https://github.com/N4IRS/AllStar/archive/master.zip  
rm -f AllStar-master  
ln -s /srv AllStar-master  
unzip master.zip  
rm AllStar-master  
cd /srv  
cp platforms/orangepi/orangepi-allstar-asterisk-install.sh ./  
```

Remove firsttime file will stop the first login script from running:  
```
rm /etc/asterisk/firsttime  
```
Run the script and follow instructions:  
```
orangepi-allstar-asterisk-install.sh 
```
Reboot OrangePi and login 

I used a CM108B USB sound card modified for COS and PTT.

This means that channel files need to be modified.
```
cd /usr/src/astsrc-1.4.23-pre/asterisk/channels/
```
Edit chan_usbradio.c   
Edit chan_simpleusb.c   

Re-run asterisk compile:
```
cd ..
make
make install
```

Modify asterisk configuration files:
```
cd /etc/asterisk/
```
Edit modules.conf to load module chan_simpleusb  
Edit rpt.conf  
Edit usbradio.conf  
...

systemctl restart asterisk.service
