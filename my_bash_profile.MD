# Lunx | .bash_profile - sample

```sh

# .bash_profile

# Get the aliases and functions
if [ -f ~/.bashrc ]; then
        . ~/.bashrc
fi

# User specific environment and startup programs

PATH=$PATH:$HOME/.local/bin:$HOME/bin:.

export PATH
clear
printf "\n su OR sudo su - To any of the below service accounts\n"
ls -lart ~/.. | awk '{print $3}' | grep username*
printf "\n"
printf "\nServer Operating System\n"
cat /proc/version
rpm -qa --last |grep kernel-devel

printf "\nCPU Number\n"
cat /proc/cpuinfo | grep processor | wc -l
printf "\nMemory Details\n"
cat /proc/meminfo | grep Mem
printf "\nKernel Parameter Set\n"
cat /etc/sysctl.conf | grep "kernel.pid_max"
printf "\n Mounts Related to MyApplication\n"
df -h| head -1;df -h | egrep "opt|home|app; df -h /export/home"

printf "\n"
who
printf "\n"

echo "Enter the number of the User to sudo su - :"
PS3="Your choice: "

serviceaccountlist=$(ls -lart ~/.. | awk '{print $3}' | grep username* | grep -v "username1\|username2\|username3")
select FILENAME in $serviceaccountlist;
do
  case $FILENAME in
        "$QUIT")
          echo "Exiting."
          break
          ;;
        *)
          echo "You picked $FILENAME ($REPLY)"
          sudo su - "$FILENAME"
          ;;
  esac
done


```sh
