# Playground 001

RHEL 8 Quadlet playground

Based on great quadlet demo from https://github.com/ygalblum/quadlet-demo/tree/main

## Environment

```
System   : Red Hat Enterprise Linux 8.8 (Ootpa)
Kernel   : 4.18.0-477.21.1
Selinux  : Enforcing
Firewalld: Enabled
Podman   : 4.4.1
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

## Results

```
# podman pod ps
POD ID        NAME          STATUS      CREATED       INFRA ID      # OF CONTAINERS
dc6aba99381f  quadlet-demo  Running     14 hours ago  ff78f152bbc6  3
```

```
# podman ps -a
CONTAINER ID  IMAGE                                    COMMAND               CREATED       STATUS       PORTS                                           NAMES
b366ca604b80  docker.io/library/mysql:5.6              mysqld                14 hours ago  Up 14 hours                                                  quadlet-demo-mysql
3f218cd10f08  localhost/podman-pause:4.4.1-1692285794                        14 hours ago  Up 14 hours                                                  39b3e27cf20d-service
ff78f152bbc6  localhost/podman-pause:4.4.1-1692285794                        14 hours ago  Up 14 hours  0.0.0.0:8000->8080/tcp, 0.0.0.0:9000->9901/tcp  dc6aba99381f-infra
9635924116c3  docker.io/library/wordpress:4.8-apache   apache2-foregroun...  14 hours ago  Up 14 hours  0.0.0.0:8000->8080/tcp, 0.0.0.0:9000->9901/tcp  quadlet-demo-wordpress
dcf27d44a3d6  docker.io/envoyproxy/envoy:v1.25.0       envoy -c /etc/env...  14 hours ago  Up 14 hours  0.0.0.0:8000->8080/tcp, 0.0.0.0:9000->9901/tcp  quadlet-demo-envoy
```

## Warning

This is playground repo. It's not intended to be used in production environment. I strongly advise to look at the playbook, roles and how they work, especially xfs_storage_*. If not careful you might loose all your data!
