# WSL Stuffs

## How to add new user

### as a root user

open the `command-prompt` or `powershell` or even `git-bash` from windows terminal and run the following,

```
$ ubuntu config --default-user root
```

which basically sets the `root` user as default so that if I open ubuntu, it would open with root user.

So then, open the `ubuntu-wsl-terminal` and run the following,

```
root$ adduser <username>
```

for example,

```
adduser stat-noob
```

which then will prompt for new password and give it. It will also prompt for a few additional info like, full name, Room number, work phone, home phone, other. You may ignore them, by pressing `<Enter>`. Then press `Y` for confirmation.

Then logout the terminal with `logout` command and run the following from `cmd` or `powershell` or `git-bash`,

~~~
ubuntu config --default-user stat-noob
~~~


Now opening the `ubuntu-wsl` again will open as the user `stat-noob`


### as a sudo user

open the `ubuntu-wsl` terminal and run the following,

```
sudo adduser <new-user>
```

it will prompt for password and othe some optional info as described above. Give them and then press Y for confirmation. Done!
