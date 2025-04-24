# 🛡️ vault-minimal

**DeadSwitch Open Source Vault Roles**  
Minimal. Modular. Monitored by silence.

This repo contains open-source Ansible roles for system hardening, curated and maintained by [DeadSwitch](https://github.com/DeadSwitch404).  
These are the public-facing versions of the hardened Vault Pack.

> 🔒 Pro versions with extended features are developed privately.

---

## 📦 Roles Included

- `vault-fs-harden` - Secure filesystem permissions
- `vault-password-policy` - Enforce password complexity
- `vault-services-minimal` - Stop & mask unsafe default services
- `vault-ssh-harden` - Lock down OpenSSH configs
- `vault-sysctl-harden` - Harden kernel-level sysctls
- `vault-unsafe-packages` - Remove legacy, unsafe packages

---

## 🔧 Usage

```yaml
- name: Apply Vault Minimal roles
  hosts: all
  become: true
  roles:
    - vault-unsafe-packages
    - vault-password-policy
    - vault-services-minimal
    - vault-fs-harden
    - vault-ssh-harden
    - vault-sysctl-harden
```

Run the playbook with:

```bash
ansible-playbook -i inventory.ini example-playbook.yml
```

## 🧙‍♂️ Author

DeadSwitch | The Cyber Ghost  
"In silence, we rise. In the switch, we fade."

## 🔗 License

MIT - Use freely, attribute wisely.
