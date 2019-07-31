# Linux Issues Resolutions

- 1. cannot open display localhost:10.0 
```
Update /etc/ssh/sshd_config on you Local Host with below
X11Forwarding yes
#X11DisplayOffset 10
X11UseLocalhost yes

Connect to Remote Host Using
ssh -X user@remotehostname.domain

Set Display on Remote Host
export DISPLAY="<ip address of localhost>:10.0"

Test If x11 Forwarding is working
execute command
xclock
This should popup manual clock's dial on you localhost screen
```
