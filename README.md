# IPA Server Ansible Role

This repository contains a configuration template 
(i.e. an [Ansible Role](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_reuse_roles.html)) 
to customize your environment in the
[European Weather Cloud (EWC)](https://europeanweather.cloud/).
The template is designed to:
* Validate that network/subnet configuration in the EWC tenancy, that is OpenStack
security group rules, is suitable for IPA server operation (e.g. open ports for 
DNS, LDAP, Kerberos, HTTP/HTTPS, SSH, etc.)
* Check that target host has the recommended RAM availability
* Configure a pre-existing RockyLinux 8 or RockyLinux 9 virtual machine such that it:
  * Provides DNS resolutions for discovery of resources (i.e. other virtual machines)
  * Enables centralized user and credentials creation/edition/deletion/authentication
  * Allows centralized authorization between users and resources
* Automatically update the underlying subnet DNS nameserver to point to the newly configured IPA server


## Copyright and License
Copyright © EUMETSAT 2025.

The provided code and instructions are licensed under the [MIT license](./LICENSE).
They are intended to automate the setup of an environment that includes 
third-party software components.
The usage and distribution terms of the resulting environment are 
subject to the individual licenses of those third-party libraries.

Users are responsible for reviewing and complying with the licenses of
all third-party components included in the environment.

Contact [EUMETSAT](http://www.eumetsat.int) for details on the usage and distribution terms.

## Authentication

Before proceeding, if you lack OpenStack Application Credentials or do not know
how to make them available to Ansible in your development environment, make sure
to check out the 
[EWC documentation](https://confluence.ecmwf.int/display/EWCLOUDKB/EWC+-+How+to+request+Openstack+Application+Credentials).

## Usage

The step-by-step described below assume your local file system follows the 
example structure below, with `ewc-ansible-role-ipa-server` being a clone of this
repository:
```
.
├── roles
│   └── ewc-ansible-role-ipa-server
├── inventory.yml
└── playbook.yml
```

### 1. Specify the target host and SSH credentials
Create an inventory file to specify address/credentials that Ansible should use
to reach the virtual machine you wish to configure:
```yaml
# inventory.yml
---
ewcloud:
  hosts:
    ipa_server:
      ansible_python_interpreter: /usr/bin/python3
      ansible_host: <add the IPV4 address of the target host>
      ansible_ssh_private_key_file: <add the path to local SSH RSA private key file>
      ansible_user: <add the username which owns the SSH RSA private key >
```
### 2. Customize the template

Edit input values for the template [variables](./vars/main.yml) as needed (see
[Inputs](#inputs) section for details).
Then, proceed to create an Ansible Playbook file to load your customizations: 

```yaml
# playbook.yml
---
- name: Deploy IPA Server on RockyLinux
  hosts: ipa_server
  become: true
  become_user: root
  become_method: ansible.builtin.sudo

  roles:
    - ewc-ansible-role-ipa-server

```

### 3. Apply the template

You can apply changes on the target host by running:
```bash
ansible-playbook -i inventory.yml playbook.yml
```

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|----------|
| ipa_domain |IPA domain name. Example: `<memberstate>-<organization>-<projectname>.ewc` | `string` | n/a | yes |
| ipa_server_hostname | IPA server host name. Example: `ldap` | `string`| n/a | yes |
| ipa_admin_username | username of administrator account to replace the default IPA admin | `string` | n/a | yes |
| ipa_admin_password | IPA Directory Manager/Admin password (at least 8 characters long) | `string` | n/a | yes |
| ipa_admin_givenname | given name of the administrator to replace the default IPA admin (needs not to belong to a physical person). Example: `EWC` | `string` | n/a | yes |
| ipa_admin_surname | surname of the administrator to replace the default IPA admin (needs not to belong to a physical person). Example: `IPAADMIN` | `string` | n/a | yes |
| os_network_name | OpenStack network to which the target virtual machine has access to. Example: `private` | `string` | n/a | yes |
| os_subnet_name | OpenStack subnet in which the target virtual machine is running. Example: `private subnet` | `string` | n/a | yes |
| os_subnet_cidr | IP range (in CIDR format) that spans the OpenStack subnet in which the target virtual machines is running. Example: `10.0.0.0/24` | `string` |n/a  | yes |
| os_security_group_name | OpenStack security group containing all firewall rules required by the IPA server/client communication. Example: `ldap`  | `string` | n/a | yes |
| os_subnet_dns_nameserver_ip_default | default DNS nameserver IPV4 address registered on the OpenStack subnet where the IPA server will run. Example: `1.1.1.1` | `string` | n/a | yes |
| os_subnet_dns_nameserver_ip_fallback | fallback DNS nameserver IPV4 address registered on the OpenStack subnet where the IPA server will run. Example: `8.8.8.8` | `string` | n/a  | yes |


## SW Bill of Materials (SBoM)

Third-party components used in the resulting environment.

### RockyLinux 8 Environment
The following components will be included in the resulting environment:

| Component | Version | License | Home URL |
|------|---------|---------|--------------|
| firewalld | 0.9 | GPLv2+ | http://www.firewalld.org |
| ipa-server | 4.9 | GPLv3+ | http://www.freeipa.org |
| ipa-server-dns | 4.9 | GPLv3+ | http://www.freeipa.org |
| bind-dyndb-ldap | 11.6 | GPLv2+ | https://releases.pagure.org/bind-dyndb-ldap |

### RockyLinux 9 Environment
The following components will be included in the resulting environment:

| Component | Version | License | Home URL |
|------|---------|---------|--------------|
| firewalld | 1.3 | GPLv2+ | http://www.firewalld.org |
| ipa-server | 4.12 | GPLv3+ | http://www.freeipa.org/ |
| ipa-server-dns | 4.12 | GPLv3+ | http://www.freeipa.org/ |
| bind-dyndb-ldap | 11.11 | GPLv2+ | https://releases.pagure.org/bind-dyndb-ldap |

## Changelog
All notable changes (i.e. fixes, features and breaking changes) are documented 
in the [CHANGELOG.md](./CHANGELOG.md).

## Contributing

Thanks for taking the time to join our community and start contributing!
Please make sure to:
* Familiarize yourself with our [Code of Conduct](./CODE_OF_CONDUCT.md) before 
contributing.
* See [CONTRIBUTING.md](./CONTRIBUTING.md) for instructions on how to request 
or submit changes.

## Authors

[European Weather Cloud](http://support.europeanweather.cloud/) 
<[support@europeanweather.cloud](mailto:support@europeanweather.cloud)>
