
# Termux Ansible VLAN Lab

A hands-on Ansible lab for Android. The playbooks run locally in Debian inside Termux and generate IOS-style VLAN configuration files. No physical switches or simulator connection are required.

## Requirements

- Termux with a Debian environment
- Ansible installed in a Python virtual environment inside Debian

Activate your virtual environment before running the commands below. Run them from the repository root.

## Run the lab

```bash
ansible-playbook -i 'localhost,' first-lab.yml
ansible-playbook -i 'localhost,' vlan-lab.yml
ansible-playbook -i 'localhost,' multi-vlan.yml -e @sw1-vlans.yml
cat multi-vlan.cfg
```

- `first-lab.yml` confirms Ansible can run a local playbook.
- `vlan-lab.yml` generates `vlan-lab.cfg` for one VLAN.
- `multi-vlan.yml` uses a Jinja loop to generate `multi-vlan.cfg`.
- `sw1-vlans.yml` supplies the VLAN IDs and names for one switch.

## Preview changes and test idempotence

Edit a VLAN name in `sw1-vlans.yml`, then preview the change:

```bash
ansible-playbook -i 'localhost,' multi-vlan.yml --check --diff -e @sw1-vlans.yml
```

Run again without `--check` to write the file. Repeat that same run with the same inputs and look for `changed=0` in the recap.
