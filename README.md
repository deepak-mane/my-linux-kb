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

2. Linux find/copy FAQ: How can I use the find command to find many files and copy them all to a directory?
```
find . -type f -name "*.mp3" -exec cp {} /tmp/MusicFiles \;
find . -type f -name "*.mp3" -exec cp -n {} /tmp/MusicFiles \;

Features
-1- If you don’t want to overwrite existing files, use the cp -n command, like this:
-2- All of these files will end up in one folder.
-3- If there are duplicate file names, some of the files will be lost.
```

3. Linux find/move FAQ: How can I use the find command to find many files and move them all to a directory?
```
find . -type f -exec mv {} . \;
```
4. Linux ‘find’ example: How to copy one file to many directories
```
find dir1 dir2 dir3 dir4 -type d -exec cp header.html {} \;

Features
-1- Find command, and I tell it to look in four sub-directories (dir1, dir2, dir3 and dir4).
-2- find only directories (-type d).
-3- issue the Linux copy (cp) command, and copy the file header.html to each directory that is found, 
one directory at a time.
```


