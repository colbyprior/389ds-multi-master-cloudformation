# 389ds Multi Master Cloudformation
This repository is for deploying a multi master 389ds ldap setup with two Ec2 instances behind a network load balancer.

## Deploying
- First create an S3 bucket to hold the config files.
- Then populate a variable file based off `example-vars.yml`.
- Run ansible.

`ansible-playbook ansible-deploy.yml --extra-vars "var_file=dev.yml"`
