# workstation-builder

# Prerequisites Setup

- Install the OS (assume debian)
- Ensure OpenSSH server
    - PermitRootLogin yes (debian)
    - PasswordAuthentication yes (debian)
- Set static IP (https://www.cyberciti.biz/faq/add-configure-set-up-static-ip-address-on-debianlinux/)
- scp your id_rsa file
- ssh-copy-id -i ~/.ssh/id_rsa.pub ritchie@10.1.0.21
- Install git, sudo
    - apt install git sudo
- Add user to sudoers
    - usermod -aG sudo [username]
- REBOOT!

## Setup

- Create 'workspace' folder and clone core repos

mkdir ~/workspace && cd ~/workspace
git clone git@github.com:rsmacapinlac/workstation-builder.git
git clone git@github.com:rsmacapinlac/dots.git
git clone git@github.com:rsmacapinlac/wallpapers.git
git clone git@github.com:rsmacapinlac/cautious-dollop.git ~/.password-store

- Setup core stuff

cd ~/workspace/workstation-builder
bin/ansible-init.sh

- Run the core ansible playbook

ansible-playbook core.yml -K

- Reboot!

- Setup dot files

cd ~/workspace/dots
rcup

- Run wal (to remove initial Error)

wal -i ~/workspace/wallpapers/Generic

