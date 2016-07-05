# Ansible Nginx Role

This role can install (optionally from the official repo), and configure Nginx, as well as it's site files (coming soon).  The role tries to not apply any opinioned default settings, though it does take some liberties on location for the configurations.  Configurations are built via YAML dictionaries whenever possible, with the setting and value as the respective key and value.

### Requirements

  * Ansible >= 2.0
  * sudo/root privileges

### Usage

#### Main

Once the role has been added to your roles path, the default behavior is to install Nginx from the official repository (for Debian/Ubuntu and RHEL/CentOS), and apply a very minimal configuration.  An example minimal default install would be to simply include the role like:

```
---
- hosts: all
  become: yes

  roles:
    - { role: nginx }
```

This install will setup a configuration file with the following settings defined:

  * user (changes based on os used)
  * worker_processes (defaults to auto)
  * pid (/var/run/nginx.pid)
  * empty "events" section
  * http section that just includes a few directories

You can add additional options to each section of the main config ('main', 'events', and 'http') by using the following dictionary:

```
nginx_conf_settings:
  main:
    key: value
  events:
    key: value
  http:
    key: value
```

This will place the option with a value of "key" in the corresponding section of the main nginx.conf file.

#### Upstreams

Upstreams can be defined by defining a YAML dictionary called `nginx_upstreams`.  To create an upstream with the name 'php-handler', you would use something like:

```
---
- hosts: all
  become: yes
  vars:
    nginx_upstreams:
      php-handler:
        server: 'unix:/var/run/php5-fpm.sock'

  roles:
    - { role: nginx }
```

You can create as many upstreams as you'd like, by using the format:

```
nginx_upstreams:
  upstream1:
    key: value
  upstream2:
    key1: value1
    key2: value2
```

where 'key' is the configuration setting (i.e. 'server') and value is that settings value (i.e. 'unix:/var/run/php5-fpm.sock').  Upstreams are only created when you define one.

#### Sites

Sites are not yet implemented.  They will be soon, however.

### License

This role is released under the MIT license. See LICENSE file for copyright, and full details.
