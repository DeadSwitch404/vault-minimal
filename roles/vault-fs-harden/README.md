# DeadSwitch Vault Minimal - Filesystem Hardening

This Ansible role applies secure mount options to common partitions that are often misused in attacks.

## Features

- Mounts `/tmp` and `/dev/shm` with `noexec`, `nosuid`, `nodev` for runtime isolation.
- Ensures `/home` is mounted with `nodev` to prevent device files in user space.
- All changes are idempotent and only apply when safe to do so.

## Requirements

- Ansible 2.9+
- Tested on Debian Bookworm and Rocky 9

## Safe by Design

- `/tmp` and `/dev/shm` are only mounted if not already configured.
- `/home` keeps its original device and type, only updating mount options.

## Example Playbook

```yaml
- hosts: all
  roles:
    - vault-fs-hardening
```

## License

MIT License

## Author Information

This role is maintained by DeadSwitch | The Cyber Ghost
