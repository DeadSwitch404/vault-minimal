# DeadSwitch Vault Minimal - Unsafe Packages

This Ansible role removes insecure, legacy, or unnecessary network packages that can weaken system security.

## Features

- Uninstalls risky packages like `telnet`, `ftp`, `rsh`, `netcat`, and others.
- Helps reduce your attack surface with minimal effort.
- Designed to be fast, minimal, and effective.

## Requirements

- Ansible 2.9+
- Tested on Debian Bookworm and Rocky 9

## Variables

`vault_minimal_unsafe_packages`: List of packages to be removed

Default packages (can be overridden):

``` yaml
  - telnet
  - rsh
  - rlogin
  - ypbind
  - tftp
  - talk
  - xinetd
  - vsftpd
  - ftp
  - samba
  - nfs-utils
  - netcat
```

## Why Remove These?

``` text
  - telnet         # Unencrypted protocol, exposes credentials to interception.
  - rsh            # Uses cleartext authentication; vulnerable to spoofing.
  - rlogin         # Relies on `.rhosts`, easily abused for unauthorized access.
  - ypbind         # Part of NIS; outdated directory service with known weaknesses.
  - tftp           # No authentication, used in many past exploitation chains.
  - talk           # Obsolete chat protocol, not secured or monitored.
  - xinetd         # Super-server for legacy services; expands attack surface.
  - vsftpd         # FTP server, plain text credentials unless explicitly hardened.
  - ftp            # Transmits files and passwords in the clear.
  - samba          # SMB protocol stack, often misconfigured and exposed.
  - nfs-utils      # Enables NFS, which can leak data if not securely locked down.
  - netcat         # A powerful backdoor tool often used in post-exploitation.
```

## Part of the Vault Minimal Series

Hardening with precision. Remove what shouldn’t be there.

## Example Playbook

```yaml
- hosts: all
  roles:
    - vault-unsafe-packages
```

## License

MIT License

## Author Information

This role is maintained by DeadSwitch | The Cyber Ghost
