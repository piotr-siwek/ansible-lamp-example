# Ansible LAMP Deployment

This Ansible playbook deploys a LAMP (Linux, Apache, MySQL, PHP) environment on a target server.

## Prerequisites

- Ansible installed on control machine
- Target server accessible via SSH
- Target server should be Ubuntu/Debian based (tested on Ubuntu 20.04)
- User with sudo privileges

## Usage

1. Edit inventory file (create hosts.ini or use default)
2. Run the playbook:

```
ansible-playbook -i hosts.ini site.yml
```

## Roles

### base
Performs basic system configuration:
- Updates apt cache
- Installs basic packages (vim, curl)

Variables:
- `packages`: list of packages to install

### web
Installs and configures Apache web server.
- Installs apache2
- Starts and enables the service

Variables:
- `apache_port`: Apache listening port
- `apache_document_root`: Apache document root directory

### database
Installs and configures MySQL database.
- Installs mysql-server
- Creates database and user for the application

Variables:
- `mysql_packages`: list of mysql packages
- `mysql_root_password`: MySQL root password
- `mysql_db_name`: database name
- `mysql_user`: database user
- `mysql_password`: database password

### php
Installs PHP and integrates with Apache.
- Installs PHP, libapache2-mod-php, php-mysql
- Enables PHP module in Apache

Variables:
- `php_packages`: list of php packages

### app
Deploys a sample PHP application.
- Deploys index.php that connects to the database and displays MySQL version

Variables:
- `app_dir`: directory to deploy the app
- `mysql_db_name`, `mysql_user`, `mysql_password`: database connection details

## Customization

To customize, edit the variables in roles/*/defaults/main.yml or override in group_vars/all.yml (for global variables) or inventory/group_vars.
