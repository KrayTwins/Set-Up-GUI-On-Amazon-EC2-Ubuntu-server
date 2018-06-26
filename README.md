# Set Up GUI On Amazon EC2 Ubuntu server

Information gathered from https://stackoverflow.com/questions/25657596/how-to-set-up-gui-on-amazon-ec2-ubuntu-server \


```
## Create new user with password login
$ sudo useradd -m awsgui
$ sudo passwd awsgui
$ sudo usermod -aG admin awsgui
$ sudo vim /etc/ssh/sshd_config # edit line "PasswordAuthentication" to yes
$ sudo /etc/init.d/ssh restart
```
```
# Setting up ui based ubuntu machine on AWS.
# In security group open port 5901. Then ssh to the server instance. Run following commands to install ui and vnc server:

$ sudo apt-get update
$ sudo apt-get install ubuntu-desktop
$ sudo apt-get install vnc4server
$ sudo apt-get install gnome-panel gnome-settings-daemon metacity nautilus gnome-terminal
```
```
$ su - awsgui
$ vncserver
$ ps # note pid of vncserver
$ kill -9 pid
```
```
# And use this ~/.vnc/xstartup file:
$ vim /home/awsgui/.vnc/xstartup
```
```
#######################################################################################
## replace the .vnc/xstartup file contents with this

#!/bin/sh

export XKL_XMODMAP_DISABLE=1
unset SESSION_MANAGER
unset DBUS_SESSION_BUS_ADDRESS

[ -x /etc/vnc/xstartup ] && exec /etc/vnc/xstartup
[ -r $HOME/.Xresources ] && xrdb $HOME/.Xresources
xsetroot -solid grey
vncconfig -iconic &

gnome-panel &
gnome-settings-daemon &
metacity &
nautilus &
gnome-terminal &
########################################################################################
```
```
$ reboot

#log back into EC2
$ su - awsgui
$ vncserver
```

