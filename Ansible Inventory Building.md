# Ansible Inventory 

## Overview

This README explains the concept of Ansible inventory and provides an example of how to create a static host inventory using a real-world scenario.

## What is Ansible Inventory?

Ansible inventory is a crucial component in Ansible, helping you manage the hosts you want to automate tasks on. It defines a collection of hosts, which can be grouped, organized, and assigned variables. There are two main types of Ansible inventory:

1. **Static Host Inventory**: Manually created text files with a list of hosts, groups, and variables. Suitable for a set of servers that don't change frequently.

2. **Dynamic Host Inventory**: Generated dynamically using Ansible plugins based on external information sources. Ideal for large, dynamic environments with frequently changing hosts.

## Example: Managing Servers in a Web Hosting Company

Imagine you're a system administrator responsible for managing servers in a web hosting company. You have three types of servers: web servers, database servers, and backup servers. Here's how to define a static host inventory for these servers.

### Static Host Inventory Example

```ini
[web_servers]
webserver1.example.com
webserver2.example.com

[db_servers]
dbserver1.example.com

[backup_servers]
backupserver1.example.com
backupserver2.example.com

[all_servers:children]
web_servers
db_servers
backup_servers
```
### Example Explanation

In the provided example:

- `[web_servers]`, `[db_servers]`, and `[backup_servers]` are **groups**. Groups are used to categorize hosts for organizational purposes.
- `webserver1.example.com`, `webserver2.example.com`, and so on, are **individual servers**. These are the specific hosts you want to manage.
- `[all_servers:children]` is a special group that includes **all the servers** defined in the inventory. It's a way to create a group of groups.

You can also define **variables** for specific servers or groups, allowing you to customize settings for each server. For example, you can set SSH port, user, or other configuration options.

## Static Inventory vs. Dynamic Inventory

**Static inventory** is a straightforward approach for managing a known set of servers. It involves manually creating a text file, as shown in the example, and is suitable when your host list is relatively stable.

For larger, dynamic environments where hosts are frequently created or destroyed, using **dynamic inventories** is more practical. Dynamic inventories, like the AWS EC2 inventory, can automatically generate host lists based on external sources.

## Summary

In summary, Ansible inventory is a fundamental concept that allows you to organize and manage your infrastructure effectively. By defining groups, individual hosts, and variables, you can streamline your automation workflows. Whether you're dealing with a small set of servers or a large, ever-changing environment, Ansible's inventory system can help you manage and automate tasks across your servers and devices.

## Managing Servers with Ansible: Static Inventory
### What is a Static Inventory?

In Ansible, a static inventory is a text file that lists the servers (managed hosts) you want to work with. It can be created in various formats, but we'll focus on the common INI-style format for this guide.

## Basic Inventory Format

In its simplest form, you can list the hostnames or IP addresses of the managed hosts in your inventory, with each host on a separate line. Consider our web hosting example:

```ini
webserver1.example.com
webserver2.example.com
dbserver1.example.com
dbserver2.example.com
backupserver1.example.com
backupserver2.example.com
```
