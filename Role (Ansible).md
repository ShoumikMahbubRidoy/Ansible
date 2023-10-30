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
2. **Tasks:** The `tasks` directory contains the YAML files that define the tasks to be executed. These tasks are the actual steps your role will perform. Example:
    ```bash
    /roles
    /web_server
        /tasks
            - main.yml
    ```
    In `main.yml`, you'd define tasks like installing software, configuring settings, and managing services.
3. **Templates:** The `templates` directory holds template files. Templates are used to dynamically generate configuration files by substituting variables. Example:
    ```bash
    /roles
    /web_server
        /templates
            - config_template.j2
    ```
4. **Vars (Variables):** The vars directory contains YAML files with variables specific to the role. These variables can be used in tasks and templates to make your role more flexible. Example:
    ```bash
    /roles
    /web_server
        /vars
            - main.yml
    ```
    In `main.yml`, you'd define variables such as `web_port` or `install_path`.
5. **Defaults:** The `defaults` directory holds default variable values for your role. These are used when no other values are provided. Example:
    ```bash
    /roles
    /web_server
        /defaults
            - main.yml
    ```
    Default values are useful to ensure your role works out-of-the-box without needing to specify every variable.
6. **Meta:** The meta directory contains metadata about your role, such as its dependencies. Example:
    ```bash
    /roles
    /web_server
        /meta
            - main.yml
    ```
    In `main.yml`, you'd specify any roles that your role depends on.

So, to create an Ansible role, you'd start with this directory structure, define tasks, variables, and templates in the respective directories, and then use your role to automate specific tasks on remote servers. This structured approach makes your automation projects more organized and easier to manage, especially as they become more complex.

## Directory Structure:
Before we dive into the playbook, let's first understand the directory structure that you mentioned:

```bash
/your_project_directory
   /roles
      /role_1
      /role_2
   /playbooks
      - orchestrate.yml
   /war_files
      - your_app.war
```
In this structure:

- `/your_project_directory` is the main directory where you keep your project files.
- `/roles` is where you store your Ansible roles (e.g., `role_1` and `role_2`).
- `/playbooks` contains your playbook `orchestrate.yml`.
- `/war_files` is a directory where you have your application's `.war` file that you want to deploy.
Now, let's elaborate on the playbook and roles with a detailed example:

### Example Playbook (`orchestrate.yml`):

Here's a detailed explanation of an example playbook that deploys a WAR file to a remote server using two roles:
```yaml
---
- name: Deploy WAR File
  hosts: your_target_host  # Replace with the name or group of hosts you want to target

  roles:
    - role_1
    - role_2

  tasks:
    - name: Copy WAR file to the remote server
      copy:
        src: /your_project_directory/war_files/your_app.war
        dest: /path/on/remote/server/your_app.war
      become: yes  # This ensures the task is executed with sudo (admin) privileges on the remote server

    - name: Restart the application server
      service:
        name: your_application_server
        state: restarted
      become: yes
```
**Explanation:**
- **`name`:** A descriptive name for your playbook.
- **`hosts`:** This defines the target hosts where you want to deploy your WAR file. You can specify a hostname, IP address, or a group of hosts from your Ansible inventory file. Replace your_target_host with your actual target.
- **`roles`:** This section specifies which roles to apply to the target hosts. In this example, we are applying role_1 and role_2 to the target host.
- **`tasks`:** These are additional tasks that are not part of the roles but are specific to this playbook.
    - The first task copies your .war file from your local machine to the remote server using the copy module. Make sure to replace /your_project_directory/ and /path/on/remote/server/ with actual paths.
    - The second task restarts the application server where you deployed the WAR file using the service module. Replace your_application_server with the actual service name on your remote server.
