# ansible-kvm-cloud-init
Playbook with Ansible tasks to setup some settings on the KVM.

Run the command in the terminal:
```bash
  ansible-playbook kvm_setup.yml -e "node=kvm-07 vm_id=901 hotplug=disk,network,cpu storage_pool=Ceph_Silver"
```

# Tasks:

### 1. Remove the CDROM.

### 2. Add the hotplug options.

### 3. Set the Cloud-Init settings.

# Created by: 

1. Luciano Sampaio.
