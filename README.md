# Ansible Role: diagrams

Ansible role for installing an [Diagrams](https://diagrams.mingrammer.com/)
into a Python3 VirtualEnv.

[![Build Status](https://www.travis-ci.org/PyratLabs/ansible-role-diagrams.svg?branch=master)](https://www.travis-ci.org/PyratLabs/ansible-role-diagrams)

## Requirements

This role has been tested on Ansible 2.7.0+ against the following Linux Distributions:

  - Amazon Linux 2
  - CentOS 8
  - CentOS 7
  - Debian 10
  - Fedora 29
  - Fedora 30
  - Fedora 31
  - Ubuntu 18.04 LTS

The target server requires the following packages:

  - Graphviz
  - python3
  - python3 venv

## Disclaimer

If you have any problems please create a GitHub issue, I maintain this role in
my spare time so I cannot promise a speedy fix delivery.

## Role Variables


| Variable                           | Description                                                                   | Default Value        |
|------------------------------------|-------------------------------------------------------------------------------|----------------------|
| `diagrams_version`                 | Use a specific version of diagrams, eg. `0.10.0`. Specify `false` for latest. | `false`              |
| `diagrams_install_dir`             | Installation directory to put diagrams virtual environments.                  | `$HOME/.virtualenvs` |
| `diagrams_venv_name`               | Name for the diagrams Virtualenv.                                             | diagrams             |
| `diagrams_venv_suffix`             | Add a custom suffix to virtualenv.                                            | `diagrams_version`   |
| `diagrams_venv_site_packages`      | Allow venv to inherit packages from global site-packages.                     | `false`              |
| `diagrams_install_os_dependencies` | Allow role to install OS dependencies.                                        | `false`              |
| `diagrams_python3_path`            | Specify a path to a specific python version to use in virtualenv.             | _NULL_               |

## Dependencies

No dependencies on other roles.

## Example Playbook

Example playbook for installing to single user:

```yaml
- hosts: diagrams_hosts
  roles:
     - { role: xanmanning.diagrams, diagrams_version: 0.10.0 }
```

Example playbook for installing the latest diagrams version globally:

```yaml
---
- hosts: diagrams_hosts
  become: true
  vars:
    diagrams_install_os_dependencies: true
    diagrams_install_dir: /opt/diagrams/bin
    diagrams_venv_name: current
  roles:
    - role: xanmanning.diagrams
```

### Activating the diagrams venv

You need to activate the python3 virtual environment to be able to access
`diagrams`. This is done as per the below:

```bash
source {{ diagrams_install_dir }}/{{ diagrams_venv_name }}/bin/activate
```

In the above example global installation playbook, this would look like the
following:

```bash
source /opt/diagrams/bin/current/bin/activate
```

## License

[BSD 3-clause](LICENSE.txt)

## Author Information

[Xan Manning](https://xanmanning.co.uk/)
