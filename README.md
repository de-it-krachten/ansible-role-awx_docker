[![CI](https://github.com/de-it-krachten/ansible-role-awx_docker/workflows/CI/badge.svg?event=push)](https://github.com/de-it-krachten/ansible-role-awx_docker/actions?query=workflow%3ACI)


# ansible-role-awx_docker

Install AWX using Docker 



## Dependencies

#### Roles
None

#### Collections
- community.docker

## Platforms

Supported platforms

- Red Hat Enterprise Linux 8<sup>1</sup>
- RockyLinux 8
- OracleLinux 8<sup>1</sup>
- OracleLinux 9<sup>1</sup>
- AlmaLinux 8<sup>1</sup>
- Debian 11 (Bullseye)
- Debian 12 (Bookworm)
- Ubuntu 20.04 LTS

Note:
<sup>1</sup> : no automated testing is performed on these platforms

## Role Variables
### defaults/main.yml
<pre><code>
# AWX required OS Packages
awx_os_packages:
  - git
  - make

# AWX required pypi Packages
awx_pip_packages:
  - ansible
  - pexpect

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
# awx_pg_hostname: '127.0.0.1'
# awx_pg_port: 5432
# awx_pg_username:
# awx_pg_password: awx
# awx_broadcast_websocket_secret: awx
# awx_secret_key: awx

# Enable LDAP
awx_ldap: false

# AWX admin user
awx_admin_username: admin
awx_admin_password: admin
awx_admin_email: admin@example.com

awx_possible_changed_files:
  - tools/docker-compose/inventory
  - tools/docker-compose/ansible/roles/sources/templates/docker-compose.yml.j2

awx_inventory_updates:
  - name: pg_host
    value: "{{ vars['awx_pg_host'] | default('') }}"
  - name: pg_hostname
    value: "{{ vars['awx_pg_hostname'] | default('') }}"
  - name: pg_port
    value: "{{ vars['awx_pg_port'] | default('') }}"
  - name: pg_username
    value: "{{ vars['awx_pg_username'] | default('') }}"
  - name: pg_password
    value: "{{ vars['awx_pg_password'] | default('') }}"
  - name: pg_database
    value: "{{ vars['awx_pg_database'] | default('') }}"
  - name: broadcast_websocket_secret
    value: "{{ vars['awx_broadcast_websocket_secret'] | default('') }}"
  - name: secret_key
    value: "{{ vars['awx_secret_key'] | default('') }}"

awx_docker_compose_updates:
  - name: port8080
    regexp: '^(\s*)(- )("8080:8080")'
    replace: '\1#\2\3'
  - name: port8888
    regexp: '^(\s*)(- )("8888:8888")'
    replace: '\1#\2\3'
</pre></code>




## Example Playbook
### molecule/default/converge.yml
<pre><code>
- name: sample playbook for role 'awx_docker' pre playbook
  ansible.builtin.import_playbook: converge-pre.yml
  when: molecule_converge_pre is undefined or molecule_converge_pre | bool
- name: sample playbook for role 'awx_docker'
  hosts: all
  become: 'yes'
  vars:
    awx_version: HEAD
  tasks:
    - name: Include role 'awx_docker'
      ansible.builtin.include_role:
        name: awx_docker
</pre></code>
