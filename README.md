```
git config user.name "kibblewhite"
git config user.email "kibblewhite@live.com"
git config --list
```

```
sudo groupadd docker
sudo chmod 666 /var/run/docker.sock
sudo chown "$USER":"$USER" /home/"$USER"/.docker -R
sudo chmod g+rwx "$HOME/.docker" -R
```

/etc/sudoers
```
> <username> ALL=(ALL) NOPASSWD:<command>
kibble ALL=(ALL) NOPASSWD:/usr/bin/dockerd
kibble ALL=(ALL) NOPASSWD:/usr/bin/tmux
kibble ALL=(ALL) NOPASSWD:ALL
```

C:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp

C:\Windows\System32\wsl.exe -e "/usr/bin/bash /home/kibble/.services/docker-daemon.sh"

```bash
# Start Docker daemon automatically when logging in if not running.
RUNNING=`ps aux | grep dockerd | grep -v grep`
if [ -z "$RUNNING" ]; then
	/usr/bin/sudo /usr/bin/tmux new-session -d -s dockerd
	/usr/bin/sudo /usr/bin/tmux send-keys -t dockerd "/usr/bin/dockerd > /dev/null 2>&1 &" ENTER;
	/usr/bin/sleep 3
	/usr/bin/sudo /usr/bin/tmux send-keys -t dockerd "/usr/bin/chmod 666 /var/run/docker.sock" ENTER;
	/usr/bin/sudo /usr/bin/tmux send-keys -t dockerd "exit" ENTER;
fi
```

```bash
/usr/bin/sudo /usr/bin/tmux new-session -d -s dockerd
/usr/bin/sudo /usr/bin/tmux send-keys -t dockerd "/usr/bin/dockerd > /dev/null 2>&1 &" ENTER;
/usr/bin/sleep 3
/usr/bin/sudo /usr/bin/tmux send-keys -t dockerd "/usr/bin/chmod 666 /var/run/docker.sock" ENTER;
```

```bash
tmux detach
sudo tmux ls
sudo tmux attach-session -t dockerd
```
