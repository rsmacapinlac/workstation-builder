# workstation-builder

# Prerequisites Setup

- Install the OS (assume debian)
- Ensure OpenSSH server
    - PermitRootLogin yes (debian)
    - PasswordAuthentication yes (debian)
- Set static IP (https://www.cyberciti.biz/faq/add-configure-set-up-static-ip-address-on-debianlinux/)

- Install git, sudo and then add your user to the sudoers

```
apt install -y git sudo
usermod -aG sudo [username]
```


- REBOOT!

- SSH into the terminal

```
ssh [username]@[ip_address]
```

- Move over your ID's and make it easier to login

```
ssh-copy-id -i ~/.ssh/id_rsa.pub [username]@[ip_address]
scp ~/.ssh/id_rsa* [username]@[ip_address]:~/.ssh
```

## Setup

- Create 'workspace' folder and clone core repos

```
mkdir ~/workspace && cd ~/workspace
git clone git@github.com:rsmacapinlac/workstation-builder.git
git clone git@github.com:rsmacapinlac/dots.git
git clone git@github.com:rsmacapinlac/wallpapers.git
git clone git@github.com:rsmacapinlac/cautious-dollop.git ~/.password-store
```

- Setup core stuff

```
cd ~/workspace/workstation-builder
bin/ansible-init.sh
ansible-playbook core.yml -K
```

- Reboot!

- Setup dot files

```
cd ~/workspace/dots && rcup
```

- Run wal for the first time (to remove initial Error)

```
wal -i ~/workspace/wallpapers/Generic
```
