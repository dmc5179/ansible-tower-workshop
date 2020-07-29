# ansible-tower-workshop
Ansible Tower Workshop with multiple teams and roles

*** These playbook cannot be run until the tower server has been entitled with a subscription ***

This workshop creates the following:

- 2 users (helpdesk1 and engineer1)
- 2 teams (Scaning, Remediation)
- 1 project (containing the security scanning playbook)
- 2 templates (1 for the scanning team and 1 for the remediation team)

The template for the scanning team is set to check mode. The scanning team only has the power to check compliance. The Remediation team has the power to fix/remediate issues
