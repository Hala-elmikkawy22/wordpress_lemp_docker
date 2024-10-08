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
  
    Create WordPress Directory**: Ensures that the directory `/var/www/html/` exists for WordPress installation.
    Download WordPress**: Downloads the latest version of WordPress from the official source and extracts it to the specified directory.
    Set Permissions for Files**: Sets the appropriate permissions for all WordPress files.
    Delete wp-config-sample.php**: Removes the sample configuration file that comes with WordPress.
    Set up wp-config.php**: Copies a templated configuration file (`wp-config.php.j2`) to the WordPress directory.

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

