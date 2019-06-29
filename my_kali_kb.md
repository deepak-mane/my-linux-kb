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
