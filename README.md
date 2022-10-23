[![CI](https://github.com/de-it-krachten/ansible-role-awx_docker/workflows/CI/badge.svg?event=push)](https://github.com/de-it-krachten/ansible-role-awx_docker/actions?query=workflow%3ACI)


# ansible-role-awx_docker

Install AWX using Docker 



## Dependencies

#### Roles
None

#### Collections
- community.general
- community.docker

## Platforms

Supported platforms

- Red Hat Enterprise Linux 8<sup>1</sup>
- RockyLinux 8
- OracleLinux 8<sup>1</sup>
- AlmaLinux 8<sup>1</sup>
- Debian 11 (Bullseye)
- Ubuntu 20.04 LTS

Note:
<sup>1</sup> : no automated testing is performed on these platforms

## Role Variables
### defaults/main.yml
<pre><code>
# AWX version
awx_version: latest

# Github API endpoint to get latest version
awx_api: https://api.github.com/repos/ansible/awx

# AWX git repo
awx_git_url: https://github.com/ansible/awx.git

# Local path to clone git repo into
awx_git_path: /opt/awx/git

# Should git repo be recreated
awx_git_refresh: false

# Git commit to use
awx_git_tag: "{{ awx_version }}"

# Location to write log files to
awx_log_path: /opt/awx/log

# Steps to execute in the process
awx_create_receptor: false
awx_compose_build: true
awx_compose: true

# Autostart AWX at boot
awx_autostart: true

# Passwords / secrets to use (when not defined, automatically defined)
# awx_pg_password: awx
# awx_broadcast_websocket_secret: awx
# awx_secret_key: awx

# Enable LDAP
awx_ldap: false

# AWX admin user
awx_admin_username: admin
awx_admin_password: admin
awx_admin_email: admin@example.com
</pre></code>




## Example Playbook
### molecule/default/converge.yml
<pre><code>
- ansible.builtin.import_playbook: converge-pre.yml

- name: sample playbook for role 'awx_docker'
  hosts: all
  become: "{{ molecule['converge']['become'] | default('yes') }}"
  vars:
    awx_version: HEAD
  tasks:
    - name: Include role 'awx_docker'
      ansible.builtin.include_role:
        name: awx_docker
</pre></code>
