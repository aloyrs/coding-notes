Ansible is a software tool to automate the deployment, configuration, and management of IT infrastructure and applications.

Ansible :

- Inventory , at /etc/ansible/hosts

```bash
[aws_ec2]
3.27.145.170 ansible_ssh_private_key_file=/home/ubuntu/ansiblefolder/todo.pem
```

Add servers that you want to configure here

- Add playbook

```bash
---
- name: Install dependencies
  hosts: aws_ec2
  become: true
  vars:
    repo_path: /home/ubuntu/to-do-fullstack
  tasks:
    - name: Update apt package cache
      apt:
        update_cache: yes
    - name: Install Node.js and npm
      apt:
        name:
          - nodejs
          - npm
        state: present

    - name: Install Git
      apt:
        name: git
        state: present

    - name: Install Postgres
      apt:
        name: postgresql
        state: present

    - name: Install Nginx
      apt:
        name: nginx
        state: present

    - name: Install PM2
      npm:
        name: pm2
        global: yes

    - name: Ensure the repository is already cloned
      stat:
        path: "/home/ubuntu/to-do-fullstack"
      register: git_repo_status
    - name: Git clone
      git:
        repo: 'https://github.com/aloysiustanrs/to-do-fullstack'
        dest: " {{ repo_path }}"
      when: not git_repo_status.stat.exists

    - name: Frontend  npm install
      npm:
        path: "{{ repo_path }}/frontend"
        state: present
    - name: Build frontend
      command: npm run build
      args:
        chdir: "{{ repo_path }}/frontend"
    - name: Backend  npm install
      npm:
        path: "{{ repo_path }}/backend"
        state: present

    - name: Copy nginx configuration template
      template:
        src: /home/ubuntu/ansiblefolder/nginx.conf.j2
        dest: /etc/nginx/sites-available/yomy.online
    - name: Create symlink from sites-available to sites-enabled
      file:
        src: /etc/nginx/sites-available/yomy.online
        dest: /etc/nginx/sites-enabled/yomy.online
        state: link
      notify:
        - Restart Nginx
  handlers:
    - name: Restart Nginx
      service:
        name: nginx
        state: restarted

```

What I did : install required apps, clone code using git, setup nginx to run frontend

Can add more tasks like : setup backend to pm2 service, setup env variables, setup firewall, setup ssl, configure db user
