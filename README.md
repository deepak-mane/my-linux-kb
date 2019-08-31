# my-linux-kb
My Linux Knowledgebase


## Important Articles

## Important Commands
- To add user to sudoer list and without password
```
#Add Below line 
root@cplusdevenv:~# vi /etc/sudoers.d
sysadmin      ALL=(ALL) NOPASSWD:ALL
```


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


### Powerful commnds:
1. Linux: Recursive file searching with grep -r (like grep + find) [Reference](https://alvinalexander.com/linux)
```
find . -type f -exec grep -l 'mane' {} \;
```
This command can be read as, “Search all files in all subdirectories of the current directory for the string ‘mane’, and print the filenames that contain this pattern.” It’s an extremely powerful approach for recursively searching files in all subdirectories that match the pattern I specify.


