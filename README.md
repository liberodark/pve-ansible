# Ansible Proxmox

Ansible playbook for VM deployment.

In order to run these playbooks, you need at least ansible 2.9.10. Additional you need to install community.general collection and proxmoxer pip module. You can do it with the following commands (run them as the user who will run ansible, because these modules are installed for your user, not globally)

Install this on your PC :

```
ansible-galaxy collection install community.general
pip install proxmoxer
```

Install this on PVE if you use SSH :

```
apt install python3-proxmoxer
```

Edit config.yml and set password for the proxmox user.

Next step is to edit cts.yml file and add/change settings there. Keep in mind you need these values (or at least vmid), if you want to use the yaml file to delete the machines later.
You can copy cts.yml to another file and use it instead (see create_cts.yml and delete_cts.yml)

You can create the machines by running (API)
```
ansible-playbook create_cts.yml
```

You can create the machines by running (SSH)
ansible-playbook -i hosts create_cts.yml
```
ansible-playbook create_cts.yml
```

Add -v for more verbosity

You can delete the machines by running (API)
```
ansible-playbook delete_cts.yml
```

You can delete the machines by running (SSH)
```
ansible-playbook -i hosts delete_cts.yml
```

Attention: Keep in mind, if a machine takes longer to shut down, it may not be stopped/removed correctly. Log in the proxmox server and stop/delete the machines manually. On deletion, choose "purge" tick box.

By default, update of the machine does not work for following parameters "net, virtio, ide, sata, scsi" (see https://docs.ansible.com/ansible/latest/collections/community/general/proxmox_module.html, update parameter). If you still want do to it, edit  ~/.ansible/collections/ansible_collections/community/general/plugins/modules/proxmox.py on your own risk.

Based on https://gitlab.com/todorpetkov/ansible-proxmox/ work
