# Apache VirtualHost Configuration with Ansible

## Table of Contents
- [Apache VirtualHost Configuration with Ansible](#apache-virtualhost-configuration-with-ansible)
  - [Table of Contents](#table-of-contents)
  - [Overview](#overview)
  - [Features](#features)
  - [Prerequisites](#prerequisites)
    - [System Requirements](#system-requirements)
    - [Required Ansible Collections](#required-ansible-collections)
  - [Installation](#installation)
  - [Project Structure](#project-structure)
  - [Configuration](#configuration)
    - [1. Inventory Setup](#1-inventory-setup)
    - [2. Group Variables](#2-group-variables)
    - [3. Virtual Hosts](#3-virtual-hosts)
  - [Usage](#usage)
    - [Basic Deployment](#basic-deployment)

## Overview

This Ansible project automates Apache (httpd) web server configuration with multiple virtualhosts, featuring custom logging, SSL configuration, and private directory authentication.

## Features

* **SELinux Configuration**
  * Custom port (88) configuration
  * Proper security contexts

* **Virtual Hosts Management**
  * Separate log files per virtualhost
  * Custom DocumentRoot configuration
  * SSL/TLS support

* **Security Features**
  * Private directories with basic authentication
  * IP-based access control
  * HTTPS redirection
  * Secure default settings

* **Logging**
  * Individual access and error logs
  * Automated log rotation
  * Custom log formats

## Prerequisites

### System Requirements
* Ansible 2.9+
* RHEL/CentOS 7/8
* Python 3.x
* Root/sudo access

### Required Ansible Collections
```bash
ansible-galaxy collection install community.general
```

## Installation


## Project Structure

```
.
├── README.md
├── inventory/
│   └── hosts
├── group_vars/
│   └── all.yml
├── roles/
│   └── apache_logging/
│       ├── tasks/
│       │   └── main.yml
│       ├── templates/
│       │   ├── virtualhost.conf.j2
│       │   └── logrotate.conf.j2
│       └── handlers/
│           └── main.yml
└── site.yml
```

## Configuration

### 1. Inventory Setup
```ini
# inventory/hosts
[webservers]
webserver1 ansible_host=192.168.1.10
```

### 2. Group Variables
```yaml
# group_vars/all.yml
apache_log_dir: /var/log/httpd
apache_user: apache
apache_group: apache
selinux_port: 88
allowed_ip: "192.168.1.100"
```

### 3. Virtual Hosts
```yaml
# site.yml
virtualhosts:
  - server_name: "example1.com"
    docroot: "/var/www/html/example1.com"
  - server_name: "example2.com"
    docroot: "/var/www/html/example2.com"
```

## Usage

### Basic Deployment
```bash
# Deploy with default settings
ansible-playbook -i inventory/hosts site.yml
```
