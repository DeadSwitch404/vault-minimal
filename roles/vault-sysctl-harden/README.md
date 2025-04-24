# DeadSwitch Vault Minimal - Sysctl Hardening

This role enforces hardened kernel and network parameters via `sysctl`, shielding your system from common attacks and insecure defaults.

## Features

- Disables IP redirects and source routing to prevent spoofing and man-in-the-middle attacks.
- Enables logging of suspicious packets and enforces ICMP safety.
- Enables TCP SYN cookies to mitigate SYN flood DoS attacks.
- Disables kernel debugging (`sysrq`) and enforces ASLR.

## Requirements

- Ansible 2.9+
- Root privileges required
- Tested on Debian Bookworm and Rocky 9

## Variables

`vault_minimal_sysctl_settings`: A dictionary of sysctl parameters to apply.

Default values:

```yaml
net.ipv4.conf.all.accept_redirects: 0
net.ipv4.conf.default.accept_redirects: 0
net.ipv4.conf.all.send_redirects: 0
net.ipv4.conf.default.send_redirects: 0
net.ipv4.conf.all.accept_source_route: 0
net.ipv4.conf.default.accept_source_route: 0
net.ipv4.conf.all.log_martians: 1
net.ipv4.conf.default.log_martians: 1
net.ipv4.icmp_echo_ignore_broadcasts: 1
net.ipv4.icmp_ignore_bogus_error_responses: 1
net.ipv4.tcp_syncookies: 1
kernel.randomize_va_space: 2
kernel.sysrq: 0
```

## Why These Settings Matter

Each parameter below plays a direct role in reducing attack surface and enforcing secure behavior at the kernel level:

- `net.ipv4.conf.all.accept_redirects: 0`
  Prevents the system from accepting malicious ICMP redirects which could hijack traffic.

- `net.ipv4.conf.default.accept_redirects: 0`
  Applies the same protection to interfaces created after boot.

- `net.ipv4.conf.all.send_redirects: 0`
  Stops the system from sending redirects that could mislead other hosts.

- `net.ipv4.conf.default.send_redirects: 0`
  Ensures new interfaces also avoid sending redirects.

- `net.ipv4.conf.all.accept_source_route: 0`
  Blocks source-routed packets used to bypass routing controls.

- `net.ipv4.conf.default.accept_source_route: 0`
  Extends that protection to new interfaces dynamically added.

- `net.ipv4.conf.all.log_martians: 1`
  Enables logging of suspicious packets with impossible source addresses.

- `net.ipv4.conf.default.log_martians: 1`
  Ensures this logging is active even on future interfaces.

- `net.ipv4.icmp_echo_ignore_broadcasts: 1`
  Thwarts smurf attacks by ignoring ICMP echoes to broadcast addresses.

- `net.ipv4.icmp_ignore_bogus_error_responses: 1`
  Ignores spurious ICMP error messages that could be used in network scanning.

- `net.ipv4.tcp_syncookies: 1`
  Enables SYN cookies to defend against SYN flood denial-of-service attacks.

- `kernel.randomize_va_space: 2`
  Enforces full Address Space Layout Randomization (ASLR) to make exploitation harder.

- `kernel.sysrq: 0`
  Disables magic sysrq key combinations to prevent local attackers from triggering debugging actions.


## Example Playbook

```yaml
- hosts: all
  roles:
    - vault-sysctl-harden
```

## Part of the Vault Minimal Series

Tune the kernel. Silence the noise.

## License

MIT License

## Author Information

This role is maintained by DeadSwitch | The Cyber Ghost
