---
id: 10
date: 2025-05-02T00:00:00Z
title: Ansible Cheatsheet
author: Jeremy Novak
summary: Cheatsheet for Ansible
slug: ansible-cheatsheet
tags:
  - ansible
published: true
---

# Ansible Cheatsheet

---

## Basic Commands

- Run ad-hoc command on all hosts
```bash
ansible all -m ping
```

- Run command on specific group
```bash
ansible webservers -m command -a "uptime"
```

- Run command as sudo
```bash
ansible all -m command -a "systemctl status nginx" --become
```

- Run command with specific user
```bash
ansible all -m command -a "whoami" --become-user=nginx
```

- Check Ansible version
```bash
ansible --version
```

- List all hosts in inventory
```bash
ansible all --list-hosts
```

---

## Inventory Management

- Use custom inventory file
```bash
ansible all -i inventory.ini -m ping
```

- Example static inventory file (inventory.ini)
```ini
[webservers]
web1.example.com
web2.example.com

[databases]
db1.example.com
db2.example.com

[all:vars]
ansible_user=ubuntu
ansible_ssh_private_key_file=~/.ssh/id_rsa
```

- Example dynamic inventory (YAML)
```yaml
all:
  children:
    webservers:
      hosts:
        web1.example.com:
        web2.example.com:
    databases:
      hosts:
        db1.example.com:
```

- View inventory structure
```bash
ansible-inventory --list
```

- View specific group
```bash
ansible-inventory --list --yaml webservers
```

---

## Playbooks

- Run a playbook
```bash
ansible-playbook playbook.yml
```

- Run playbook with specific inventory
```bash
ansible-playbook -i inventory.ini playbook.yml
```

- Dry run (check mode)
```bash
ansible-playbook playbook.yml --check
```

- Run with increased verbosity
```bash
ansible-playbook playbook.yml -v
# or -vv, -vvv for more detail
```

- Run specific tags
```bash
ansible-playbook playbook.yml --tags "install,configure"
```

- Skip specific tags
```bash
ansible-playbook playbook.yml --skip-tags "testing"
```

- Example basic playbook
```yaml
---
- name: Install and configure nginx
  hosts: webservers
  become: yes
  tasks:
    - name: Install nginx
      apt:
        name: nginx
        state: present
        update_cache: yes

    - name: Start nginx service
      systemd:
        name: nginx
        state: started
        enabled: yes
```

---

## Common Modules

- Package management (apt/yum)
```bash
ansible all -m apt -a "name=nginx state=present" --become
```

- Service management
```bash
ansible all -m systemd -a "name=nginx state=started enabled=yes" --become
```

- Copy files
```bash
ansible all -m copy -a "src=/local/file dest=/remote/file owner=root mode=644" --become
```

- Template files
```bash
ansible all -m template -a "src=template.j2 dest=/etc/config.conf" --become
```

- Create directories
```bash
ansible all -m file -a "path=/opt/myapp state=directory owner=root group=root mode=755" --become
```

- Download files
```bash
ansible all -m get_url -a "url=https://example.com/file.tar.gz dest=/tmp/"
```

- Execute shell commands
```bash
ansible all -m shell -a "echo $HOME"
```

- Gather facts
```bash
ansible all -m setup
```

---

## Variables and Facts

- Use variables in playbook
```yaml
---
- name: Use variables
  hosts: all
  vars:
    app_name: myapp
    app_version: 1.0
  tasks:
    - name: Create app directory
      file:
        path: "/opt/{{ app_name }}"
        state: directory
```

- External variable files
```bash
ansible-playbook playbook.yml --extra-vars "@vars.yml"
```

- Pass variables via command line
```bash
ansible-playbook playbook.yml --extra-vars "version=2.0 environment=production"
```

- View all facts for host
```bash
ansible hostname -m setup
```

- View specific facts
```bash
ansible hostname -m setup -a "filter=ansible_distribution*"
```

---

## Roles

- Create role structure
```bash
ansible-galaxy init myrole
```

- Install role from Galaxy
```bash
ansible-galaxy install geerlingguy.nginx
```

- Install roles from requirements file
```bash
ansible-galaxy install -r requirements.yml
```

- Example requirements.yml
```yaml
---
- name: geerlingguy.nginx
  version: 2.8.0
- src: https://github.com/username/repo.git
  name: custom-role
```

- Use role in playbook
```yaml
---
- name: Configure web servers
  hosts: webservers
  roles:
    - geerlingguy.nginx
    - { role: myapp, app_env: production }
```

---

## Ansible Vault

- Create encrypted file
```bash
ansible-vault create secrets.yml
```

- Edit encrypted file
```bash
ansible-vault edit secrets.yml
```

- View encrypted file
```bash
ansible-vault view secrets.yml
```

- Encrypt existing file
```bash
ansible-vault encrypt vars.yml
```

- Decrypt file
```bash
ansible-vault decrypt vars.yml
```

- Change vault password
```bash
ansible-vault rekey secrets.yml
```

- Run playbook with vault
```bash
ansible-playbook playbook.yml --ask-vault-pass
```

- Use vault password file
```bash
ansible-playbook playbook.yml --vault-password-file .vault_pass
```

---

## Conditionals and Loops

- Conditional execution
```yaml
- name: Install package on Ubuntu
  apt:
    name: nginx
    state: present
  when: ansible_distribution == "Ubuntu"
```

- Loop over list
```yaml
- name: Install multiple packages
  apt:
    name: "{{ item }}"
    state: present
  loop:
    - nginx
    - git
    - curl
```

- Loop over dictionary
```yaml
- name: Create users
  user:
    name: "{{ item.name }}"
    shell: "{{ item.shell }}"
  loop:
    - { name: 'user1', shell: '/bin/bash' }
    - { name: 'user2', shell: '/bin/zsh' }
```

---

## Error Handling

- Ignore errors
```yaml
- name: This might fail
  command: /bin/false
  ignore_errors: yes
```

- Handle failures
```yaml
- name: Attempt something
  command: /might/fail
  register: result
  failed_when: result.rc != 0 and "expected error" not in result.stderr
```

- Retry on failure
```yaml
- name: Download file
  get_url:
    url: https://example.com/file.tar.gz
    dest: /tmp/file.tar.gz
  retries: 3
  delay: 5
```

---

## Debugging and Testing

- Debug variable values
```yaml
- name: Show variable
  debug:
    var: ansible_hostname
```

- Debug with message
```yaml
- name: Show custom message
  debug:
    msg: "The hostname is {{ ansible_hostname }}"
```

- Syntax check
```bash
ansible-playbook playbook.yml --syntax-check
```

- List tasks in playbook
```bash
ansible-playbook playbook.yml --list-tasks
```

- List hosts affected
```bash
ansible-playbook playbook.yml --list-hosts
```

- Step through playbook
```bash
ansible-playbook playbook.yml --step
```

---

## Configuration

- View Ansible configuration
```bash
ansible-config view
```

- List all config options
```bash
ansible-config list
```

- Example ansible.cfg
```ini
[defaults]
inventory = ./inventory
remote_user = ubuntu
private_key_file = ~/.ssh/id_rsa
host_key_checking = False
retry_files_enabled = False

[privilege_escalation]
become = True
become_method = sudo
become_user = root
```

---

## Useful Patterns

- Run playbook on single host
```bash
ansible-playbook playbook.yml --limit "web1.example.com"
```

- Run on subset of hosts
```bash
ansible-playbook playbook.yml --limit "webservers:&production"
```

- Exclude hosts
```bash
ansible-playbook playbook.yml --limit "all:!databases"
```

- Check if service is running
```yaml
- name: Check if nginx is running
  command: systemctl is-active nginx
  register: nginx_status
  failed_when: false
  changed_when: false
```

- Restart service only if config changed
```yaml
- name: Copy nginx config
  template:
    src: nginx.conf.j2
    dest: /etc/nginx/nginx.conf
  notify: restart nginx

handlers:
  - name: restart nginx
    systemd:
      name: nginx
      state: restarted
``` 