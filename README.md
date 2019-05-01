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
cd /app_bin/weblogic/w1221/wlserver/server/lib
./setEnv.sh
java weblogic.version
