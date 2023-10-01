# Playground 001

RHEL 8 Quadlet playground

Based on great quadlet demo from https://github.com/ygalblum/quadlet-demo/tree/main

## Environment

```
System   : Red Hat Enterprise Linux 8.8 (Ootpa)
Kernel   : 4.18.0-477.21.1
Selinux  : Enforcing
Firewalld: Enabled
```

```
$ lsblk | grep 'sd[a-z]'

sda                  8:0    0   32G  0 disk
├─sda1               8:1    0    1G  0 part /boot
└─sda2               8:2    0   31G  0 part
sdb                  8:16   0  100G  0 disk
```

## Setup

Install ansible galaxy dependencies
```
ansible-galaxy collection install -r requirements.yml
```

Provision stuff
```
ansible-playbook -i inventory.yml playbook.yml
```

Are we there yet?
```
watch -c "curl -sk https://localhost:8000 | grep -i wordpress > /dev/null && echo OK || echo 'NOT THERE YET'"
```

