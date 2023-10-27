# Playbooks (Ansible)
## What is Ansible?
Ansible is an open-source automation tool used for configuration management, application deployment, and task automation. It allows you to manage and configure remote servers from a central control machine without the need for agents or additional software on the remote servers.

## What are Playbooks in Ansible?
Playbooks are files in Ansible where you define the tasks and instructions that Ansible needs to perform. These tasks are written in a human-readable format called YAML (Yet Another Markup Language). Playbooks serve as a kind of "script" for Ansible to execute, specifying what needs to be done on remote machines.

### Example of a Simple Playbook:
Let's say you have a group of web servers that need to have their Apache web server service started. You can create a playbook to define this task. Here's an example of what a simple playbook might look like:

```yaml
---
- name: Install and Configure DB
  hosts: testServer
  become: yes
  vars:
    oracle_db_port_value: 1521

  tasks:
    - name: Install the Oracle DB
      yum: 
        name: <code to install the DB>
    
    - name: Ensure the installed service is enabled and running
      service:
        name: <your service name>
```
### Understanding an Ansible Playbook

Let's break down an Ansible playbook step by step:

1. **Playbook Header (---):**
   - This `---` at the beginning is like a separator and indicates the start of a YAML document. It's just a technical thing to let Ansible know that the YAML document begins here.
2. **`name` (Name of the Playbook):**
   - This line specifies the name of the Ansible playbook. It's like giving a title to your playbook, so you can easily understand what this playbook is meant for. In this case, it's about installing and configuring a database.
3. **`hosts` (Target Hosts):**
   - Here, you specify the list of hosts or host groups where you want to run the tasks. Think of hosts as the computers or servers you want to manage. This playbook will run on the machine named `testServer`.
4. **`become: yes` (Privilege Escalation):**
   - This tells Ansible that it should escalate privileges to become a superuser, typically 'root'. This is necessary when you want to install software or manage services that require superuser permissions.
5. **`vars` (Variables):**
   - In this section, you can define variables like `oracle_db_port_value`. Variables are like placeholders where you can store values to use later in your playbook. Here, we're storing the Oracle database port number as `1521`.
6. **`tasks` (List of Actions):**
   - Every playbook should contain a list of tasks to be executed. Tasks are the actions you want to perform. In this playbook, there are two tasks:
     - **Task 1: Install the Oracle DB**: It uses the `yum` module to install the Oracle Database. You should replace `<code to install the DB>` with the actual command to install the database.
     - **Task 2: Ensure the installed service is enabled and running**: This task uses the `service` module to ensure that a specified service is enabled and running. Replace `<your service name>` with the actual name of the service you want to manage.

**In a nutshell:**
   - An Ansible playbook is like a to-do list for managing servers.
   - It starts with a name, tells Ansible which servers to work on, may need superuser powers, can use variables, and lists tasks to perform.

### How This Playbook Works:

When you run this playbook with Ansible, it will perform the following actions:
1. Connect to the `testServer` host.
2. Execute the task "Install the Oracle DB" by running the installation command you provide.
3. Execute the task "Ensure the installed service is enabled and running" to ensure that the specified service is running.

This example demonstrates the structure of a playbook and how it defines the tasks to be executed on a remote server, specifically installing and configuring an Oracle Database. Playbooks can be more complex and versatile, but this example gives you a starting point to understand how Playbooks work in Ansible.

This example is quite basic, but it shows the structure of an Ansible playbook. Playbooks can get more complex and powerful, but this should give you a newbie-friendly starting point for understanding how they work in Ansible.



# プレイブック（Ansible）
## Ansibleとは？
Ansibleは、構成管理、アプリケーションの展開、タスクの自動化に使用されるオープンソースの自動化ツールです。これにより、リモートサーバーをエージェントやリモートサーバー上の追加ソフトウェアなしで、中央の制御マシンから管理および設定できます。

## Ansibleのプレイブックとは？
Ansibleのプレイブックは、Ansibleが実行するタスクと指示を定義するファイルです。これらのタスクはYAML（Yet Another Markup Language）と呼ばれる人間が読める形式で書かれています。プレイブックは、Ansibleがリモートマシンで行うべきことを指定する、一種の「スクリプト」のようなものです。

### シンプルなプレイブックの例：
ウェブサーバーのグループにApacheウェブサーバーサービスを起動させたいとします。このタスクを定義するためのプレイブックを作成できます。以下は、シンプルなプレイブックの例です：

```yaml
---
- name: Install and Configure DB
  hosts: testServer
  become: yes
  vars:
    oracle_db_port_value: 1521

  tasks:
    - name: Install the Oracle DB
      yum: 
        name: <code to install the DB>
    
    - name: Ensure the installed service is enabled and running
      service:
        name: <your service name>
```
### Ansible プレイブックの理解

Ansible プレイブックをステップバイステップで解説しましょう。

1. **プレイブックヘッダ (---):**
   - 最初の `---` は区切り線のようなもので、YAML ドキュメントの開始を示すものです。Ansible に、ここからYAML ドキュメントが始まることを知らせるためのものです。
2. **`name` (プレイブックの名前):**
   - この行は Ansible プレイブックの名前を指定します。プレイブックにタイトルを付けるようなもので、プレイブックの目的を簡単に理解できるようにします。この場合、データベースのインストールと設定に関するものです。
3. **`hosts` (対象ホスト):**
   - ここでは、タスクを実行するホストまたはホストグループのリストを指定します。ホストは、管理したいコンピュータやサーバーと考えてください。このプレイブックは `testServer` という名前のマシンで実行されます。
4. **`become: yes` (権限昇格):**
   - これは Ansible に、通常 'root' と呼ばれるスーパーユーザーに昇格するように指示するものです。これは、ソフトウェアをインストールしたり、スーパーユーザー権限が必要なサービスを管理したりする場合に必要です。
5. **`vars` (変数):**
   - このセクションでは、`oracle_db_port_value` のような変数を定義できます。変数は、後で使用する値を格納する場所のようなものです。ここでは Oracle データベースのポート番号を `1521` として保存しています。
6. **`tasks` (アクションのリスト):**
   - すべてのプレイブックには実行するタスクのリストを含める必要があります。タスクは実行したいアクションです。このプレイブックには2つのタスクがあります：
     - **タスク 1: Oracle データベースのインストール**: Oracle データベースをインストールするために `yum` モジュールを使用します。`<code to install the DB>` を実際のデータベースのインストールコマンドに置き換える必要があります。
     - **タスク 2: インストール済みのサービスが有効かつ実行中であることを確認**: このタスクは `service` モジュールを使用して、指定したサービスが有効かつ実行中であることを確認します。`<your service name>` を実際に管理したいサービスの名前に置き換えてください。

**要約:**
   - Ansible プレイブックは、サーバーを管理するためのタスクリストのようなものです。
   - プレイブックは名前で始まり、Ansible にどのサーバーで作業するかを指示し、スーパーユーザーの権限が必要かもしれず、変数を使用できるようにし、実行するタスクのリストを含みます。

この例はかなり基本的なものですが、Ansible プレイブックの構造を示しています。プレイブックはさらに複雑でパワフルになることがありますが、これはAnsible での動作を理解する初心者向けのスタートポイントとなるでしょう。


### このプレイブックの動作方法

このプレイブックをAnsibleで実行すると、以下の手順に従います：
1. `testServer` ホストに接続します。
2. インストールコマンドを実行することで「Install the Oracle DB」タスクを実行します。
3. 指定したサービスが実行中であることを確認するために「Ensure the installed service is enabled and running」タスクを実行します。
この例では、プレイブックの構造と、リモートサーバーに対して特定の作業を定義する方法が示されています。プレイブックはより複雑で多様なものになる可能性がありますが、この例はAnsibleでのプレイブックの動作を理解する出発点となるでしょう。

これは基本的な例ですが、条件文、ループ、およびより高度な機能の追加により、プレイブックは複雑になることができます。それにもかかわらず、この例はAnsibleでのプレイブックの動作原理を理解する初心者にとって良い出発点となります。
