# Ansible Secure Baseline – Troubleshooting Guide

This document covers common issues encountered when running the Ansible
secure baseline playbooks against Amazon Linux 2023 EC2 instances and how
to diagnose and resolve them.

---

## 1. SSH Connection Failures

### Symptoms
- Playbook fails with SSH errors
- Timeout errors
- Permission denied (publickey)

### Checks
- Verify the instance is running and reachable
- Confirm the correct SSH key is used
- Ensure port 22 is allowed in the EC2 security group
- Confirm the instance is in the correct subnet/VPC
- Test manually:
  ```bash
  ssh -i key.pem ec2-user@<instance-ip>

---

Resolution

Update the Ansible inventory with the correct IP or DNS

Fix security group rules to allow SSH from the control node

Verify ansible_user is set correctly for Amazon Linux 2023

Ensure SSH hardening roles do not lock out access prematurely


# Safe Recovery Strategy

If a playbook run causes instability:

Restore from snapshot or AMI

Roll back recent role changes

Re-run playbooks incrementally

Validate changes in a staging environment first


# Best Practices

Always test playbooks in a non-production environment

Use version control for roles and variables

Run playbooks with --check mode when possible

Keep SSH access available during hardening

Document intentional security exceptions

# Ansible Role Fails Mid-Execution
Symptoms

Playbook stops on a specific role or task

Partial configuration applied

Checks

Review the exact failing task output

Run playbook with verbose logging:

ansible-playbook site.yml -vvv


Check system logs on the target host:

journalctl -xe

Resolution

Fix syntax or logic errors in the role

Make tasks idempotent

Add handlers where services must be restarted

Re-run the playbook after correction


# OS Update Failures
Symptoms

Symptoms

Package installation errors

Repository unavailable errors

Checks

Verify network access to package repositories

Check disk space:

df -h


Confirm correct Amazon Linux release

Resolution

Retry updates after network issues resolve

Clean package cache:

dnf clean all


Pin critical packages if required