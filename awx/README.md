## The AWX Project

#### What is The AWX?
AWX provides a web-based user interface, REST API, and task engine built on top of Ansible. It is one of the upstream projects for Red Hat Ansible Automation Platform.
AWX is an open source project maintained by the community and Red Hat. It offers a graphical interface for managing ansibles projects.

#### Architecture AWX
[awx-infra](https://github.com/EzzioMoreira/challenge_devops/blob/main/awx/img/awx-infra.JPG)
- awx_task: runs AWX scheduled tasks.
- awx_web: provides a web interface and does all the intermediation between awx_task and the user.
- awx_memcached: responsible for storing awx_tasks and awx_web values.
- awx_rabbitmq: message exchange between awx_web and awx_tasks, allowing disconnection between these two services.
- awx_postgres: database used by AWX to store all information via the web interface.

#### Host Inventory
[inventory](https://github.com/EzzioMoreira/challenge_devops/blob/main/awx/img/inventory.JPG)
Ansible is designed to work with multiple environments (Dev, QA, UAT, Prod, etc.) at the same time. It uses an inventory file that contains a group of hosts and their variables.
File default the Ansible is saved in /etc/ansible/hosts.

#### Playbook
[playbook](https://github.com/EzzioMoreira/challenge_devops/blob/main/awx/img/playbook.JPG)
A playbook is a file where the user describes the tasks that will be performed on a host or group of hosts. Basically the ‘tasks’ calls the Ansible modules to get the desired configuration.

#### Best practices:
- Access to AWX web interface can be separated by teams (Dev, QA, UAT, Prod)..
- Define a host group in INVENTORIES for each stage (Dev, QA, UAT, Prod).
- Playbooks, papers must be stored in git repositories. RPs must be reviewed and approved by team members.
- Define permissions on PROJECTS for teams at each stage.
- Create CREDENTIALS and set permissions for teams.
- After authorization from the PR of the Ansible project repository, define the users who can run the MODELS.
- After executing a JOB in MODELS, it is recommended to trigger a NOTIFICATION to the responsible team and/or other teams.

#### References
[Tower docs site](http://docs.ansible.com/ansible-tower/index.html)
[Guidelines](https://github.com/ansible/awx-logos/blob/master/TRADEMARKS.md)
[Question AWX](https://www.ansible.com/awx-project-faq)
[What is Ansible](http://ansible-br.org/por-que-ansible/)
