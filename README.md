[![CI](https://github.com/de-it-krachten/ansible-role-awx_docker/workflows/CI/badge.svg?event=push)](https://github.com/de-it-krachten/ansible-role-awx_docker/actions?query=workflow%3ACI)


# ansible-role-awx_docker

Install AWX using Docker 


## Platforms

Supported platforms

- Red Hat Enterprise Linux 7<sup>1</sup>
- Red Hat Enterprise Linux 8<sup>1</sup>
- Red Hat Enterprise Linux 9<sup>1</sup>
- CentOS 7
- RockyLinux 8
- RockyLinux 9
- OracleLinux 8
- AlmaLinux 8
- AlmaLinux 9
- Debian 10 (Buster)
- Debian 11 (Bullseye)
- Ubuntu 18.04 LTS
- Ubuntu 20.04 LTS
- Ubuntu 22.04 LTS
- Fedora 35
- Fedora 36

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
awx_git_path: /tmp/awx

# Should git repo be recreated
awx_git_refresh: true

# Location to write log files to
awx_log_path: /root

# Steps to execute in the process
awx_create_receptor: false
awx_compose_build: true
awx_compose: true

# Passwords / secrets to use (when not defined, automatically defined)
#awx_pg_password: awx
#awx_broadcast_websocket_secret: awx
#awx_secret_key: awx

# AWX admin user
awx_admin_username: admin
awx_admin_password: admin
awx_admin_email: admin@example.com
</pre></code>



## Example Playbook
### molecule/default/converge.yml
<pre><code>
- name: sample playbook for role 'awx_docker'
  hosts: all
  become: "{{ molecule['converge']['become'] | default('yes') }}"
  tasks:
    - name: Include role 'awx_docker'
      include_role:
        name: awx_docker
</pre></code>
