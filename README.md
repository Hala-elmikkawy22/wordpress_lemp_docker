# wordpress_ansible
Role Name
=========

## 1. Provisioning

This role handles the initial setup of the server, including installing necessary packages, updating the package list, and upgrading all packages.

Tasks:

    Install required packages.
    Run apt update and apt upgrade.
    
## 2. Create Users

This role automates the process of user management on a remote server.

Tasks:

     Create group for users.
     Create users and assign them to a group.
     Configure sudoers file for the group.
     Create .ssh directory for the user.
     copy public key from local host to remote server.
     
## 3. SSH Configuration

This role configures SSH settings by modifying the actual SSH configuration file. It includes changing the SSH port, disabling root login, and password authentication. It also manages user and group creation.

Tasks:

    Change SSH port.
    Disable root login.
    Disable password authentication.
   

## 4. Docker

This role installs Docker, and Docker Compose.

Tasks:

    Install required packages for Docker.
    Add Docker's official GPG key and APT repository.
    Install Docker.
    install Docker Compose.
    Unlink default Nginx site.
    Deploy custom Nginx configuration.
    Enable the new site by creating a symlink in sites-enabled.
    Restart Nginx service.

## 5. Docker Containers Role

This role manages the setup of Docker containers for Nginx and PHP-FPM.
Tasks:

    Create Multiple Directories: Creates necessary directories for Nginx and PHP-FPM configurations.
    Copy Nginx Configuration: Copies the Nginx configuration template to the correct location.
    Copy PHP-FPM Configuration: Copies the PHP-FPM configuration file to the specified directory.
    Copy Docker Compose File: Copies the Docker Compose template to manage services easily.
    Copy Dockerfile: Copies the Dockerfile for building the PHP-FPM container.
    Start Containers Using Docker Compose: Runs the Docker Compose command to start the services.


## 6. UWF
This role for configuring UFW (Uncomplicated Firewall) on a server.

Tasks:
     
    installs UFW.
    sets up firewall rules for SSH, HTTP, and HTTPS.
    enables the firewall with a default deny policy.

    
## 7. MySql
This role installs and configures MariaDB for WordPress, ensuring the database is created and the appropriate user is set up. It also modifies the configuration to allow remote connections by changing the bind-address.
Tasks:
      
    Install MariaDB and Dependencies.
    Ensure MariaDB Service is Running and Enabled.
    Create WordPress Database.
    Create WordPress User.
    Configure MariaDB to Accept Remote Connections.

## 8. WordPress Role

This role is responsible for installing WordPress and setting it up correctly on the server.

Tasks:
  
    Create WordPress Directory.
    Downloads the latest version of WordPress from the official source and extracts it to the specified directory.
    Sets the appropriate permissions for all WordPress files.
    Removes the sample configuration file that comes with WordPress.
    Copies a templated configuration file (`wp-config.php.j2`) to the WordPress directory.

Prerequisites
------------
    Ansible installed on your local machine.
    Access to the target server(s) with SSH.

Role Variables
--------------
### provisioning
- `packages`: The packages to be installed.
  
### Create Usere
- `users_group` :The name of group to be add.
- `users`: The users wanted to be created and add to the group.
- `privileges`: The privileges want to be add. 

### Docker Compose
- 'shh_port': Port number for SSH (default is `22`).
- `root_login`: Whether root login is allowed (`yes` or `no`).
- `password_authentication`: Whether password authentication is allowed (`yes` or `no`).
- `server_name`: The server name or domain for the Nginx configuration.
- `nginx_image`: The Nginx container is built using this image.
- `nginx_container_name`: The name of nginx container.
- `nginx_conf_path`: The directory where Nginx will be installed.
- `php_fpm_image`: The PHP-FPM container is built using this image.
- `php_fpm_container_name`: The name of PHP-FPM the container.
- `php_fpm_conf_path`:The directory where PHP-FPM configuration file will be.

 ### MySql
 
 - `db_name`: The name of wordpress database.
 - `db_user`: the user of the database.
 - `db_password`: The password for the dataebase 
 - `mariadb_root_password`: The password of the Root of database.
   
### Wordpress
- `wordpress_path`: The Directory where wordpress will be installed.

### Lets Encrypt

- `ssl_cert_path`: The SSL Certificate Path.
- `ssl_key_path` :The SSL key Path.


Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Below is an example of how to use roles in a playbook:

    ---
---
#hosts: myhosts
-  hosts: all
   remote_user: root
   become: yes
   vars_files:
    - group_vars/all.yml
    
   roles:
    - provisioning
    - create_users
    - ssh
    - docker
    - docker-containers
    - uwf
    - mysql
    - wordpress      
    - letsencrypt

  

License
-------

BSD

