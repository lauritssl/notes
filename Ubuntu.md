##Fix network driver in Virtual box for local ssh

Edit the file: `/etc/network/interfaces`

Insert the following:

```
allow-hotplug eth1
iface eth1 inet dhcp
```

##Docker in Ubuntu

Start out by installing docker

`sudo apt-get install docker.io`

Run the following command to add user to group:

`sudo gpasswd -a ${USER} docker`

Check if you have been added to the docker group:

`cat /etc/group`

**Reboot** the machine, and chech that you are in the group again by running the `groups` command.

And you are redy to go!

##Change color in terminal

Edit the bash file: `~/.bashrc`

Locate the commented `#force_color_prompt=yes` and uncomment it out eg. `force_color_prompt=yes`

Save the file and open the terminal, the color should now have been change to light green.

To change the colors, locate the following part of in the `~/.bashrc` file:

```
if [ "$color_prompt" = yes ]; then
PS1='${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;31m\]\w\[\033[00m\]\$ '
else
PS1='${debian_chroot:+($debian_chroot)}\u@\h:\w\$ '
fi
```

Change where it says `1;32m` to one of the following colors:

```
Black 0;30 – Dark Gray 1;30 – Blue 0;34 – Light Blue 1;34 – Green 0;32 – Light Green 1;32 – Cyan 0;36 – Light Cyan 1;36 – Red 0;31 – Light Red 1;31 – Purple 0;35 – Light Purple 1;35 – Brown 0;33 – Yellow 1;33 – Light Gray 0;37 – White 1;37

```

##Keep terminal running while logout

You should use the `screen` command.

Start screen session: `screen`

Log out of session: `ctrl+a d`

Get into running session: `screen -r`

Switch between multiply sessions: `ctrl+a n`
