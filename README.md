# ansible-pi

Ansible project for automated deployment and configuration of a Transmission torrent daemon on a Raspberry Pi 5.

## Stack

- **Ansible** — provisioning and configuration management
- **Transmission** — headless torrent daemon (`transmission-daemon`)
- **Raspberry Pi 5** (Debian-based) — target host
- **External NTFS drive** — mounted storage for downloads

## Project Structure
```bash
.
├── ansible.cfg
├── inventory.yaml          # host definitions
├── inventory_secrets.yaml  # credentials (not tracked in git)
├── group_vars/
│   ├── all.yaml
│   └── pi.yaml             # Pi-specific vars
├── playbook.yaml
├── uninstall.yaml
└── roles/
└── transmission/
├── defaults/       # role defaults
├── handlers/       # service restart handler
├── tasks/          # installation + config tasks
└── templates/
└── settings.json.j2  # Transmission config template
```
## Features

- Idempotent role-based deployment
- Jinja2-templated `settings.json` with configurable download paths and ports
- systemd service override support
- NTFS volume support with correct uid/gid mapping
- Secrets separated from inventory (not committed to VCS)

## Usage

```bash
# Deploy Transmission
ansible-playbook playbook.yaml

# Remove Transmission
ansible-playbook uninstall.yaml
```

## Requirements

- Ansible 2.12+
- SSH access to target host
- `inventory_secrets.yaml` with `ansible_password` and `ansible_become_password`