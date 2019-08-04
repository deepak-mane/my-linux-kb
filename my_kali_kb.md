# my_kali_kb

### My Learnings about Kali

### How to Enable and Start SSH on Kali Linux
 
The Linux distribution Kali used by many penetration testers (including those here at LMG Security) recently released version 2017.1 of their rolling release. For quite some time now (Since version 2.0) Kali has used Systemd (System Management Daemon) in place of an init system.  This change brought with it a new way of enabling and starting services, even though many still use the old commands, which often still work but may also lead to errors.  This post will go over the Systemd method for enabling and starting the SSH (Secure Shell) service on Kali Linux.

The openssh-server package should already be installed, to verify this you can use the following command:
```
# apt list openssh-server
```
You should see the version with [installed] after it like this:

If it’s not installed, you can use this command to install it:
```
# apt install openssh-server
```
When enabling the service, be sure to fully secure SSH first.  I will cover some of the basics briefly, but this is not meant to be a guide on securely running an SSH server.  Since Kali comes with pre-generated SSH keys, to make it more secure, the first thing we will do is generate new ones.

To backup the original keys first as a precaution use:
```
# mkdir /etc/ssh/default_keys
# mv /etc/ssh/ssh_host_* /etc/ssh/default_keys/
```
Then to regenerate the keys:
```
# dpkg-reconfigure openssh-server
```
The next step is to edit the SSH server configuration file with the settings you need:
```
# nano /etc/ssh/sshd_config
```
If you are only planning on using SSH briefly the defaults are probably fine.  If you think you will use it for a length of time I would recommend at minimum enabling public key authentication:
```
PubkeyAuthentication yes
```
Then disabling password authentication:
```
PasswordAuthentication no
```
You could also allow the root user login here, but instead consider creating a non-privileged user account instead.

It’s useful to know that Systemd has different units, a unit configuration file encodes information.  The units relevant to SSH are ssh.service and ssh.socket. At a basic level a service unit controls a process and a socket unit controls a filesystem or network socket.  If you only need to temporarily start up the SSH service it’s recommended to use ssh.socket:
```
# systemctl start ssh.socket
```
When finished:
```
# systemctl stop ssh.socket
```
To instead permanently enable the SSH service to start whenever the system is booted use:
```
# systemctl enable ssh.service
```
Then to use SSH immediately without having to reboot use:
```
# systemctl start ssh.service
```
To check the status of the service you can use:
```
# systemctl status ssh.service
```
To stop the SSH service use:
```
# systemctl stop ssh.service
```
And to disable the SSH service so it no longer starts at boot:
```
# systemctl disable ssh.service
```
This gives you the basics of starting and enabling the SSH service in Kali Linux.  If you are planning on using the system for any length of time I highly recommend going further with securing the SSH service. If you have any questions or comments about SSH on Kali Linux, contact us at questions@lmgsecurity.com

### If still fails after above steps make changes as below

In server's /etc/ssh/sshd_config:

- To enable password authentication, uncomment
```
#PasswordAuthentication yes
```
- To enable root login, uncomment
```
#PermitRootLogin yes
```
- To enable ssh key login, uncomment
```
#PubkeyAuthentication yes
#AuthorizedKeysFile .ssh/authorized_keys
```
### How to enable Remote Desktop connections on Kali

The following steps assumes that you have installed Kali Linux from the latest ISO and did the update procedure:
```
apt-get update && apt-get upgrade
apt-get dist-upgrade
```
In order to install the RDP server you run the following command from a terminal window:
```
apt-get install xrdp
```
After xrdp is installed you can start the server with the following command:
```
service xrdp start
Service xrdp-sesman start 
```
If want it to auto start after reboot you need to run this command also:
```
update-rc.d xrdp enable     (It will not start xrdp-sesman automatic)
```
Now you should be able to RDP directly into your Kali Linux

The only way I found that fixes this is to uninstall the Gnome-desktop and use another window manager (I use LXDE):
```
apt-get remove gnome-core
apt-get install lxde-core lxde kali-defaults kali-root-login desktop-base
update-alternatives –config x-session-manager
Choose /usr/bin/startlxde
After this you need to reboot and the RDP should work “perfectly”
```


### How to create a new normal user with sudo permission in Kali Linux
Kali Linux, the pentester’s Linux does not need an introduction. Today, I’ll show you how to create a normal user under Kali Linux. You might ask, Why would someone want to create a normal/standard user in Kali? What’s wrong with root only? Well, simply saying, being root all the time is not so good. Some applications won’t work in root. (Google chrome won’t work in root by default). If you want to use Kali as a day to day operating system, I’d suggest you to create a standard user and use it. If you want to do pentesting and stuff, you could ‘sudo’ or just log in as root.

Note: This procedure can be used in any Linux distro to add a normal user. That includes ubuntu, Linux mint, or even Centos

Here’s how you will create a normal user
Open a terminal and issue the following command.
```
useradd -m username
# -m creates a home directory for the user.
```
Now we have to set a password for the user.
```
passwd username
```
It will ask you to create a new password.

At this point, we have a new user account. But we might want to add our new user to the “sudoers” group, so that we can use “sudo” to do administrative actions.
```
usermod -a -G sudo username
The option -a means to add and ‘-G sudo’ means to add the user to the sudo group. If you want to know more about the usermod command, issue man usermod command to know more about usermod
```

Now we have to specify the shell for our new user.
```
chsh -s /bin/bash username
chsh command is used to change the login shell for a user.
```

All done.! you are all set. You could logout and login to your new account.


### KaliLinux 2017.1: Install Eclipse CDT for C/C++ development
This article will describe installing Eclipse CDT.

Table of Contents
1. Install Eclipse
2. Run Eclipse


1 Install Eclipse
Eclipse CDT in KaliLinux repository does not load CDT plugins. This article will install Eclipse CDT from Eclipse site while installing Eclipse CDT from KaliLinux repository for installing require packages.

Install Eclipse CDT from KaliLinux repository.
```
$ sudo apt install -y eclipse-cdt-*
```
Download Eclipse installer.
```
$ URL=https://www.eclipse.org/downloads/download.php
$ ECLIPSE=/oomph/epp/oxygen/R/eclipse-inst-linux64.tar.gz
$ MIRROR=1
$ wget -q -O eclipse-inst-linux64.tar.gz "${URL}?file=${ECLIPSE}&mirror_id=${MIRROR}"
$ tar zxf eclipse-inst-linux64.tar.gz
```
Run Eclipse installer.
```
$ ./eclipse-installer/eclipse-inst
Select "Eclipse IDE for C/C++ Developers".
```
0001_SelectType.png

Decide install directory and press "INSTALL".

0002_InstallationFolder.png

Accept license with pressing "Accept".

0003_AcceptLicenses.png

Accept download URL certificates with pressing "Select All" and "Accept selected".

0004_TrustCertificates.png

Eclipse installation is completed. Pressing "LAUNCH" runs Eclipse.

0005_InstallationCompleted.png

You can remove Eclipse installer.
```
$ rm -rf eclipse-inst-linux64.tar.gz eclipse-installer
```

2 Run Eclipse
Run the following command.
```
$ ./eclipse/cpp-oxygen/eclipse/eclipse
```

0006_Eclipse.png
