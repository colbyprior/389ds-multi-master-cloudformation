# 389ds Multi Master Cloudformation
This repository is for deploying a multi master 389ds ldap setup with two Ec2 instances behind a network load balancer.

![Architecture](https://raw.githubusercontent.com/colbyprior/389ds-multi-master-cloudformation/master/docs/ldap.png)

## Deploying
- First create an S3 bucket to hold the config files.
- Then populate a variable file based off `example-vars.yml`.
- Run ansible.

`ansible-playbook ansible-deploy.yml --extra-vars "var_file=dev.yml"`

## Target Group Health Checks
After deploying the cloudformation stack the network load balancer will blindly route traffic to both servers. In order to enable health checks for the network load balancer you must add the IP addresses for it to your security group. You can get a list of network interfaces IP addresses via the CLI and filter by those with the name LDAP.

`aws ec2 describe-network-interfaces | jq '[.NetworkInterfaces | .[] | {IP: .PrivateIpAddress, Name: .Description} ]' | grep ldap -B1`

Put these addresses in to the network load balancer addresses cloudformation parameter and re-deploy the stack.
