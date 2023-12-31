# Basic of Ansible: Simplifying IT Automation

## What is Ansible?

Ansible is like a helpful robot for IT tasks. It can do many things automatically, such as setting up software, managing servers, and more. It's open source, meaning it's free for anyone to use.

## How Ansible Works

Ansible doesn't need special software on the computers it's working with. It uses a simple language called YAML to give it instructions. YAML looks like this:

```yaml
---
- name: Example Task
  hosts: web_servers
  tasks:
    - name: Install Apache
      apt:
        name: apache2
        state: present
```
In this example, Ansible is instructed to install the Apache web server on machines in the "web_servers" group.

#### Example Explained:

Let's say you have a bunch of web servers (like "web_servers"), and you want to make sure they all have the Apache web server installed. You create an Ansible playbook like the one you provided.

- `name: Example Task`: This is the name of the task you're performing. It's like a title for this step in your playbook.
- `hosts: web_servers`: It tells Ansible which group of servers this task should be performed on. In this case, it's the group named "`web_servers`".
- `tasks`: This is where you define what you want to do on those servers.
- `- name: Install Apache`: Another name for the specific task you're doing.
- `apt`: Here, you're telling Ansible to use the apt module, which deals with package management.
- `name: apache2`: This specifies the name of the package you want to work with, in this case, "`apache2`".
- `state: present`: This means you want to ensure that the "`apache2`" package is installed (i.e., in a "`present`" state).

## Agentless Approach
Unlike some other automation tools, Ansible doesn't need to install anything on the computers it's managing. It connects to them using SSH, like how you might log in remotely to a computer

## Playbooks
Ansible instructions are organized into something called "playbooks." Think of a playbook like a script that tells Ansible what to do. Here's an example of a simple playbook:

```yaml
---
- name: Configure Web Server
  hosts: web_servers
  tasks:
    - name: Install Apache
      apt:
        name: apache2
        state: present
    - name: Start Apache Service
      service:
        name: apache2
        state: started
```
In this playbook, Ansible will install Apache and start the Apache service on the computers in the "web_servers" group.

#### Example Explained: (Ansible Playbook: Configure Web Server)

This Ansible playbook is like a set of instructions for configuring web servers. Let's break it down:

**1. Playbook Name**:
- `name: Configure Web Server`: This line gives a name to the entire playbook. Think of it as a title for the tasks you want to perform. In this case, it's all about configuring web servers.
**2. Hosts**:
- `hosts: web_servers`: Here, you specify the group of servers you want to configure, known as "`web_servers`" The tasks in this playbook will be executed on all the servers within this group.
**3. Tasks**:
Under the "tasks" section, you list the specific actions or tasks you want to perform on the selected servers.

**Task 1 - Install Apache**:
- `name: Install Apache`: This is a descriptive label for the task.
- `apt`: This is the Ansible module for managing software packages.
- `name: apache2`: It specifies the package you want to work with, in this case, "`apache2`" It means you want to ensure that the Apache web server package is installed on the servers.
- `state: present`: This part tells Ansible to ensure that the "`apache2`" package is present (installed) on the servers. If it's not installed, Ansible will take care of installing it.

**Task 2 - Start Apache Service**:
- `name: Start Apache Service`: Another descriptive label for this task.
- `service`: This is the Ansible module used for managing services on the servers.
- `name: apache2`: It specifies the service you want to work with, which is the "`apache2`" service.
- `state: started`: Here, you're telling Ansible to ensure that the "`apache2`" service is in a "started" state. If it's not running, Ansible will start it.

**In Simple Terms:**
This Ansible playbook is like a to-do list for configuring web servers. It ensures that the Apache web server is both installed and running on all the servers within the "`web_servers`" group. It's like having a step-by-step recipe for setting up a web server, and Ansible follows the recipe on all the selected servers.

By using this playbook, you can easily configure and manage your web servers without manual intervention. It's automation magic for IT tasks!

## Multi-Tier Deployment
Ansible is good at managing many computers that work together. For example, it can set up a web server, a database server, and connect them properly. Imagine you're building a house. Instead of focusing on just one brick at a time, Ansible helps you see the whole structure and how the bricks fit together.

## Inventory
Ansible keeps track of the computers it manages in something called an "inventory." An inventory is like a list of computers and groups of computers. Here's a simple example:

```yaml
web_servers:
  192.168.1.10
  192.168.1.11

db_servers:
  192.168.1.12
```
In this inventory, we have two groups: "`web_servers`" and "`db_servers`" and each group has the IP addresses of the computers.

### Groups:
In this inventory, you have two groups: "`web_servers`" and "`db_servers`" Think of groups as categories for your machines. You can put machines with similar roles or functions in the same group.
- **`web_servers:`** This group includes servers that are meant for handling web-related tasks, like hosting a website. In this group, you have two servers with the IP addresses 192.168.1.10 and 192.168.1.11.
- **`db_servers:`** This group includes servers that are meant for handling database-related tasks. In this group, you have one server with the IP address 192.168.1.12.

### Why Groups Matter:
Groups are useful because they allow you to apply configurations or tasks to a specific set of machines. For example, if you have web-related tasks to perform, you can target the "`web_servers`" group, and Ansible will perform those tasks on all machines in that group. It's like sorting your contacts into groups on your phone to send messages to specific sets of people.

**In Simple Terms:** Imagine you have a big toolbox, and inside the toolbox, you want to group your tools. You have one section for tools used for carpentry (`web_servers`) and another for tools used for plumbing (`db_servers`). The IP addresses are like the labels on the tools, so you can easily find the right tool when you need it.
So, the inventory file helps Ansible know which machines are part of which group, making it easier to manage and perform tasks on those machines. It's like having a well-organized toolbox for your IT tasks.
So, Ansible makes IT tasks easier by using plain text instructions (YAML playbooks), connecting to computers remotely without needing special software, and helping manage multiple computers working together. It's like having a friendly robot to handle repetitive tasks and ensure your IT systems run smoothly.

# Ansible Hosts File: Managing Your Server Inventory

## What is a Hosts File in Ansible?

In Ansible, the hosts file is like a contact list that tells Ansible which computers it should manage and how to connect to them. Each computer is referred to as a "host" Here's an example of a simple hosts file:

```yaml
# File name: hosts
# Description: Inventory file for your application. Defines machine type abc node to deploy specific artifacts.
# Defines machine type def node to upload metadata.

[abc-node]
server1 ansible_host=<target machine for DU deployment> ansible_user=<Ansible user> ansible_connection=ssh

[def-node]
server2 ansible_host=<target machine for artifact upload> ansible_user=<Ansible user> ansible_connection=ssh
```

# Understanding the Ansible Hosts File

The Ansible hosts file is a crucial component for managing your servers and defining how Ansible should connect to them. Let's break down the key elements of this file:

## Group Names
In your hosts file, group names are enclosed in square brackets, like `[abc-node]` and `[def-node]`. These groups act as categories to organize your hosts.

## Host Names
Host names are the individual computers or servers you want to manage. In your example, you have `server1` and `server2`. Each host belongs to a specific group, e.g., `server1` is part of the `[abc-node]` group, and `server2` is in the `[def-node]` group.

## Connection Variables
Within the hosts file, you define connection variables to specify how Ansible should connect to each host. These variables include:
- `ansible_host`: This is the target machine's IP address or hostname.
- `ansible_user`: It specifies the username Ansible should use for logging in to the machine.
- `ansible_connection`: This variable specifies the connection method; in your case, it's set to "ssh" for secure remote connections.

### Practical Examples

Imagine you have two servers, one for deploying a software update (DU) and another for uploading metadata:

- For the DU deployment server (`server1`), the hosts file instructs Ansible to connect to it via SSH using the provided username. When you create Ansible playbooks, you can refer to `[abc-node]` to define actions for this server, like deploying software updates.

- For the metadata upload server (`server2`), the hosts file similarly specifies connection details. You can use `[def-node]` in your playbooks to define tasks for this server, such as uploading metadata files.

In simple terms, the hosts file is like a phone book for Ansible. It helps Ansible locate your computers, understand their identities, and determine how to connect to them. This organization simplifies Ansible's task of managing different machines in your network effectively.

# Understanding Configuration Management with Ansible

## What is Configuration Management?

Configuration management is like having a digital memory for your computers. It keeps track of all the details about the software and hardware on your machines. This includes things like what software is installed, which versions are used, and where your hardware is located.

## How Ansible Helps with Configuration Management

Imagine you have a bunch of computers in your company, and you want to make sure they all have the same software, like a new version of WebLogic or WebSphere server. Doing this manually on each computer is a huge task, and it's easy to make mistakes.

Here's where Ansible comes to the rescue!

With Ansible, you can create what's called a "playbook." A playbook is like a set of instructions for Ansible to follow. It's like giving a recipe to a chef. In this case, the recipe is for installing software on your computers.

### Simple Example:

```yaml
---
- name: Install WebLogic
  hosts: your_computers
  tasks:
    - name: Download WebLogic Installer
      get_url:
        url: "https://example.com/weblogic-installer.exe"
        dest: "/tmp/weblogic-installer.exe"
    
    - name: Install WebLogic
      command: "/tmp/weblogic-installer.exe"
```
In this example playbook:

- "`Install WebLogic`" is the name of the task.
- "`your_computers`" is where you list the IP addresses or names of your computers.
- The playbook tells Ansible to download the WebLogic installer from a website and install it.

## Getting Started

To get started with Ansible's configuration management magic, follow these simple steps:

1. **Create Your Playbook**: Write a playbook like the example provided. Specify the tasks you want to automate.
2. **Define Your Inventory**: Update your inventory file with a list of your target computers (IP addresses or names). This is where Ansible will work its magic.
3. **Run the Playbook**: Execute the playbook from your control machine. Ansible will take care of the rest, making sure all your machines are up to date and consistent.

That's it! Ansible becomes your super-efficient assistant, ensuring all your computers have the same software and configurations. You provide the recipe (playbook), and Ansible handles the hard work. It's like magic for IT tasks!

# How Ansible Works
Think of Ansible as a smart messenger that helps you manage and control many computers at once. Here's how it works:

## Controlling Node
The controlling node is your computer, the one you're using to control Ansible. Think of it as your command center.

## Inventory
You create a list of all the computers you want to manage. This list is called the "inventory." It's like making a guest list for a party and deciding who to invite.

## Modules
Ansible uses little programs called "modules." These modules are like tools in a toolbox. Each module does a specific job, like installing software, restarting a server, or copying files. You can think of them as magical helpers.

## Execution
Ansible connects to the computers in your inventory. It's like calling your friends to join the party. Then, Ansible sends the right modules to each computer, telling them what to do. For example, it might send an "Install Web Server" module to install a web server.

## Cleaning Up
Once the work is done, Ansible is polite and cleans up after itself. It removes the modules from the computers. It's like your friends leaving the party when it's over.

## Example
Imagine you have ten computers in your office, and you want to update the software on all of them to the latest version. Using Ansible, you would:
1. Create an inventory with the names or IP addresses of those ten computers.
2. Write a playbook (like a to-do list) that tells Ansible to use the "Update Software" module on all the computers.
3. Run the playbook from your computer.

<img src="./Ansible.PNG" />

Ansible would connect to each of the ten computers, send the "Update Software" module, and ensure that the software is updated. When it's all done, Ansible would clean up by removing the modules.

So, Ansible is like your digital assistant, helping you manage and maintain your computers without needing any fancy servers or databases. It's as simple as making a phone call to your friends and asking them to help out at a party, but in this case, your friends are modules, and the party is managing your computers.
