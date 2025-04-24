# DeadSwitch Vault Minimal - Unwanted Services

This Ansible role masks and disables legacy or unneeded services that expand the system's attack surface.

## Features

- Masks insecure or legacy services like `telnet`, `ftp`, and `xinetd`.
- Stops wireless and discovery services like `bluetooth` and `avahi-daemon`.
- Optional control via `vault_minimal_mask_services`.

## Requirements

- Ansible 2.9+
- Tested on Debian Bookworm and Rocky 9

## Variables

`vault_minimal_mask_services`: Enable/disable this role (default: `true`)
`vault_minimal_unwanted_services`: List of services to stop and mask

Default services (with justification):

```yaml
  - avahi-daemon      # Zeroconf/Bonjour service, not needed on hardened systems
  - cups              # Printing service, unnecessary on most servers
  - bluetooth         # Bluetooth is a wireless attack vector
  - rpcbind           # Used by NFS and other RPC services; often exploited
  - nfs-server        # Network File System; vulnerable and not minimal
  - smbd              # Samba file sharing service, rarely needed
  - rsyncd            # Daemon for file syncing, usually not needed persistently
  - telnet.socket     # Insecure remote access protocol
  - ftp               # Unencrypted file transfer protocol
  - xinetd            # Legacy internet super-server, obsolete
```

## Why This Matters

Disabling unneeded services is one of the fastest ways to secure a Linux system.
Each masked service is one less thing an attacker can abuse or exploit.
This role follows the Vault Minimal principle: if it doesn’t serve, it doesn’t stay.

##Example Playbook

```yaml
- hosts: all
  roles:
    - vault-services-minimal
```

## License

MIT License

## Author Information

This role is maintained by DeadSwitch | The Cyber Ghost
