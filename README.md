# wordpress_ansible
Role Name
=========

## 1. Provisioning

This role handles the initial setup of the server, including installing necessary packages, updating the package list, and upgrading all packages.

Tasks:

    Install required packages.
    Run apt update and apt upgrade.
    

## 2. SSH Configuration

This role configures SSH settings by modifying the actual SSH configuration file. It includes changing the SSH port, disabling root login, and password authentication. It also manages user and group creation.

Tasks:

    Change SSH port.
    Disable root login.
    Disable password authentication.
    Create users and assign them to a group.
    Configure sudoers file for the group.

## 3. Nginx

This role installs Nginx, removes the default site configuration, and sets up a new site configuration.

Tasks:

    Install Nginx.
    Unlink default Nginx site.
    Deploy custom Nginx configuration.
    Enable the new site by creating a symlink in sites-enabled.
    Restart Nginx service.

## 4. PHP-FPM

This role installs PHP-FPM and necessary PHP modules, configures the www.conf file by modifying lines instead of copying templates, and restarts PHP-FPM.

Tasks:

    Install PHP-FPM and required modules.
    Configure www.conf.
    Restart PHP-FPM service.

Prerequisites
------------
    Ansible installed on your local machine.
    Access to the target server(s) with SSH.

Role Variables
--------------

### SSH Configuration
- 'shh_port': Port number for SSH (default is `22`).
- `root_login`: Whether root login is allowed (`yes` or `no`).
- `password_authentication`: Whether password authentication is allowed (`yes` or `no`).
- 'ssh_group': The name of group to be add.
- 'users': The users wanted to be created and add to the group.
- 'privileges': The privileges want to be add.

### Nginx Configuration
- `nginx_server_name`: The server name or domain for the Nginx configuration.
- `document_root`: The directory where Nginx will be installed.
- `nginx_site_name`: The name of the Nginx site configuration. 

### PHP-FPM Configuration
-`php_fpm_packages`: The required modules need to be install.
- `php_fpm_user`: The user under which PHP-FPM will run.
- `php_fpm_group`: The group under which PHP-FPM will run.


Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Below is an example of how to use roles in a playbook:

    ---
- hosts: myhosts
  become: yes
  roles:
    - provisioning
    - ssh
    - nginx
    - PHP-FPM
  

License
-------

BSD

