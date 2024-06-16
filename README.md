<p align="center"> Ansible Role for installing and configuring php
    <br> 
</p>


### Role Variables

| Variable Name | Value | Type | Default |
| ------ | ------ | ------ | ------ |
| php_fpm_presence | defines if php-fpm will be installed or not | Bool | true |
| php_fpm_user | defines as what user php-fpm service is started | String | www-data |
| php_fpm_group | | String | www-data |
| php_version | defines which version of php is installed | String | 8.3 |
| php_packages | defines what packages of php is installed | List | See vars/main.yml |
| php_ini_cli | defines configuration of cli php.ini file | List of Dictionaries | See defaults/main.yml |
| php_ini_fpm | defines configuration of fpm php.ini file | List of Dictionaries | See defaults/main.yml |
| php_fpm_base_conf | defines global configuration of php-fpm.conf file | List of Dictionaries | See vars/main.yml |
| php_fpm_base_pool_conf | defines configuration of php-fpm.conf file | List of Dictionaries | See vars/main.yml |
| composer_version | defines which version of composer will be installed | String | 2.7.7 |
| composer_executable_path | defines the path of where composer will be installed | String | /usr/local/bin/composer`composer_version`|
| composer_owner_username | defines who will own the the executable | String | www-data |
| composer_owner_group | defines which group will own the the executable | String | www-data |


`Example:`
```
---
php_version: "8.3"

php_packages:
  - php{{ php_version }}-bcmath
  - php{{ php_version }}-ctype
  - php{{ php_version }}-curl
  - php{{ php_version }}-dom

php_fpm_presence: true
php_fpm_user: www-data
php_fpm_group: www-data


php_ini_cli:
  - section: PHP
    option: memory_limit
    value: -1

php_ini_fpm:
  - section: PHP
    option: memory_limit
    value: 128M
  - section: PHP
    option: upload_max_filesize
    value: 2M

php_fpm_base_conf:
  - section: global
    option: pid
    value: /run/php/php{{ php_version }}-fpm.pid

php_fpm_base_pool_conf:
  - section: www
    option: listen
    value: /run/php/php{{ php_version }}-fpm.sock
  - section: www
    option: user
    value: "{{ php_fpm_user }}"
  - section: www
    option: group
    value: "{{ php_fpm_group }}"
  - section: www
    option: listen.owner
    value: "{{ php_fpm_user }}"
  - section: www
    option: listen.group
    value: "{{ php_fpm_group }}"
```
