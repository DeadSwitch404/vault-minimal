# DeadSwitch Vault Minimal - Password Policy

This Ansible role enforces strong password policies using `pwquality` and PAM.

## Features

- Configures `/etc/security/pwquality.conf` with hardened values.
- Ensures PAM enforces retry limits and complexity checks.
- Supports both Debian and RHEL-based systems.

## Requirements

- Ansible 2.9+
- Package `libpam-pwquality` or `pam_pwquality` must be installed
- Tested on Debian Bookworm and Rocky Linux 9

## Variables

```yaml
vault_pw_minlen: 12        # Minimum password length
vault_pw_dcredit: -1       # At least one digit
vault_pw_ucredit: -1       # At least one uppercase
vault_pw_lcredit: -1       # At least one lowercase
vault_pw_ocredit: -1       # At least one special character
vault_pw_retry: 3          # Retry attempts for password prompts
```

## Why This Matters

Weak passwords are low-hanging fruit for attackers. This role enforces strict controls to make brute-forcing and guessing impractical. Following Vault Minimal principles, we lock the front door tight.

## Example Playbook

```yaml
- hosts: all
  roles:
    - vault-password-policy
```

## License

MIT License

## Author Information

This role is maintained by DeadSwitch | The Cyber Ghost
