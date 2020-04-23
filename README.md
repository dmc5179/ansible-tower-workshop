# ansible-tower-workshop
Ansible Tower Workshop with multiple teams and roles

This workshop creates the following:

- 2 users (john, paul)
- 2 teams (Scaning, Remediation)
- 1 project (containing the security scanning playbook)
- 2 templates (1 for the scanning team and 1 for the remediation team)

The template for the scanning team is set to check mode. The scanning team only has the power to check compliance. The Remediation team has the power to fix/remediate issues
