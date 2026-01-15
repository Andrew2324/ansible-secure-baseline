# ansible-secure-baseline (Amazon Linux 2023)

Portfolio-ready Ansible project that enforces a secure, repeatable server baseline and deploys application services using role-based automation.

---

## Why this exists

In production environments, infrastructure provisioning and OS configuration are separate concerns. This project demonstrates how Ansible can be used **after infrastructure is provisioned** to enforce a secure baseline and deploy application services safely and repeatably.

---

## Integration with Infrastructure as Code

This project is designed to run after infrastructure is provisioned using **Terraform or CloudFormation**. Infrastructure lifecycle is managed by IaC, while Ansible handles OS-level configuration and application deployment.

---

## What this project does

The project applies a secure baseline using modular Ansible roles:

- **common**: Baseline packages, timezone configuration, optional admin user
- **security**: SSH hardening with safe validation (`sshd -t`)
- **web**: NGINX installation and static page deployment

### Key characteristics

- Role-based Ansible design (idempotent automation)
- Secure configuration enforcement (SSHD hardening)
- Inventory with `group_vars` and `host_vars` for environment-specific config
- Service deployment using handlers (NGINX)
- Operational safety checks before applying changes

---

## Failure & Safety Considerations

To ensure safe operation in production environments:

- SSH configuration is validated using `sshd -t` before restart
- Services restart only when changes occur via handlers
- Tasks are idempotent to prevent configuration drift

---

## Repository Structure

```txt
inventory/dev/hosts.ini
inventory/dev/group_vars/all.yml
inventory/dev/host_vars/web1.yml
playbooks/site.yml
roles/common
roles/security
roles/web
diagram/architecture.drawio
