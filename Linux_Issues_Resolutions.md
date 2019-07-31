# Linux Issues Resolutions

  1. <b>Cannot open display localhost:10.0</b> 
```
Troubleshoot:
First: Find remote host variable set DISPLAY value
ssh -X user@remotehostname.domain env

Second: Update /etc/ssh/sshd_config on you Local Host with below
X11Forwarding yes
#X11DisplayOffset 10
X11UseLocalhost yes

Third: Connect to Remote Host Using
ssh -X user@remotehostname.domain

Fourth: If Display is NOT SET on Remote Host
export DISPLAY="<ip address of localhost>:10.0"

Firth: Test If x11 Forwarding is working
execute command
xclock
This should popup manual clock's dial on you localhost screen
```
