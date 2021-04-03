# ansible-tower-workshop
Ansible Tower Workshop with multiple teams and roles

*** These playbook cannot be run until the tower server has been entitled with a subscription ***

This workshop creates the following:

- 2 users (helpdesk1 and engineer1)
- 2 teams (Scaning, Remediation)
- 1 project (containing the security scanning playbook)
- 2 templates (1 for the scanning team and 1 for the remediation team)


The template for the scanning team is set to check mode.

The scanning team only has the power to check compliance.

The Remediation team has the power to fix/remediate issues

## Setup

Below are the steps for using this project to make calls against your own Ansible Tower system

- Copy the example Ansible variable file

```
cp group_vars/all/all.yaml.example group_vars/all/all.yaml
```

- Edit your copy for the all.yaml file


| Variable                    | Default                   | Comments                        |
| :---	                      | :--                       | :--                             |
| demo_name                   | 'tower'                   |                                 |
| aws_dynamic_inventory       | true                      |                                 |
| satellite_dynamic_inventory | false                     |                                 |
| tower.use_token             | false                     |                                 |
| tower.description_on        | false                     |                                 |
| tower.password              | 'redhat2020'              |                                 |
| tower.verify_ssl            | false                     |                                 |
| tower.format                | 'human'                   |                                 |
| tower.insecure              | true                      |                                 |
| tower.oauth_token           |                           |                                 |
| tower.verbose               | false                     |                                 |
| tower.color                 | true                      |                                 |
| tower.username              | 'admin'                   |                                 |
| tower.host                  | 'tower.example.redhatgov.io' |                                 |
| tower.organization          | 'Default'                 |                                 |
| tower.certificate           |                           |                                 |




- To provision all of the pieces of the project simply run the tower.yaml playbook

```
ansible-playbook tower.yaml
```

- To run only portions of the tower playbook simply run the tower.yaml playbook with the desired tags; i.e

```
ansible-playbook --tags 'credentials' tower.yaml
```

or

```
ansible-playbook --tags 'credentials,teams' tower.yaml
```


## Cleanup

- The cleanup.yaml playbook is not yet supported. All tasks in that playbook have been commented out.


## Splunk search strings:

```
source="http:tower" (index="history")| spath stdout | search stdout="*new_incident.record*"
```
