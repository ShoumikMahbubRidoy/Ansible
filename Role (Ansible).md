# Role (Ansible)

## What is an Ansible Role?
An Ansible role is like a reusable set of tasks, templates, and variables that can be used to automate specific actions on remote servers. It's a way to organize and structure your Ansible automation code for better maintainability and reusability. Roles allow you to encapsulate a specific piece of functionality or configuration in a tidy package. Think of them as building blocks that you can use to construct your infrastructure automation.

## Why Use Ansible Roles?
Imagine you're managing a bunch of web servers, and they all need the same setup: installing a web server, configuring a firewall, setting up the application, and so on. Without roles, you'd need to write these tasks for each server individually, which can be time-consuming and error-prone. Roles allow you to define these tasks once and then apply them to multiple servers easily. They promote modularity, code reusability, and make your automation projects more organized.

## Ansible Role Directory Structure:
When you create an Ansible role, it should follow a specific directory structure. This structure helps Ansible know where to find your tasks, variables, and templates. Here's a breakdown of the key directories and their purposes:

1. **Role Directory (Role Name):** This is the root directory for your role, and its name should match the role's name. It's usually located within the `/roles` directory. This is where your role's content resides.
    Example:
    ```bash
    /roles
        /web_server
    ```
2. a
3. s
4. d
5. f
