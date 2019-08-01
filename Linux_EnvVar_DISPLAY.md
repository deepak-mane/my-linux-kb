# X11 - DISPLAY (environment variable)
[SSH (Secure Shell) - Remote Access >  X Windows System (commonly X or X11)](https://gerardnico.com/ssh/x11/display)

The magic word in the X window system is DISPLAY.

The DISPLAY environment variable instructs an X client which X server it is to connect to by default.

The X display server install itself normally as display number 0 on your local machine. In Putty, the “X display location” box reads localhost:0 by default.

A display consists (simplified) of:
- a keyboard,
- a mouse
- and a screen.

A display is managed by a server program, known as an X server. The server serves displaying capabilities to other programs that connect to it.

The remote server knows where it have to redirect the X network traffic via the definition of the DISPLAY environment variable which generally points to an X Display server located on your local computer.

The SSH protocol has the ability to securely forward X Window System applications over an encrypted SSH connection, so that you can run an application on the SSH server machine and have it put its windows up on your local machine without sending any X network traffic in the clear. $DISPLAY on the remote machine should point to localhost. SSH does the forwarding.

### 2. Articles Related
- [X Windows System (commonly X or X11)](https://gerardnico.com/ssh/x11/x11)
- [X11 - How to display remote clients (such as firefox, installation screen) with the X Server CygwinX ?]()
- [X11 - X Server (X-Windows, X Display Server)](https://gerardnico.com/ssh/x11/x_server)
- [X11 - X11 and su: How to ?](https://gerardnico.com/ssh/x11/x11_su)

### 3 - Syntax: The environment variable
    - 3.1 - Value
The value of the display environment variable is:

hostname:D.S
where:

hostname is the name of the computer where the X server runs. An omitted hostname means the localhost.
D is a sequence number (usually 0). It can be varied if there are multiple displays connected to one computer.
S is the screen number. A display can actually have multiple screens. Usually there's only one screen though where 0 is the default.
3.2 - Example of values
localhost:4
gerardnico.com:0
:0.0
hostname:D.S means screen S on display D of host hostname; the X server for this display is listening at TCP port 6000+D.
host/unix:D.S means screen S on display D of host host; the X server for this display is listening at UNIX domain socket /tmp/.X11-unix/XD (so it's only reachable from host).
:D.S is equivalent to host/unix:D.S, where host is the local hostname.

### 4 - Management: How to set the DISPLAY variable
    - 4.1 - With Putty
Generally you are using the putty terminal to connect.


More See Cygwin and Putty

    - 4.2 - In the console
Setting the DISPLAY variable, depend of your shell

Bourne, Bash or Korn shell:
$ export DISPLAY=localhost:0.0      
C shell
% setenv DISPLAY localhost:0.0
In this example, local_host is the host name or IP address of the local computer that you want to use to display for instance an installation screen such as Oracle Universal Installer.

    - 4.3 - For a sudo session
In a sudo session (you log on to a host as a non-root user and then create a sudo session to perform administrative functions)

If you do this remotely, multiple credentials may be used. If you simply try sudo xterm, it won’t work, because the xterm is running as root, but root doesn’t have the proper X11 authentication to connect to the X server machine.

To run an X11-based tool, you need to set the proper X credentials in the sudo session by fixing the xauth profile for root.

So copy the following in your root .bash_profile, substituting your logon username for adminuser:

su - adminuser -c 'xauth list' |\
 grep `echo $DISPLAY |\
 cut -d ':' -f 2 |\
 cut -d '.' -f 1 |\
 sed -e s/^/:/` |\
 xargs -n 3 xauth add



### X client forwarded over SSH “cannot open display: localhost:11.0”
<b>Solution:</b>
This is the very basic way of how it should work:

On the client / local machine (Xorg installed on client) try this:

$ xhost +
access control disabled, clients can connect from any host
Later try:

$ ssh -AY user@host xterm
or

$ ssh -AX user@host xterm
With non standard clients xhost may be needed.

If it doesn't resolve try below


Follow these steps to create a $HOME/.Xauthority file.

Log in as user and confirm that you are in the user's home directory.

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
