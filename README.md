# Ansible Role: mirsg.install_python

This role installs Python, pip, and setuptools on Debian and RedHat operating systems. It will also update pip to the latest version or a
user-specified version, and then install user-specified Python packages using pip.

## Requirements

If you would like to run Ansible Molecule to test this role, the requirements are in [`requirements.txt`](https://github.com/UCL-MIRSG/ansible-role-install-python/blob/main/requirements.txt).

## Role Variables

`install_python` is a dictionary contains the following varialbes:

`version`: the version of Python to install. This defaults to `"3"`.

`pip_version`: the version of pip to update to. This defaults to `"21.3.1"`.

`pip_executable`: path to the pip executalbe to use for installing packages. This defaults to `"pip3"`

`system_packages`: list of system packages to be installed along with Python. This defaults to:

```yaml
- python3
- python3-pip
- python3-setuptools
```

The packages listed in `install_python.system_packages` will be installed by the OS package manager, NOT by pip.

`python3_pip_packages`: list of Python packages to be installed by pip. This defaults to `[]`.

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
  roles:
    - mirsg.install_python
```

This will gather all facts before installing Python. If you would like to install only the necessary facts (`ansible_os_family` and `ansible_distribution_major_version`) to run the role and install Python, you can use `gather_subset`:

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

## License

[BSD 3-Clause License](https://github.com/UCL-MIRSG/ansible-role-install-python/blob/main/LICENSE).

## Author Information

This role was created by the [Medical Imaging Research Software Group](https://www.ucl.ac.uk/advanced-research-computing/expertise/research-software-development/medical-imaging-research-software-group) at [UCL](https://www.ucl.ac.uk/).
