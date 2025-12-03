# IPA Server Ansible Role

This repository contains a configuration template 
(i.e. an [Ansible Role](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_reuse_roles.html)) 
to customize your environment in the
[European Weather Cloud (EWC)](https://europeanweather.cloud/).
The template is designed to:
* Validate that network/subnet configuration in the EWC tenancy
* Configure a pre-existing virtual machine running RockyLinux version 8,
and with a minimum recommended 4GB of RAM, such that it:
  * Provides DNS resolutions for discovery of resources (i.e. other virtual
  machines)
  * Enables centralized user and credentials creation/edition/deletion/authentication
  * Allows centralized authorization between users and resources

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
| ipa_domain | domain name to be managed by the IPA server. Example: `eumetsat.sandbox.ewc` | `string` | n/a | yes |
| ipa_server_hostname | hostname of the target vm where the IPA server will be installed. Example: `ipa-server-1` | `string`| n/a | yes |
| ipa_admin_username | username of administrator account to replace the default IPA admin. Example: `ipaadmin` | `string` | n/a | yes |
| ipa_admin_password | password of administrator account to replace the default IPA admin (at least 8 characters long). Example: `my-secret-password` | `string` | n/a | yes |
| ipa_admin_givenname | given name of the administrator to replace the default IPA admin (not necessarily a real person's name). Example: `EWC` | `string` | n/a | yes |
| ipa_admin_surname | surname of the administrator to replace the default IPA admin (not necessarily a real person's name). Example: `IPAADMIN` | `string` | n/a | yes |
| os_network_name | OpenStack network to which the target virtual machine has access to. Example: `private` | `string` | n/a | yes |
| os_security_group_name | OpenStack security group containing all firewall rules required by the IPA server/client communication. Example: `ipa` | `string` | n/a | yes |

## Dependencies
> 💡 Upon execution, a SBOM (SPDX format) is auto-generated and stored in the VM's file system root directory (see `/sbom.json`).
Third-party components used in the resulting environment.

| Component |  Home URL |
|------|---------|
| ipa-server |  http://www.freeipa.org |
| ipa-server-dns | http://www.freeipa.org |
| bind-dyndb-ldap | https://releases.pagure.org/bind-dyndb-ldap |

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
