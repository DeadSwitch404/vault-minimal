# vault-ssh-harden

An Ansible role by **DeadSwitch | The Cyber Ghost**  
_"In silence, we rise. In the switch, we fade."_

## Overview

This role hardens the SSH configuration on a Linux host, enhancing security with best practices.

## Features

- Changes SSH port to a non-standard one
- Disables root login
- Configures permitted users for SSH login
- Enforces secure ciphers and protocols
- Sets login banners for legal warnings
- Restricts X11 and TCP forwarding
- Ensures proper permissions on `sshd_config`
- Ensures `sshd` is active

## Requirements

- Ansible 2.9+
- Target hosts must have `sshd` installed and running
- Tested on Debian Bookworm and Rocky 9

## Variables

- `ssh_hardening_port`: SSH port (default: `22`)
- `ssh_hardening_permitted_users`: List of allowed SSH users (default: `[]`)
- `ssh_hardening_allowed_ssh_commands`: List of allowed SSH commands (default: `[]`)

## Example Playbook

```yaml
- hosts: all
  roles:
    - vault-ssh-harden
```

## License

MIT License

## Author Information

This role is maintained by DeadSwitch | The Cyber Ghost
