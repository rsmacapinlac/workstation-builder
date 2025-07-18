# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is an Ansible-based workstation builder that automates Linux system configuration and software installation. It works in conjunction with a separate `dots` repository for complete workstation setup.

## Architecture

The repository is organized by distribution with separate configurations for different Linux distros:

- **arch/**: Arch Linux configurations and playbooks
- **debian/**: Debian-based system configurations  
- **roles/**: Ansible roles organized by functional areas
  - `system/`: Base system configuration, security, users
  - `workstation/`: AUR packages, dotfiles integration
  - `development/`: Development tools, editors, programming languages
  - `applications/`: Desktop applications (browsers, media, productivity)
  - `desktop/`: Window manager, fonts, terminal configuration
  - `maintenance/`: System maintenance and update tasks
- **inventory/**: Ansible inventory files defining target hosts
- **galaxy/**: External Ansible roles and collections
- **bin/**: Helper scripts and utilities

## Common Development Commands

### Initial Setup
```bash
# Install Ansible and dependencies
bin/ansible-init.sh

# Install required Ansible collections and roles
ansible-galaxy role install --force --roles-path galaxy/roles -r galaxy/requirements.yml
ansible-galaxy collection install --force --collections-path galaxy/collections -r galaxy/requirements.yml
```

### Running Playbooks

**Arch Linux:**
```bash
cd arch/
ansible-playbook core.yml -K                    # Main system setup
ansible-playbook core.yml -K -vv               # With verbose output
ansible-playbook maintenance.yml -K             # System maintenance
```

**Debian/Ubuntu:**
```bash
cd debian/
ansible-playbook core.yml -K                    # Main system setup
ansible-playbook maintenance.yml -K             # System maintenance
```

### Testing and Development
```bash
# Test with increased verbosity for debugging
ansible-playbook core.yml -K -vv

# Run specific roles by targeting specific tags or limiting to certain tasks
ansible-playbook core.yml -K --tags "development"

# Check what would be changed without making changes
ansible-playbook core.yml -K --check --diff
```

## Key Configuration Files

- **ansible.cfg**: Ansible configuration with custom settings for inventory, roles path, and SSH behavior
- **inventory/desktop.yml**: Defines target hosts (typically localhost for workstation setup)
- **core.yml**: Main playbook that orchestrates all roles for complete system setup
- **maintenance.yml**: Playbook for ongoing system maintenance tasks

## Relationship with External Repositories

This repository handles system-level configuration and package installation, while the companion `dots` repository manages user-specific dotfiles and application configurations. The typical workflow is:

1. Run workstation-builder for system setup
2. Reboot system
3. Run dots repository (`rcup`) for user configuration

## Development Notes

- All roles use the standard Ansible role structure (tasks/, files/, templates/, etc.)
- Local connections are used (ansible_connection: local) for workstation setup
- SSH key checking is disabled for development convenience
- Facts caching is enabled using JSON files for performance
- The repository supports both Arch Linux and Debian-based distributions with separate configurations