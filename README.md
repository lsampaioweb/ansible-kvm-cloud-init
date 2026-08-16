# ansible-kvm-cloud-init

Role for configuring Proxmox KVM virtual machine settings including CPU type, cloud-init, and hardware hotplug options.

**Note:** This is a sub-module role. It is not intended to be run as a standalone playbook; it should be imported or included by a parent orchestration project.

## Usage

Import or include this role in a parent playbook and provide the required variables via `vars:`, `group_vars`, or extra vars. Example in a parent playbook:

```yaml
- name: "Configure KVM VM"
  ansible.builtin.import_role:
    name: ansible-kvm-cloud-init
  vars:
    vm_name: my-vm
    cpu_type: host
    hotplug: disk,network,cpu
```

Or pass variables via extra vars when running the parent playbook:

```bash
ansible-playbook parent-playbook.yml -e "vm_name=my-vm cpu_type=host hotplug=disk,network,cpu"
```

## Variables

### Required Variables (extra vars or group_vars)

| Variable | Type | Description | Example |
|----------|------|-------------|---------|
| `vm_name` | string | Name of the Proxmox VM to configure | `my-vm` |
| `cpu_type` | string | CPU type to set on the VM (passed to `qm set --cpu`) | `host` |
| `hotplug` | string | Comma-separated list of hotplug options (passed to `qm set --hotplug`) | `disk,network,cpu` |

### Optional Variables

| Variable | Type | Default | Description |
|----------|------|---------|-------------|
| `vm_id` | integer | auto-detected | Proxmox VM ID; if not provided, will be resolved from `vm_name` |

### Role Variables (vars/main.yml)

| Variable | Type | Description |
|----------|------|-------------|
| `ansible_user` | string | Proxmox root user (default: `root`) |
| `ansible_password` | string | Proxmox root password (resolved via `secret-tool`) |

## Tasks

1. **Getting VM ID by name** — Resolves `vm_id` from the VM name if not already provided.
2. **Setting the CPU Type** — Configures the VM CPU type via `qm set --cpu`.
3. **Setting Cloud-Init** — Enables DHCP cloud-init configuration via `qm set --ipconfig0 ip=dhcp`.
4. **Setting Hardware HotPlug** — Enables hardware hotplug options via `qm set --hotplug`.

## Created by

Luciano Sampaio
