---
title: "Solve grey screen and X pointer problem of vncviewer on Ubuntu"
categories: Engineer
date: 2017-02-21 13:49
tag:
- ubuntu
- vnc
---

After setting up successfully the vncserver on your Ubuntu machine, a common problem is the grey screen and "X" pointer in vncviewer.

This problem is caused by there is no desktop running while running the vncserver, so there is going to show nothing. A simple solution is to edit the file `~/.vnc/xstartup` by simply replacing the content with
    
    #!/bin/sh 
    # Uncomment the following two lines for normal desktop:
    # unset SESSION_MANAGER
    # exec /etc/X11/xinit/xinitrc

    [ -x /etc/vnc/xstartup ] && exec /etc/vnc/xstartup
    [ -r $HOME/.Xresources ] && xrdb $HOME/.Xresources

    xsetroot -solid grey 
    vncconfig -iconic &
    x-terminal-emulator -geometry 80x24+10+10 -ls -title "$VNCDESKTOP Desktop" &
    x-window-manager &
    mate-session &

At last, run `(sudo) chmod 777 ~/.vnc/xstartup` to change the previlege. Then the problem is solved.

Here we introduce some common *vncserver commands*:

- Create a connection: `vncserver`
    + -geometry 1920x1200: the resolution of desktop in vncviewer will be 1920x1200
This will return a connection address with a port number.
- Delete a connection: `vncserver -kill :PORT_NUMBER`
- List all vnc connections: `ps -ef | grep vnc`

The PID of each connection will be stored in `~/.vnc/xxxxx:x.pid` file, **DO NOT** delete .pid file unless you want to kill the connection by yourself.

### The following procedure is expecially for connecting computers in VML lab via VNC outside campus

1. `ssh -L 5901:cs-vml-ID_OF_MACHINE.cs.sfu.ca:5901 USER_ID@rcg-linux-ts1.rcg.sfu.ca` and enter your password to make
an SSH tunnel.
2. In your VNC client software, connect to 127.0.0.1:1.
3. If port 5901 is occupied, try `5902` and `127.0.0.1:2` till you successfully connect.









