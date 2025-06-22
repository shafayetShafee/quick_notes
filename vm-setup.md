## SSH login setup

First install ssh on the VM

```bash
sudo apt update
sudo apt install -y openssh-server
```

Check ssh status

```bash
sudo systemctl status ssh
```

if not active, enable it

```bash
sudo systemctl enable sshsudo systemctl enable ssh
sudo systemctl start ssh
sudo systemctl start ssh
```

Now you need to generate ssh key pair, to login VM without password. At first check if public key already exists on the host machine. Run the following on the host machine,

```
ls ~/.ssh/id_rsa.pub
```

if not, generate one,

```
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

Then run the following on host machine,

```
ssh-copy-id vm-name@vm-ip-address
```

this will add the public key from your host machine to your VM ssh authorized_keys.


## Set a static IP for VM

Create a new yml file for netplan,

```bash
sudo vim /etc/netplan/99-static-ip.yaml
```

and add these,

```yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    enp0s3:  # Replace with your actual interface name
      dhcp4: no
      addresses:
        - 192.168.0.104/24
      gateway4: 192.168.0.1
      nameservers:
        addresses: [8.8.8.8, 8.8.4.4]
```

then, save and apply,

```bash
sudo netplan apply
```


## User Group Setup

check the existing user on VM list using

```bash 
ls /home
```

create a new user (say john-doe)

```bash 
sudo adduser john-doe
```

check whether the user have sudo power

```bash 
groups john-doe
```

if the output list `sudo` then the user have sudo power.

Now, we need to enable ssh login for new user. Just get the ssh public key from john and add it in `/home/john/.ssh/authorized_keys`.

now change the file properties of authorized_keys file

```bash
sudo chwon root:root /home/john-doe/.ssh/authorized_keys
sudo chmod 644 /home/john-doe/.ssh/authorized_keys
sudo chattr +i /home/john-doe/.ssh/authorized_keys
```

the last command made the file immutable, even for root. To make the file writable in future (say adding new keys for john-doe), we need to remove the i flag.

```bash
sudo chattr -i /home/john-doe/.ssh/authorized_keys
```


## Creating User Group

Its better to create a user group also, 

```bash
sudo groupadd dbt
```

and then add the new user to the group,

```bash
sudo usermod -aG dbt john-doe
```

check the groups for user `john-doe`

```bash
sudo groups john-doe
```

## Setting up SSH for a user

run the following in VM

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

this will generate ssh key in the user home directory, i.e. `/home/john-doe/.ssh/`. 

If you are using a legacy system that doesn't support the Ed25519 algorithm, use:

```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

Now start the ssh agent in backgroud and add the ssh key to ssh agent,

```bash
eval "$(ssh-agent -s)"
```

```bash
ssh-add ~/.ssh/id_ed25519
```

And add the content of `~/.ssh/id_ed25519.pub`  in Github.

For details, see [here](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent?platform=linux)

NOTE: The above steps make sure that only the user specifically can use ssh to maintain git connection with githeub, not others (NOT EVEN THE `root` user). It's because the ssh key resides into a specific home directory.


## Setting up git repo in /opt directory

`/opt` is standard on Linux systems for optional, third-party, or custom-installed software/projects. It’s outside user home directories — makes it feel like part of system-managed resources - which will be used across users or services (e.g., cron, dbt-user, systemd tasks, etc.) 

Now at first git clone the repository in a user home directory for whom ssh setup is complete,

```bash
pwd 
# output: /home/john-doe
```

```bash
git clone git@github:shafayetShafee/<repo>
```

Then move the directory to `/opt/`, make `john-doe` owner of the director so that john-doe can do git-pull-push and change the file mode,

```bash
sudo mv dbt-demo-project /opt/
sudo chown -R john-doe:dbt /opt/dbt-demo-project
sudo chmod -R 2750 /opt/dbt-demo-project
```

- 2 in 2750 = setgid: ensures new files inherit the dbt group

- 7 = owner: read/write/execute

- 5 = group: read/execute

- 0 = others: no access


NOTE: `chmod -R 2750` will affect the git file tracking, since it changes the file mode. Hence git will consider all contents as git-modified. To tell git, not to set alarm for file mode change, run,

```bash
git config core.fileMode false
```

## Installing python uv in VM

One easy way to install uv system-wide is by using `snap` in Debian.

At first install snap,

```bash
sudo apt update
sudo apt install snapd
```

After this, install the snapd snap in order to get the latest snapd:

```bash
sudo snap install snapd
```

then To install uv, simply use the following command,

```bash
sudo snap install astral-uv --classic
```

## Copying files to VM using SCP

```bash
scp -r from-directory john-doe@192.168.0.104:/to-directory/
```


## Setting up Cron Job

check the list of cronjobs for current user

```bash
crontab -l
```

you can check the list of cronjobs of other user

```bash
sudo crontab -u john-doe -l
```

Before adding a command in cronjob, its better to everything in a bash file and make the bash file executable, which makes cronjob statment compact and cleaner.

```bash
chmod +x /path-to-bash-file.sh
```

Then to edit (add or modify) the current user cronjobs,

```bash
crontab -e
```

```bash
sudo crontab -e -u john-doe
```

Add the following to run the bash file at every 20 mins,

```bash
*/20 * * * * /opt/project/run.sh >> /opt/project/logs/cron_$(date +\%F).log 2>&1
```

NOTE: In cronjobs `%` needs to escaped using `\`.