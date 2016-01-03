## Ansible Playbook: LEP (2-Tier)

[Ansible](http://www.ansible.com/) **playbook** to provision a LEP ([Linux](http://www.linux.org/), [NGINX](http://nginx.org/), [PHP](http://php.net/)) stack (2-tier).

NGINX web server and PHP application tiers are configured separately.

By default, the playbook provisions a `web` and `app` node in the `webservers` and `appservers` groups, respectively, using the following configurations declared in `group_vars/`:

    # group_vars/webservers.yml
    nginx_user: "nginx"
    nginx_vhosts:
      + listen: "80 default_server"
        server_name: "example.com"
        root: "/srv/app"
        index: "index.html"

    # group_vars/appservers.yml
    php_packages:
      + php70w
      + php70w-cli
      + php70w-common
      + php70w-devel
      + php70w-gd
      + php70w-mbstring
      + php70w-pdo
      + php70w-xml
      + php70w-fpm
    ...

**OS**
- RHEL/CentOS 6.x.

### Roles

- ca-certificates
- git
- libselinux-python
- nginx
- php
- repo-epel-release
- repo-webtatic
- vim

### Clone

Clone repo into your project:
    
    $ git clone <repo> ./ansible-playbook-lep-2

### Installation

Ansible Galaxy install requirements.

    $ sh bin/install

### Usage

Vagrant up.

    $ vagrant up
