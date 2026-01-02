# ansible-secure-baseline (Amazon Linux 2023)

Portfolio-ready Ansible project that applies a repeatable baseline using roles:
- **common**: baseline packages + timezone + optional admin user
- **security**: SSH hardening with safe validation (`sshd -t`)
- **web**: NGINX + static page deployment

- Role-based Ansible design (idempotent automation)
- Secure configuration enforcement (SSHD hardening)
- Inventory + group_vars/host_vars structure
- Service deployment with handlers (NGINX)
- Operational safety: validate sshd config before restart

## Repo Structure
```txt
inventory/dev/hosts.ini
inventory/dev/group_vars/all.yml
inventory/dev/host_vars/web1.yml
playbooks/site.yml
roles/common
roles/security
roles/web
diagram/architecture.drawio
