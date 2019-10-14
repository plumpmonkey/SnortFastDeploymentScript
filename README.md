# Snort Fast Deployment Script

## What it is, and why/when to use it

SFDS is an UNOFFICIAL deployment script for Snort 2.9.15. If other scripts, more advance then this one, will install snort but you will need to configure it and add your own rules, "SFDS" will not only install Snort but will place some basic rules in place so you can immediately start your security system.

This script can be very useful for the fallowing:
 > Learning Purposes (you what to learn more about security, and Snort is your choice)

>Home fast security. (you will like to try Snort for some extra protection and you have an old laptop/pc to spare/dedicate)



   
# Installation

## Get the files
Simply create a working folder then clone this git.

```bash
sudo mkdir your-folder
cd your-folder
sudo git clone https://github.com/WillyWeiss/SnortFastDeploymentScript.git
sudo tar xvfz sourcecode.tar.gz
```

## Use the installer

```
sudo chmod +x SFDS
sudo ./SFDS
```


# Use the Snort Software



If you are not sure which interface to use, check for the public IPv4 address of your server in the Network settings. You can also use the following commands on your server according to your distribution.

```
### IF you use IFCONFIG
ifconfig 

### Or if you use IP
ip addr
```
Once you know your ethernet card that you will like to moniotor, just run the below command, replacing ```eth0``` with your own card.

```
sudo snort -A console -i eth0 -u snort -g snort -c /etc/snort/snort.conf
```

# USE SNORT IN BACKGROUND (AFTER YOU DECIDE ON WHAT CARD TO RUN)
To run Snort on Debian/Ubuntu as a service in the background you will need to add a startup script for Snort. Open a new a file in a text editor for example with the next command.


```
sudo nano /lib/systemd/system/snort.service
```
Enter the following to the file, save and exit the editor and CHANGE your Ethernet card accordingly.
```
[Unit]
Description=Snort NIDS Daemon
After=syslog.target network.target

[Service]
Type=simple
ExecStart=/usr/local/bin/snort -q -u snort -g snort -c /etc/snort/snort.conf -i eth0

[Install]
WantedBy=multi-user.target
```
With the service defined, reload the systemctl daemon.

```
sudo systemctl daemon-reload
```


Snort can then be run with the configuration you set up using the command below.
```
sudo systemctl start snort
```


The startup script also includes other usual systemctl commands: 
>stop

> restart

> status 

For example, you can check the status of the service with the following command.




```
sudo systemctl status snort
```

## Full List of included rules (NOT UP TO DATE BUT FUNCTIONAL)
 ```
tree legendary
|
├── preproc_rules                                                                                                                              
│   ├── decoder.rules                                                                                                                          
│   ├── preprocessor.rules                                                                                                                     
│   └── sensitive-data.rules
├── rules
│   ├── app-detect.rules
│   ├── attack-responses.rules
│   ├── backdoor.rules
│   ├── bad-traffic.rules
│   ├── blacklist.rules
│   ├── botnet-cnc.rules
│   ├── browser-chrome.rules
│   ├── browser-firefox.rules
│   ├── browser-ie.rules
│   ├── browser-other.rules
│   ├── browser-plugins.rules
│   ├── browser-webkit.rules
│   ├── cgi-bin.list
│   ├── chat.rules
│   ├── content-replace.rules
│   ├── ddos.rules
│   ├── deleted.rules
│   ├── dns.rules
│   ├── dos.rules
│   ├── experimental.rules
│   ├── exploit-kit.rules
│   ├── exploit.rules
│   ├── file-executable.rules
│   ├── file-flash.rules
│   ├── file-identify.rules
│   ├── file-image.rules
│   ├── file-java.rules
│   ├── file-multimedia.rules
│   ├── file-office.rules
│   ├── file-other.rules
│   ├── file-pdf.rules
│   ├── finger.rules
│   ├── ftp.rules
│   ├── icmp-info.rules
│   ├── icmp.rules
│   ├── imap.rules
│   ├── indicator-compromise.rules
│   ├── indicator-obfuscation.rules
│   ├── indicator-scan.rules
│   ├── indicator-shellcode.rules
│   ├── info.rules
│   ├── local.rules
│   ├── Makefile.am
│   ├── malware-backdoor.rules
│   ├── malware-cnc.rules
│   ├── malware-other.rules
│   ├── malware-tools.rules
│   ├── metasploit_payloads.rules
│   ├── misc.rules
│   ├── multimedia.rules
│   ├── mysql.rules
│   ├── netbios.rules
│   ├── nntp.rules
│   ├── open-test.conf
│   ├── oracle.rules
│   ├── os-linux.rules
│   ├── os-mobile.rules
│   ├── os-other.rules
│   ├── os-solaris.rules
│   ├── os-windows.rules
│   ├── other-ids.rules
│   ├── p2p.rules
│   ├── phishing-spam.rules
│   ├── policy-multimedia.rules
│   ├── policy-other.rules
│   ├── policy.rules
│   ├── policy-social.rules
│   ├── policy-spam.rules
│   ├── pop2.rules
│   ├── pop3.rules
│   ├── protocol-dns.rules
│   ├── protocol-finger.rules
│   ├── protocol-ftp.rules
│   ├── protocol-icmp.rules
│   ├── protocol-imap.rules
│   ├── protocol-nntp.rules
│   ├── protocol-other.rules
│   ├── protocol-pop.rules
│   ├── protocol-rpc.rules
│   ├── protocol-scada.rules
│   ├── protocol-services.rules
│   ├── protocol-snmp.rules
│   ├── protocol-telnet.rules
│   ├── protocol-tftp.rules
│   ├── protocol-voip.rules
│   ├── pua-adware.rules
│   ├── pua-other.rules
│   ├── pua-p2p.rules
│   ├── pua-toolbars.rules
│   ├── rpc.rules
│   ├── rservices.rules
│   ├── scada.rules
│   ├── scan.rules
│   ├── server-apache.rules
│   ├── server-iis.rules
│   ├── server-mail.rules
│   ├── server-mssql.rules
│   ├── server-mysql.rules
│   ├── server-oracle.rules
│   ├── server-other.rules
│   ├── server-samba.rules
│   ├── server-webapp.rules
│   ├── shellcode.rules
│   ├── smtp.rules
│   ├── snmp.rules
│   ├── specific-threats.rules
│   ├── spyware-put.rules
│   ├── sql.rules
│   ├── telnet.rules
│   ├── tftp.rules
│   ├── virus.rules
│   ├── VRT-License.txt
│   ├── web-activex.rules
│   ├── web-attacks.rules
│   ├── web-cgi.rules
│   ├── web-client.rules
│   ├── web-coldfusion.rules
│   ├── web-frontpage.rules
│   ├── web-iis.rules
│   ├── web-misc.rules
│   ├── web-php.rules
│   └── x11.rules
└── so_rules
    ├── bad-traffic.rules
    ├── chat.rules
    ├── dos.rules
    ├── exploit.rules
    ├── icmp.rules
    ├── imap.rules
    ├── misc.rules
    ├── multimedia.rules
    ├── netbios.rules
    ├── nntp.rules
    ├── p2p.rules
    ├── pop3.rules
    ├── smtp.rules
    ├── sql.rules
    ├── web-activex.rules
    ├── web-client.rules
    ├── web-iis.rules
    └── web-misc.rules
```
