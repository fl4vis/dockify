# Dockify 🐋

Manage Docker installation, versions, upgrades, uninstallation, and user management on Linux hosts using Ansible.

<br>

## Requirements

- Tested Ubuntu 22.04 / 24.04. Mint 21.3
- Requires `apt` on target hosts.
- Ensure the user running the playbook has sudo privileges if installing, upgrading, or managing Docker users.

<br>

## Role Variables

| Variable | Description | Required |
|----------|-------------|----------|
| `action` | Determines which operation the role will perform. Supported actions: `install`, `check_installed`, `check_version`, `check_repo_versions`, `upgrade`, `uninstall_engine`, `add_docker_user` | Yes |
| `version` | Docker version to install or upgrade to (format: `x.y.z`). Required for `install` and `upgrade` actions | No |
| `user` | System user to add to the Docker group. Required for `add_docker_user` action | No |

<br>

## Supported Actions

| Action | Description |
|--------|-------------|
| `install` | Installs a specific Docker version. Requires `version` variable. |
| `check_installed` | Checks if Docker is already installed. |
| `check_version` | Displays the currently installed Docker version. |
| `check_repo_versions` | Shows available Docker versions from the repository. |
| `upgrade` | Upgrades Docker to a specific version. Requires `version` variable. |
| `uninstall_engine` | Uninstalls Docker Engine, CLI, containerd, and Docker Compose. |
| `add_docker_user` | Adds a non-root user to the Docker group. Requires `user` variable. |

<br>

## Dependencies

- No external roles are required.

<br>

## Install / Uninstall

```bash
ansible-galaxy install git+https://github.com/fl4vis/dockify.git

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
