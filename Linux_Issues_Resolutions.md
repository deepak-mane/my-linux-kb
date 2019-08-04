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
 
Download  the script from [CMake's Download Page](https://cmake.org/download/). The documentation how to use it is admittedly a little sparse.

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
The one you are searching for is --prefix=dir. Otherwise it will just use the current directory to extract the installation files.

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

Ask Ubuntu: How do I install the latest version of cmake from the command line?
```
