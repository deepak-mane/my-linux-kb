# my_kali_kb

### My Learnings about Kali

In
server's /etc/ssh/sshd_config:
To enable password authentication, uncomment
```
#PasswordAuthentication yes
```
To enable root login, uncomment
```
#PermitRootLogin yes
```
To enable ssh key login, uncomment
```
#PubkeyAuthentication yes
#AuthorizedKeysFile .ssh/authorized_keys
```
