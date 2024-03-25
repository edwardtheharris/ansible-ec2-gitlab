---
abstract: The readme for some Ansible playbooks that intend to allow for simple
  deployment and recovery of self-managed GitLab instances.
authors: Xander Harris
date: 2024-03-24
title: Ansible GitLab Deployment & Recovery Readme
---

## Assumptions

The default configuration assumes a vault password exists at
{file}`/etc/ansible/vault`. It also assumes the inventory file is in YAML format
and located at {file}`/etc/ansible/hosts.yaml`

### Fact Caching

The default configuration uses fact caching with Redis running on the controller
with the default port.

## Usage

Dependencies are managed with Pipenv, to prepare an environment for
development run the following.

```{code-block} shell
python3 -m pip install -U pip pipenv
pipenv install --dev
pipenv shell
```

You're ready to go.

### Hosts example

You can find an example inventory file below, this inventory is intended
to house a Kubernetes cluster with a pair of control planes that are members
of a Samba Active Directory Domain that contains a pair of controllers and
is responsible for authentication, file, and routing services.

```{code-block} yaml
:caption: /etc/ansible/hosts.yaml

dc:
  hosts:
    dc01.example.com:
      ansible_user: user
    dc02.example.com:
      ansible_user: user
np:
  hosts:
    napalm.example.com:
      ansible_user: user
kcp:
  hosts:
    kcp01.example.com:
      ansible_user: user
    kcp02.example.com:
      ansible_user: user
ca:
  hosts:
    ca.example.com:
      ansible_user: user
      secret_ca_passphrase: secret-ca-passphrase
```

```{toctree}
:caption: Other Information

cicd
license
security
```
