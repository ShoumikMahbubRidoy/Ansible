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

## Ansible Playbooks(Ansibleプレイブック):
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
### YAML Document Separator (文書セパレータ) (---)

The `---` at the beginning of the file is a YAML document separator, indicating the start of a new YAML document.

### List of Plays プレイのリスト

A play in Ansible is a section of tasks that are run on a specific set of hosts. In this playbook, there is a single play, which is represented by a list (a sequence in YAML).

### Play Metadata プレイのメタデータ

- `name` is a key that assigns a name to the play. It's a description of what this play does. 

### Hosts ホスト

- `hosts` is a key that specifies which hosts this play will target. In this case, it targets hosts labeled as "webservers".  

### Tasks List タスクリスト

- `tasks` is a key that defines a list of tasks to be executed in this play.  

### Task Definitions タスクの定義

Each task is represented as a dictionary with several key-value pairs:

- `name` provides a human-readable name for the task. 
- `become` is a key with a boolean value (`yes`). It indicates that the task should run with elevated privileges (like using sudo). 
- `apt` is the module used to manage packages in Ubuntu/Debian-based systems.
  - `name` specifies the name of the package to be installed (`apache2`).
  - `state` specifies that the package should be in a "present" state.
- `service` is the module used to manage services.
  - `name` specifies the service name (`apache2`).
  - `state` specifies that the service should be "started."
- `copy` is the module used to copy files.
  - `src` is the source path of the local HTML files.
  - `dest` is the destination path on the remote host where the HTML files should be copied.
This playbook, when executed, will install the Apache web server, start the Apache service, and copy HTML files to the specified directory on the target hosts labeled as "webservers." It demonstrates key-value pairs, lists, boolean values, and the modular structure of an Ansible playbook.

To run this playbook, you'd use the `ansible-playbook` command:
```shell
ansible-playbook -i inventory_file webserver_playbook.yml
```
This command tells Ansible to execute the tasks defined in the playbook on the servers specified in the inventory.

In summary, ad-hoc commands are for quick, one-off tasks, while Ansible playbooks are used for more complex and automated tasks that you can run repeatedly. Playbooks are especially useful for configuration management and deployment, where you need consistency and repeatability in your server management tasks.

## Parallelism 並列処理:

Parallelism in Ansible allows you to execute tasks on multiple servers simultaneously. This can speed up operations, especially when you need to perform actions like rebooting multiple servers. In this example, we want to reboot servers in the "abc" group using 12 parallel forks, which means you'll reboot up to 12 servers at a time.
## SSH Agent and Authentication:

Before running Ansible commands, you should ensure that your SSH agent is set up and your SSH key is added for authentication. The SSH agent is a program that manages your SSH keys securely, so you don't have to type your SSH passphrase repeatedly. Here's how you set it up:

1. Start an SSH agent and open a new shell session:
   ```shell
   ssh-agent bash
   ```
2. Add your SSH key to the agent:
   ```shell
   ssh-add ~/.ssh/id_rsa
   ```
Now, you're ready to run Ansible commands with SSH authentication.

**Running Ad-hoc Reboot Commands (アドホック再起動コマンドの実行):**
To reboot servers in the "abc" group using 12 parallel forks, you can use the following Ansible ad-hoc command:
```shell
ansible abc -a "/sbin/reboot" -f 12
```
**Here's a breakdown of the command:**
- `ansible`: This is the Ansible command.
- `abc`: It specifies that you want to target the servers in the "abc" group from your Ansible inventory.
- `-a "/sbin/reboot"`: This is the actual command you want to run, which is "/sbin/reboot." It will initiate a server reboot.
- `-f 12`: This flag specifies that you want to run the reboot command on up to 12 servers in parallel.

By running this command, Ansible will log in to the servers in the "abc" group and execute the "/sbin/reboot" command on up to 12 servers at a time.

**Changing the Username (ユーザー名の変更):**
By default, Ansible will use your current user account for SSH authentication. If you want to specify a different username, you can do so using the `-u` option. For example, if your username is "username," you can use the following command:
```shell
ansible abc -a "/sbin/reboot" -f 12 -u username
```
This will ensure that Ansible uses the "username" for SSH authentication when connecting to the servers in the "abc" group.

In summary, parallelism allows you to perform tasks on multiple servers simultaneously, and setting up the SSH agent and specifying the username are essential for secure and efficient server management with Ansible ad-hoc commands.

## File/Folder/Directory Management ファイル/フォルダ/ディレクトリの管理
### Transferring Files (ファイルの転送):

You can use Ansible ad-hoc commands to securely copy files to multiple servers in parallel. Explaining how to use Ansible ad-hoc commands for file transfer, creating directories, and deleting files and directories with examples for a beginner. In this example, we'll transfer a file from your local machine to multiple servers in the "abc" group:
```shell
ansible abc -m copy -a "src=/path/to/local/file dest=/tmp/remote-file"
```
- `ansible`: This is the Ansible command.
- `abc`: It specifies that you want to target the servers in the "abc" group from your Ansible inventory.
- `-m copy`: This indicates that you want to use the "copy" module for file transfer.
- `-a "src=/path/to/local/file dest=/tmp/remote-file"`: This is where you specify the source and destination of the file you want to copy. It will copy the file from your local machine to `/tmp/remote-file` on each server in the "abc" group.

### Creating a New Directory:

You can use Ansible ad-hoc commands to create directories on multiple servers. In this example, we'll create a new directory with specific permissions and ownership:
```shell
ansible abc -m file -a "dest=/path/user1/new mode=777 owner=user1 group=user1 state=directory"
```
- `ansible`: The Ansible command.
- `abc`: Targeting the "abc" group of servers.
- `-m file`: Using the "file" module for file system operations.
- `-a "dest=/path/user1/new mode=777 owner=user1 group=user1 state=directory"`: Here, you specify the destination path for the new directory, set its permissions to 777, and define the owner and group as "user1." The `state=directory` option indicates that you want to create a directory.

### Deleting a Directory and Files:

You can also use Ansible ad-hoc commands to delete directories and their contents on multiple servers. In this example, we'll delete a directory and its files:
```shell
ansible abc -m file -a "dest=/path/user1/new state=absent"
```
- `ansible`: The Ansible command.
- `abc`: Targeting the "abc" group of servers.
- `-m file`: Using the "file" module for file system operations.
- `-a "dest=/path/user1/new state=absent"`: Here, you specify the destination path for the directory you want to delete, and `state=absent` indicates that you want to remove the directory and its contents.

## Package Management
### Checking if a Yum Package is Installed:

You can use Ansible ad-hoc commands to check if a package is installed on multiple servers without updating it. In this example, we'll check if the package named "demo-tomcat-1" is installed on servers in the "abc" group:
```shell
ansible abc -m yum -a "name=demo-tomcat-1 state=present"
```
- `ansible`: This is the Ansible command.
- `abc`: It specifies that you want to target the servers in the "abc" group from your Ansible inventory.
- `-m yum`: This indicates that you want to use the yum module for package management.
- `-a "name=demo-tomcat-1 state=present"`: Here, you specify the package name as "demo-tomcat-1" and set the state to "present," which means you want to check if the package is installed.

### Checking if a Yum Package is Not Installed:

You can also use Ansible ad-hoc commands to check if a package is not installed on multiple servers. In this example, we'll check if the package named "demo-tomcat-1" is not installed on servers in the "abc" group:
```shell
ansible abc -m yum -a "name=demo-tomcat-1 state=absent"
```
- `ansible`: The Ansible command.
- `abc`: Targeting the "abc" group of servers.
- `-m yum`: Using the yum module for package management.
- `-a "name=demo-tomcat-1 state=absent"`: Here, you specify the package name as "demo-tomcat-1" and set the state to "absent," which means you want to check if the package is not installed.

### Checking for the Latest Version of a Yum Package:

You can also use Ansible ad-hoc commands to ensure that the latest version of a package is installed on multiple servers. In this example, we'll check if the latest version of the package named "demo-tomcat-1" is installed on servers in the "abc" group:
```shell
ansible abc -m yum -a "name=demo-tomcat-1 state=latest"
```
- `ansible`: The Ansible command.
- `abc`: Targeting the "abc" group of servers.
- `-m yum`: Using the yum module for package management.
- `-a "name=demo-tomcat-1 state=latest"`: Here, you specify the package name as "demo-tomcat-1" and set the state to "latest," which means you want to ensure that the latest version of the package is installed.

These ad-hoc commands allow you to manage packages using `yum` on multiple servers easily. They are useful for checking the status of packages, ensuring the presence or absence of packages, and updating packages to their latest versions, making software management more efficient.

## Gathering System Facts:

Ansible can collect various pieces of information about the remote servers, such as operating system details, hardware information, network configuration, and more. This information is called "facts." Gathering facts is useful for implementing conditional statements in your playbooks or for understanding the state of your remote servers.

To gather facts about all your servers, you can use the following Ansible ad-hoc command:
```shell
ansible all -m setup
```
- `ansible`: This is the Ansible command.
- `all`: It specifies that you want to target all servers defined in your inventory.
- `-m setup`: This indicates that you want to use the "setup" module, which is designed to gather system facts.

**Example:**

Suppose you have a group of servers in your inventory, and you want to gather facts about them. Here's how you can do it with the Ansible ad-hoc command:
```shell
ansible all -m setup
```
When you run this command, Ansible will connect to each server in your inventory and collect a wide range of facts about each system. These facts can include information about the server's hardware, operating system, network configuration, and more. Ansible will then display this information on your screen.

Here's a simplified example of the kind of information you might receive:
```json
{
    "ansible_facts": {
        "ansible_distribution": "Ubuntu",
        "ansible_os_family": "Debian",
        "ansible_processor": "x86_64",
        "ansible_kernel": "4.19.104",
        "ansible_hostname": "server1",
        "ansible_default_ipv4": {
            "address": "192.168.1.100",
            "interface": "eth0"
        },
        "ansible_default_ipv6": {
            "address": "fe80::abcd:1234",
            "interface": "eth0"
        },
        // ... more facts
    }
}
```
This JSON represents a set of facts about a server. Let's go through each part step by step:
- `"ansible_facts"`: This is the root key of the JSON object and indicates that the data inside it contains Ansible facts.
- `"ansible_distribution"`: This fact provides information about the Linux distribution running on the server. In this example, the server is running Ubuntu.
- `"ansible_os_family"`: This fact provides information about the family of the operating system. In this case, it's "Debian," which is the family to which Ubuntu belongs.
- `"ansible_processor"`: This fact tells you about the CPU architecture of the server. Here, it's "x86_64," indicating a 64-bit processor.
- `"ansible_kernel"`: This fact specifies the kernel version of the operating system. The kernel is a critical part of the operating system. Here, it's version "4.19.104."
- `"ansible_hostname"`: This fact provides the hostname of the server. In this case, the server's hostname is "server1."
- `"ansible_default_ipv4"`: This part of the facts provides information about the default IPv4 address and associated network interface on the server. The address is "192.168.1.100," and the interface is "eth0."
- `"ansible_default_ipv6"`: Similar to the IPv4 fact, this provides information about the default IPv6 address and associated network interface. The IPv6 address is "fe80: :abcd:1234," and the interface is "eth0."
  These are just a few of the many facts that Ansible can collect. You can use these facts in your Ansible playbooks to make decisions and perform specific tasks based on the characteristics of the target server. For instance, you could use `"ansible_distribution"` to install distribution-specific packages or `"ansible_default_ipv4"` to configure network settings. Facts provide valuable information that helps you automate server management effectively.

You can use these facts in your playbooks to make decisions based on the characteristics of your servers. For example, you might use facts like the operating system to install specific software packages or use facts about the server's IP address for network configuration.

In summary, gathering facts using Ansible is a valuable feature that provides you with detailed information about your servers, which you can then use to make informed decisions in your automation tasks.


# アドホックコマンド
Ansibleのアドホックコマンドは、リモートサーバー上で特定のタスクを実行するための、素早い一度性の指示と考えることができます。これらは、自動化したり頻繁に繰り返す必要のないタスクに使用されます。

たとえば、会社のすべてのサーバーを再起動する必要がある場合、Ansibleアドホックコマンドを使用できます。次のようなコマンドを使用します：
```shell
ansible all -i inventory_file -m shell -a "reboot"
```
これを分解してみましょう：
- `ansible`：これはAnsibleコマンドです。
- `all`：これは、インベントリで定義されたすべてのサーバーを対象にしたいことを指定します。
- `-i inventory_file`：ここでは、管理対象のサーバーリストを含むインベントリファイルを指定します。
- `-m shell`：これはAnsibleに「shell」モジュールを使用するように指示し、リモートサーバー上でシェルコマンドを実行するようにします。
- `-a "reboot"`：これは実際に実行したいコマンドで、ここでは「reboot」です。このコマンドはサーバーを再起動します。
このコマンドにより、Ansibleはインベントリ内のすべてのサーバーにログインし、「reboot」コマンドを実行して、サーバーを再起動します。

## Ansibleプレイブック:
アドホックコマンドは簡単なタスクに適していますが、Ansibleプレイブックはより複雑で、繰り返し可能な自動化タスクに使用されます。プレイブックは、Ansibleが1つまたは複数のサーバー上で実行するべき手順またはタスクの一連を記述したスクリプトのようなものです。

たとえば、複数のサーバーにWebサーバーをインストールして設定する必要がある場合、これを実行するAnsibleプレイブックを作成できます。次は、プレイブックの簡略化された例です：
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
この例では次のようになります：
### YAML Document Separator (文書セパレータ) (---)
ファイルの先頭にある「---」はYAML文書セパレータで、新しいYAML文書の開始を示しています。
### List of Plays プレイのリスト

Ansibleのプレイは、特定のホストセットに対して実行されるタスクのセクションです。このプレイブックには、リスト（YAMLでのシーケンス）で表現された1つのプレイがあります。

### Play Metadata プレイのメタデータ

- `name` はプレイに名前を割り当てるキーで、プレイが何を行うかを説明します。

### Hosts ホスト

- `hosts`は、このプレイが対象とするホストを指定するキーです。この場合、 "webservers" とラベル付けされたホストを対象にします。

### Tasks List タスクリスト

- `tasks`は、このプレイで実行されるタスクのリストを定義するキーです。

### Task Definitions タスクの定義

各タスクは、いくつかのキーと値のペアを持つ辞書として表現されます：
- `name`はタスクに対して人が読みやすい名前を提供します。
- `become`はブール値(`yes`)を持つキーで、タスクがスーパーユーザー権限（sudoの使用など）で実行されるべきことを示します。
- `apt`はUbuntu / Debianベースのシステムでパッケージを管理するためのモジュールです。
  - `name`はインストールするパッケージの名前（apache2）を指定します
  - `state`はパッケージが "present"（インストール済み）の状態であるべきことを指定します。
- `service`はサービスを管理するためのモジュールです。
  - `name`はサービスの名前(`apache2`)を指定します。
  - `state`はサービスが "started"（開始済み）であるべきことを指定します。
-  `copy`はファイルのコピーに使用するモジュールです。
  - `src`はローカルのHTMLファイルのソースパスを指定します。
  - `dest`はHTMLファイルがコピーされるリモートホスト上のディレクトリのパスを指定します。
このプレイブックは実行されると、Apacheウェブサーバーをインストールし、Apacheサービスを開始し、HTMLファイルを指定されたディレクトリにコピーします。これは、Ansibleプレイブックのキー-値ペア、リスト、ブール値、およびモジュールの構造をデモンストレーションしています。

このプレイブックを実行するには、`ansible-playbook`コマンドを使用します:
```shell
ansible-playbook -i inventory_file webserver_playbook.yml
```
このコマンドは、インベントリで指定されたサーバー上でプレイブックで定義されたタスクを実行するようにAnsibleに指示します。

要約すると、アドホックコマンドは素早いタスクに適しており、Ansibleプレイブックはより複雑で自動化されたタスクに使用されます。プレイブックは特に設定管理と展開に適しており、サーバー管理タスクに一貫性と繰り返し可能性が必要な場合に便利です。

## Parallelism 並列処理:

Ansibleの並列処理は、複数のサーバーでタスクを同時に実行できるようにします。これは特に複数のサーバーを再起動するなどのアクションを高速化するのに役立ちます。この例では、「abc」グループのサーバーを12個の並列フォークで再起動することを考えています。これは、最大で12台のサーバーを同時に再起動することを意味します。

## SSH Agent and Authentication SSHエージェントと認証:

Ansibleコマンドを実行する前に、SSHエージェントが設定され、SSHキーが認証に追加されていることを確認する必要があります。SSHエージェントはSSHキーを安全に管理するプログラムで、SSHパスフレーズを繰り返し入力する必要がないようにします。セットアップ方法は以下の通りです：

1. SSHエージェントを起動し、新しいシェルセッションを開始します:
   ```shell
   ssh-agent bash
   ```
2. SSHキーをエージェントに追加します:
   ```shell
   ssh-add ~/.ssh/id_rsa
   ```
これで、SSH認証を使用してAnsibleコマンドを実行する準備が整いました。

**Running Ad-hoc Reboot Commands (アドホック再起動コマンドの実行):**
「abc」グループのサーバーを12個の並列フォークで再起動するには、次のAnsibleアドホックコマンドを使用できます：
```shell
ansible abc -a "/sbin/reboot" -f 12
```
**Here's a breakdown of the command (このコマンドの詳細):**
- `ansible`：これはAnsibleコマンドです。
- `abc`：これはAnsibleインベントリで定義された「abc」グループのサーバーを対象にすることを指定します。
- `-a "/sbin/reboot"`：これは実際に実行したいコマンドで、"/sbin/reboot" です。これによりサーバーが再起動されます。
- `-f 12`：このフラグは、再起動コマンドを最大で12台のサーバーで並列に実行することを指定します。

このコマンドを実行することで、Ansibleは「abc」グループのサーバーにログインし、最大で12台のサーバーで "/sbin/reboot" コマンドを実行します。

**Changing the Username (ユーザー名の変更):**
デフォルトでは、AnsibleはSSH認証に現在のユーザーアカウントを使用します。異なるユーザー名を指定する場合、 `-u`オプションを使用できます。たとえば、ユーザー名が「username」である場合、次のコマンドを使用できます：
```shell
ansible abc -a "/sbin/reboot" -f 12 -u username
```
これにより、Ansibleは「abc」グループのサーバーへの接続時に「username」を使用するようになります。

要約すると、並列処理は複数のサーバーでタスクを同時に実行できるようにし、SSHエージェントを設定し、ユーザー名を指定することは、Ansibleアドホックコマンドを使用したセキュアかつ効率的なサーバー管理にとって重要です。

## File/Folder/Directory Management ファイル/フォルダ/ディレクトリの管理
### Transferring Files (ファイルの転送):

Ansibleのアドホックコマンドを使用して、ファイルを複数のサーバーに安全にコピーすることができます。ファイル転送に関するAnsibleアドホックコマンド、ディレクトリの作成、ファイルおよびディレクトリの削除について説明し、初心者向けの例を示します。この例では、ローカルマシンから「abc」グループの複数のサーバーにファイルを転送します：
```shell
ansible abc -m copy -a "src=/path/to/local/file dest=/tmp/remote-file"
```
- `ansible`：これはAnsibleコマンドです。
- `abc`：これはAnsibleインベントリで定義された「abc」グループのサーバーを対象にすることを指定します。
- `-m copy`：これはファイル転送に「copy」モジュールを使用することを示します。
- `-a "src=/path/to/local/file dest=/tmp/remote-file"`：これはコピーするファイルのソースと宛先を指定する場所です。それにより、ファイルがローカルマシンから「abc」グループ内の各サーバーの「`/tmp/remote-file`」にコピーされます。
