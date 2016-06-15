Ubuntu Command
===============

 * [Setup Openssh Server](#setup-openssh-server)

##Setup Openssh Server
To install the OpenSSH client applications on your Ubuntu system:
<br>`$ sudo apt install openssh-client`

To install the OpenSSH server application, and related support files:
<br>`$ sudo apt install openssh-server`

[remove raid]
Q: in ubuntu usb bootdisk, harddisk not detected by installer, but detected by gparted
$sudo dmraid -E -r /dev/sda <------- remove ALL raid infor
$sudo dmraid -E -r /dev/sdb
