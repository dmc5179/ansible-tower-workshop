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

- Copy the sample tower_cli.cfg file

```
cp files/tower_cli.cfg.example files/tower_cli.cfg
```

- Edit your copy for the tower_cli.cfg file

Below is a description of each of the fileds in the tower_cli.cfg file. Additional documentation can be found here:
https://tower-cli.readthedocs.io/en/latest/api_ref/conf.html

| Variable       | Default               | Comments                                                                                                          |
| :---	         | :--                   | :--                                                                                                               |
| color          | Boolean/’true’        | Whether to use colored output for highlighting or not.                                                            |
| format         | String with options (‘human’, ‘json’, ‘yaml’)/’human’ | Output format.                                                                    |
| host           | String/‘127.0.0.1’    | The location of the Ansible Tower host. HTTPS is assumed as the protocol unless “http://” is explicitly provided. |
| password       | String/’‘             | Password to use to authenticate to Ansible Tower.                                                                 |
| username       | String/’‘             | Username to use to authenticate to Ansible Tower.                                                                 |
| verify_ssl     | Boolean/’true’        | Whether to force verified SSL connections.                                                                        |
| verbose        | Boolean/’false’       | Whether to show information about requests being made.                                                            |
| description_on | Boolean/’false’       | Whether to show description in human-formatted output. [CLI use only]                                             |
| certificate    | String/’‘             | Path to a custom certificate file that will be used throughout the command.                                       |
| use_token      | Boolean/’false’       | Whether to use token-based authentication. No longer supported in Tower 3.3 and above                             |

- To provision all of the pieces of the project simply run the main.yaml playbook

```
ansible-playbook main.yaml
```

- To run only portions of the main playbook simply run the main.yaml playbook with the desired tags; i.e

```
ansible-playbook --tags 'credentials' main.yaml
```

or

```
ansible-playbook --tags 'credentials,teams' main.yaml
```


## Cleanup

- The cleanup.yaml playbook is not yet supported. All tasks in that playbook have been commented out.


## Splunk search strings:

```
source="http:tower" (index="history")| spath stdout | search stdout="*new_incident.record*"
```
