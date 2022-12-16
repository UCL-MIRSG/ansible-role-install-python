# Ansible Role: mirsg.install_python3

This role installs Python 3, pip, and setuptools on Debian and RedHat operating systems. It will also update pip to the latest version.

## Requirements

If you would like to run Ansible Molecule to test this role, the requirements are in [`requirements.txt`](https://github.com/UCL-MIRSG/ansible-role-install-python3/blob/main/requirements.txt).

## Role Variables

There are no variables to set for this role.

## Dependencies

There are no Ansible-Galaxy dependencies for this role.

## Example Playbook

### Basic usage

This role uses the Ansible fact `ansible_os_family` to run the correct commands for installing Python 3 on your managed host. As such, you will
need to gather this fact when using this role:

```yaml
- name: Install Python 3
  hosts: all
  gather_facts: true
  roles:
    - mirsg.install_python3
```

This will gather only the necessary fact (`ansible_os_family`) to run the role.

### Overriding Python 2 default

When using this role, if Python 2 is installed on your host and the `ansible_python_interpreter` defaults to `/usr/bin/python`, you will need to
explicitly set your interpreter to be `/usr/bin/python3`. This can either be done at the playbook / task level, or within `host_vars` / `group_vars`.

If Python 2 is the default for your managed node, and you set `ansible_python_interpreter: /usr/bin/python3` before calling this role, you
will need to ensure that you do not attempt to gather the `ansible_python_interpreter` fact. This is because Ansible will throw an error
complaining that the path `/usr/bin/python3` does not exist.

This play below will gather only the necessary fact (`ansible_os_family`) to run the role and install Python 3.

```yaml
- name: Install Python 3
  hosts: all
  gather_facts: true
  gather_subset:
    - "os_family"
    - "!min"
    - "!all"
  roles:
    - mirsg.install_python3
```

## License

[BSD 3-Clause License](https://github.com/UCL-MIRSG/ansible-role-install-python3/blob/main/LICENSE).

## Author Information

This role was created by [Paul Smith](https://github.com/p-j-smith) from the
[Medical Imaging Research Software Group](https://www.ucl.ac.uk/advanced-research-computing/expertise/research-software-development/medical-imaging-research-software-group) at [UCL](https://www.ucl.ac.uk/).
