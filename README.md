# my-linux-kb
My Linux Knowledgebase


## Important Articles

## Important Commands

### Remotely execute commands
```
ssh user@machine 'bash -s' < local_script.sh
or you can just

 ssh user@machine "remote command to run" 
 
 ```
1. Check Weblogic patch version on Linux machine using command line

```
cd /app_bin/weblogic/w1221/wlserver/server/lib
./setEnv.sh
java weblogic.version
```

2. List all different file types in the existing directory

```
find . -type f | perl -ne 'print $1 if m/\.([^.\/]+)$/' | sort -u
```
OR
```
find . -type f | awk -F. '!a[$NF]++{print $NF}'
```

### Issues - Resolutions
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
