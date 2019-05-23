# ansible-azure

Role to create/delete/manage Azure objects. 
By default, it installs a CentOS virtual machine with all prerequisite components.

## Requirements

Using the Azure Resource Manager modules requires having specific Azure SDK modules installed on the host running Ansible.

```
sudo pip install ansible[azure]
```

[source](https://github.com/Azure/azure_modules#installation)

## Role Variables

### Default variables

```
# virtual network default vars
virtual_network_name: "{{ resource_group_name }}-vnet"
virtual_network_address_prefixes: "10.0.0.0/16"

# subnet default vars
subnet_name: "default"
subnet_address_prefix_cidr: "10.0.0.0/24"

# public ip default vars
public_ip_name: "{{ resource_group_name }}-ip"
public_ip_allocation_method: Dynamic

# security group default vars
security_group_name: "{{ resource_group_name }}-sg"
security_group_rules:
  - name: DenySSH
    protocol: Tcp
    destination_port_range: 22
    access: Deny
    priority: 100
    direction: Inbound
  - name: 'AllowSSH'
    protocol: Tcp
    source_address_prefix:
      - "{{ ssh_source_server_ip }}"
    destination_port_range: 22
    access: Allow
    priority: 101
    direction: Inbound

# network interface default vars
network_interface_name: "{{ vm_name }}-nic"

# vm size default vars
vm_size: "Standard_B1ls"

# vm image default vars
image_offer: CentOS
image_publisher: OpenLogic
image_sku: "7.6"
image_version: latest
```

### Extra variables

```
# Azure resource group vars
resource_group_name
resource_group_location

# Azure virtual machine vars
vm_name
admin_username
admin_password
```

## Example Playbook

```yaml
- hosts: servers
  roles:
  - role: ansible_azure
```

## License

BSD
