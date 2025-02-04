Ansible Role: Visual Studio Code Extensions
===========================================

[![Tests](https://github.com/gantsign/ansible-role-visual-studio-code-extensions/workflows/Tests/badge.svg)](https://github.com/gantsign/ansible-role-visual-studio-code-extensions/actions?query=workflow%3ATests)
[![Ansible Galaxy](https://img.shields.io/badge/ansible--galaxy-gantsign.visual--studio--code--extensions-blue.svg)](https://galaxy.ansible.com/gantsign/visual-studio-code-extensions)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](https://raw.githubusercontent.com/gantsign/ansible-role-visual-studio-code-extensions/master/LICENSE)

Role to install extensions for the
[Visual Studio Code](https://code.visualstudio.com) IDE / text editor.

Requirements
------------

* Ansible >= 2.9

* OS

    * Linux

      * Debian Family

          * Ubuntu

              * Bionic (18.04)
              * Focal (20.04)

      * RedHat Family

          * Rocky Linux

              * 8

          * Fedora

              * 35

      * SUSE Family

          * openSUSE

              * 15.3

      * Note: other versions are likely to work but have not been tested.

    * macOS

        * Consider macOS support experimental as this time as it's not included
          in the automated tests.

Role Variables
--------------

The following variables will change the behavior of this role (default values
are shown below):

```yaml
# The VS Code build variant:
#   stable   - https://code.visualstudio.com
#   insiders - https://code.visualstudio.com/insiders/
#   oss      - https://github.com/microsoft/vscode/wiki/Differences-between-the-repository-and-Visual-Studio-Code
#              Caution: since Microsoft doesn't distribute binaries for code-oss
#              this role doesn't include tests for code-oss.
#              Note: VSCodium is not presently supported by this role.
visual_studio_code_extensions_build: stable

# Users to install extensions for
users: []
```

Users are configured as follows:

```yaml
users:
  - username: # Unix user name
    # Extensions to be installed if not already present
    visual_studio_code_extensions:
      - # extension 1
      - # extension 2
    # Extensions to be uninstalled if not already absent
    visual_studio_code_extensions_absent:
      - # extension 3
```

Example Playbook
----------------

```yaml
- hosts: servers
  roles:
    - role: gantsign.visual-studio-code-extensions
      users:
        - username: vagrant
          visual_studio_code_extensions:
            - streetsidesoftware.code-spell-checker
            - wholroyd.jinja
            - ms-python.python
          visual_studio_code_extensions_absent:
            - seanmcbreen.Spell
```

More Roles From GantSign
------------------------

You can find more roles from GantSign on
[Ansible Galaxy](https://galaxy.ansible.com/gantsign).

Development & Testing
---------------------

This project uses [Molecule](http://molecule.readthedocs.io/) to aid in the
development and testing; the role is unit tested using
[Testinfra](http://testinfra.readthedocs.io/) and
[pytest](http://docs.pytest.org/).

To develop or test you'll need to have installed the following:

* Linux (e.g. [Ubuntu](http://www.ubuntu.com/))
* [Docker](https://www.docker.com/)
* [Python](https://www.python.org/) (including python-pip)
* [Ansible](https://www.ansible.com/)
* [Molecule](http://molecule.readthedocs.io/)

Because the above can be tricky to install, this project includes
[Molecule Wrapper](https://github.com/gantsign/molecule-wrapper). Molecule
Wrapper is a shell script that installs Molecule and it's dependencies (apart
from Linux) and then executes Molecule with the command you pass it.

To test this role using Molecule Wrapper run the following command from the
project root:

```bash
./moleculew test
```

Note: some of the dependencies need `sudo` permission to install.

License
-------

MIT

Author Information
------------------

John Freeman

GantSign Ltd.
Company No. 06109112 (registered in England)
