# Playground 001

RHEL 8 Quadlet playground

Based on great quadlet demo from https://github.com/ygalblum/quadlet-demo/tree/main

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

