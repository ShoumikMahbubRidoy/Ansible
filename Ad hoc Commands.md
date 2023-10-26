# Ad-hoc Commands
Ad-hoc commands in Ansible are like quick, one-time instructions you can give to your servers. You can think of them as simple, direct commands that you run to do specific tasks on remote servers. They are often used for tasks that you don't need to automate or repeat frequently.

For example, let's say you need to reboot all the servers in your company. You can use Ansible ad-hoc commands to do this. The command you would use could look something like this:
```shell
ansible all -i inventory_file -m shell -a "reboot"
```
Let's break this down:
- `ansible`: This is the command to run Ansible.
- `all`: It specifies that you want to target all servers defined in your inventory.
- `-i inventory_file`: Here, you specify the inventory file that contains the list of servers you want to manage.
- `-m shell`: This tells Ansible to use the "shell" module, which is like running a shell command on the remote servers.
- `-a "reboot"`: This is the actual command you want to run, which is "reboot."
This command will instruct Ansible to log in to all the servers in your inventory and run the "reboot" command, effectively rebooting them.

## Ansible Playbooks:
While ad-hoc commands are great for quick tasks, Ansible playbooks are used for more complex, repeatable, and automated tasks. Playbooks are like scripts that describe a series of steps or tasks that Ansible should perform on one or more servers.

For example, if you need to install and configure a web server on multiple servers, you can create an Ansible playbook to do this. Here's a simplified example of what a playbook might look like:
```yaml
---
- name: Install and Configure Web Server
  hosts: webservers
  tasks:
    - name: Install Apache
      become: yes
      apt:
        name: apache2
        state: present

    - name: Start Apache Service
      become: yes
      service:
        name: apache2
        state: started

    - name: Copy HTML files
      copy:
        src: /path/to/local/html
        dest: /var/www/html
```
In this example:

- `name`: Describes the name of the playbook.
- `hosts`: Specifies which servers should be targeted, in this case, the group of servers labeled as "webservers" in your inventory.
- `tasks`: Contains a list of tasks that Ansible will execute.
Each task specifies what needs to be done, like installing Apache, starting the Apache service, and copying HTML files to the server.

To run this playbook, you'd use the `ansible-playbook` command:
```shell
ansible-playbook -i inventory_file webserver_playbook.yml
```
This command tells Ansible to execute the tasks defined in the playbook on the servers specified in the inventory.

In summary, ad-hoc commands are for quick, one-off tasks, while Ansible playbooks are used for more complex and automated tasks that you can run repeatedly. Playbooks are especially useful for configuration management and deployment, where you need consistency and repeatability in your server management tasks.
