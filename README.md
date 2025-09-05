# Dockify 🐋

Manage Docker installation, versions, upgrades, uninstallation, and user management on Linux hosts using Ansible.

<br>

## Requirements

- Tested on: [ Ubuntu 22.04 / 24.04, Mint 21.3 ]
- Requires `apt` on target hosts.
- Ensure the user running the playbook has `ansible_become_pass:<password>` 

<br>

## Role Variables

| Variable | Description |
|----------|-------------|
| `action` | Determines which operation the role will perform. Supported actions: `install`, `check_installed`, `check_version`, `check_repo_versions`, `upgrade`, `uninstall_engine`, `add_docker_user` |
| `version` | Docker version to install or upgrade to (format: `x.y.z`). Required for `install` and `upgrade` actions | 
| `user` | System user to add to the Docker group. Required for `add_docker_user` action | 

<br>

## Supported Actions

| Action | Description |
|--------|-------------|
| `install` | Installs a specific Docker version. **Required** `version` variable. |
| `check_installed` | Checks if Docker is already installed. |
| `check_version` | Displays the currently installed Docker version. |
| `check_repo_versions` | Shows available Docker versions from the repository. |
| `upgrade` | Upgrades Docker to a specific version. **Required** `version` variable. |
| `uninstall_engine` | Uninstalls Docker Engine, CLI, containerd, and Docker Compose. |
| `add_docker_user` | Adds a non-root user to the Docker group. **Required** `user` variable. |

<br>

## Dependencies

- No external roles are required.

<br>

## Install / Update / Uninstall 
 
```bash
ansible-galaxy install git+https://github.com/fl4vis/dockify.git

ansible-galaxy install -f git+https://github.com/fl4vis/dockify.git

ansible-galaxy remove dockify
```

<br>

## Example Playbook

```yaml
- hosts: all
  roles:
    - role: dockify
      vars:
        action: install
        version: "28.3.1"

    - role: dockify
      vars:
        action: check_installed

    - role: dockify
      vars:
        action: check_version

    - role: dockify
      vars:
        action: check_repo_versions

    - role: dockify
      vars:
        action: upgrade
        version: "28.3.3"

    - role: dockify
      vars:
        action: uninstall_engine

    - role: dockify
      vars:
        action: add_docker_user
        user: "{{ ansible_user }}"
```
