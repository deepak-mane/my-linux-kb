# Linux Issues Resolutions

  1. <b>Cannot open display localhost:10.0</b> 
```
Troubleshoot:
First: Find remote host variable set DISPLAY value
ssh -X user@remotehostname.domain env|grep DISPLAY

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

 2.<b>ON UBUNTU : CMake not found, yet it is installed</b>
 
Download  the script from [CMake's Download Page](https://cmake.org/download/). 
The documentation how to use it is admittedly a little sparse.

In short, call (installation path for CMake here is /usr/local):
```
# sudo cmake-3.11.3-Linux-x86_64.sh --skip-license --exclude-subdir --prefix=/usr/local
Note: You need to uninstall any package manager installed CMake packages first

# sudo apt remove cmake
# sudo apt purge --auto-remove cmake
Options

The script has the following options:

# cmake-3.11.3-Linux-x86_64.sh --help
Usage: cmake-3.11.3-Linux-x86_64.sh [options]
Options: [defaults in brackets after descriptions]
  --help            print this message
  --version         print cmake installer version
  --prefix=dir      directory in which to install
  --include-subdir  include the cmake-3.11.3-Linux-x86_64 subdirectory
  --exclude-subdir  exclude the cmake-3.11.3-Linux-x86_64 subdirectory
  --skip-license    accept license
The one you are searching for is --prefix=dir. Otherwise it will just use the current 
directory to extract the installation files.

Test Output on Ubuntu

# cmake-3.11.3-Linux-x86_64.sh --skip-license --exclude-subdir --prefix=/usr/local
CMake Installer Version: 3.11.3, Copyright (c) Kitware
This is a self-extracting archive.
The archive will be extracted to: /usr/local

Using target directory: /usr/local
Extracting, please wait...

Unpacking finished successfully

# cmake --version
cmake version 3.11.3

CMake suite maintained and supported by Kitware (kitware.com/cmake).
Reference / Alternative
```

Updating CMake from 2.8.11 to 3.6.2 or Newer Version on CentOS Linux
On CentOS 7, using yum install gives you cmake version 2.8.11
[root@thrift1 ~]# cat /etc/*release
CentOS Linux release 7.2.1511 (Core)

[root@thrift1 ~]# yum info cmake
Installed Packages
Name        : cmake
Arch        : x86_64
Version     : 2.8.11


In order to install version 3.6.2 or newer version, first uninstall it with yum remove
[root@thrift1 ~]# sudo yum remove cmake -y
If you don't perform the above step to remove old CMake version, you may see below error after the final step that you installed the newer CMake version.
CMake has most likely not been installed correctly

Download, extrace, compile and install the code cmake-3.6.2.tar.gz from https://cmake.org/download/
[root@thrift1 testdelete]# wget https://cmake.org/files/v3.6/cmake-3.6.2.tar.gz
[root@thrift1 testdelete]# tar -zxvf cmake-3.6.2.tar.gz
[root@thrift1 testdelete]# cd cmake-3.6.2
[root@thrift1 cmake-3.6.2]# sudo ./bootstrap --prefix=/usr/local
[root@thrift1 cmake-3.6.2]# sudo make
[root@thrift1 cmake-3.6.2]# sudo make install
[root@thrift1 cmake-3.6.2]# vi ~/.bash_profile
PATH=/usr/local/bin:$PATH:$HOME/bin
[root@thrift1 ~]# cmake --version
cmake version 3.6.2


Ask Ubuntu: How do I install the latest version of cmake from the command line?
```
sudo -E add-apt-repository -y ppa:george-edison55/cmake-3.x
sudo -E apt-get update
sudo apt-get install cmake
```
 3.<b>ON UBUNTU : Launch Failed. Binary not found. CDT on Eclipse Neon</b>
Go to the Run->Run Configuration-> now

Under C/C++ Application you will see the name of your executable + Debug (if not, click over C/C++ Application a couple of times). Select the name (in this case projectTitle+Debug).

Under this in main Tab -> C/C++ application -> Search your project -> in binaries select your binary titled by your project....


 4.<b>ON UBUNTU : How do I create the .Xauthority file?</b>

Follow these steps to create a $HOME/.Xauthority file.

Log in as user and confirm that you are in the user's home directory.
```
# Rename the existing .Xauthority file by running the following command
mv .Xauthority old.Xauthority 

# xauth with complain unless ~/.Xauthority exists
touch ~/.Xauthority

# only this one key is needed for X11 over SSH 
xauth generate :0 . trusted 

# generate our own key, xauth requires 128 bit hex encoding
xauth add ${HOST}:0 . $(xxd -l 16 -p /dev/urandom)

# To view a listing of the .Xauthority file, enter the following 
xauth list 
After that no more problems with .Xautority file since then.
```
