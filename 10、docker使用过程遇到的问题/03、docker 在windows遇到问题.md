<>
# docker 在windows遇到问题


[WSL2- Ubuntu 20.04 Snap store doesn't work due to systemd dependency](https://github.com/microsoft/WSL/issues/5126)

```bash
sudo apt-get update && sudo apt-get install -yqq daemonize dbus-user-session fontconfig
sudo daemonize /usr/bin/unshare --fork --pid --mount-proc /lib/systemd/systemd --system-unit=basic.target
exec sudo nsenter -t $(pidof systemd) -a su - $LOGNAME

snap version
```

