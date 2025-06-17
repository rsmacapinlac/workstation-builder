# Workstation Builder - Ritchie's System Configuration

This repository contains Ansible playbooks and roles for setting up a complete Linux workstation. It works in conjunction with the [dots](https://github.com/rsmacapinlac/dots) repository to provide a complete workstation setup.

## Overview

The `workstation-builder` repository:
- Uses Ansible for automated system configuration
- Handles system-level setup and package installation
- Configures system-wide settings and services
- Sets up development environments and tools
- Works with dots repository for user-specific configurations

## Relationship with dots

These repositories work together in the following way:

1. **workstation-builder** (this repo): Handles the initial system setup, including:
   - Installing required packages and dependencies
   - Setting up system-wide configurations
   - Installing development tools and utilities
   - Configuring system services
   - Setting up base system requirements

2. **dots**: Manages user-specific configurations:
   - Application-specific dotfiles
   - User-level customizations
   - Personal preferences and settings
   - Theme and appearance configurations

## Prerequisites Setup

### For a Completely Blank System (Debian)

1. Install the OS (assume debian)
2. Configure OpenSSH server:
   - Set `PermitRootLogin yes` (debian)
   - Set `PasswordAuthentication yes` (debian)
3. Set static IP (https://www.cyberciti.biz/faq/add-configure-set-up-static-ip-address-on-debianlinux/)

4. Install git, sudo and add your user to the sudoers:
   ```bash
   apt install -y git sudo
   usermod -aG sudo [username]
   ```

5. REBOOT!

6. SSH into the terminal:
   ```bash
   ssh [username]@[ip_address]
   ```

7. Set up SSH keys for easier login:
   ```bash
   ssh-copy-id -i ~/.ssh/id_rsa.pub [username]@[ip_address]
   scp ~/.ssh/id_rsa* [username]@[ip_address]:~/.ssh
   ```

### For Local Computer

1. Ensure that you have your private key configured for connecting to Github
2. Set correct permissions:
   ```bash
   chmod 600 ~/.ssh/id_rsa
   ```

### For Virtual Machine

Follow the same steps as the "Completely Blank System" section above.

## Setup Process

1. Create workspace folder and clone core repos:
   ```bash
   mkdir ~/workspace && cd ~/workspace
   git clone git@github.com:rsmacapinlac/workstation-builder.git
   git clone git@github.com:rsmacapinlac/dots.git
   git clone git@github.com:rsmacapinlac/cautious-dollop.git ~/.password-store
   ```

2. Setup core system:
   ```bash
   cd ~/workspace/workstation-builder
   bin/ansible-init.sh
   ansible-playbook core.yml -K
   ```

3. REBOOT!

4. Setup dot files:
   ```bash
   cd ~/workspace/dots && rcup
   ```

## Repository Structure

- `arch/`: Configuration for Arch Linux systems
- `debian/`: Configuration for Debian-based systems
- `bin/`: Helper scripts and utilities
- `roles/`: Ansible roles for different components
- `playbooks/`: Main Ansible playbooks

## Setting up pass

```bash
gpg --import your_public_key_file.pgp
gpg --allow-secret-key-import --import your_private_key_file.pgp
```

## Usage

After initial setup, you can:
- Modify playbooks to customize the installation
- Add new roles for additional software
- Update existing configurations

## Contributing

Feel free to fork this repository and adapt it to your needs. The configuration is designed to be modular and easily customizable.

## License

This project is open source and available under the MIT License.

## Setup SDDM

Currently obsessed with: https://github.com/Keyitdev/sddm-astronaut-theme/tree/master?tab=readme-ov-file
```bash
# All of the above, really like Pixel Sakura
sh -c "$(curl -fsSL https://raw.githubusercontent.com/keyitdev/sddm-astronaut-theme/master/setup.sh)"
```
```
