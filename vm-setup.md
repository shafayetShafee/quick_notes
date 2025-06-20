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
