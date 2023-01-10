# Ansible Role: mirsg.install_python

This role installs Python, pip, and setuptools on Debian and RedHat operating systems. It will also update pip to the latest version.

## Requirements

If you would like to run Ansible Molecule to test this role, the requirements are in [`requirements.txt`](https://github.com/UCL-MIRSG/ansible-role-install-python/blob/main/requirements.txt).

## Role Variables

`install_python_3_packages`: list of packages to be installed when Python 3 is the default interpreter. This defaults to:

```yaml
- python3
- python3-pip
- python3-setuptools
```

`install_python2_packages`: list of packages to be installed when Python 2 is the default interpreter. This defaults to:

```yaml
- python
- python-pip
- python-setuptools
```

`extra_python3_packages`: list of additional Python 3 packages to to be installed by the OS package manager, NOT by pip
`extra_python2_packages`: list of additional Python 2 packages to to be installed by the OS package manager, NOT by pip

`python3_pip_packages`: list of Python 3 packages to be installed by pip
`python2_pip_packages`: list of Python 2 packages to be installed by pip

## Dependencies

There are no Ansible-Galaxy dependencies for this role.

## Example Playbook

### Basic usage

This role uses the Ansible facts `ansible_os_family` and `ansible_distribution_major_version` to determine whether Python 2 or Python 3
should be installed on your managed host. As such, you will need to gather these facts when using this role:

```yaml
- name: Install Python 3
  hosts: all
  gather_facts: true
  gather_subset:
    - "os_family"
    - "distribution_major_version"
    - "!min"
    - "!all"
  roles:
    - mirsg.install_python
```

This will gather only the necessary facts (`ansible_os_family` and `ansible_distribution_major_version`) to run the role and install Python.

## License

[BSD 3-Clause License](https://github.com/UCL-MIRSG/ansible-role-install-python/blob/main/LICENSE).

## Author Information

This role was created by the [Medical Imaging Research Software Group](https://www.ucl.ac.uk/advanced-research-computing/expertise/research-software-development/medical-imaging-research-software-group) at [UCL](https://www.ucl.ac.uk/).
