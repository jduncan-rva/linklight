# Linklight OCP

## Overview

Linklight-ocp is based on the [Ansible Linklight Workshop Provisioner](https://github.com/network-automation/linklight). Linklight is an efficient AWS-based workshop tool created by several members of the Red Hat Ansible team and other contributors. Essentially, we've forked Linklight to deploy OpenShift workshops instead of Ansible and Ansible Networking workshops.

## Lab Design

Each student is provisioned the following using linklight-ocp:
* bastion host for deploying OpenShift and exploring Ansible
* 3-node OpenShift cluster
* Containerized lab guide deployed on the bastion host on port 8080.

## Deploying the lab

Deploying linklight-ocp requires:

* AWS account with:
  * quotas to accommodate `$(STUDENT_COUNT) * 4` instances.
  * route53 controlled DNS zone on the account you'll be using
  * S3 access for the dynamic web page for student information
* Basic git knowledge

### AWS credentials

Ansible EC2 modules are designed to read your AWS credentials from multiple locations. I find storing a credentials file in my home directory to be easy and effective.

```
$ cat ~/.aws/credentials
[default]
aws_access_key_id = XXXXXXXXXXXXXXXX
aws_secret_access_key = YYYYYYYYYYYYYYYYYYYYYYYY
```

### extra_vars.yml

Configuring your workshop deployment will be covered as variables in a file called `extra_vars.yml`. There's an example file at `provisioner/extra_vars.yml.sample`. The variables you need to set are:  

```
ec2_region: us-east-1
ec2_az: us-east-1a
ec2_name_prefix: WORKSHOP_NAME
admin_password: ADMIN_PASSWORD
student_total: 1
workshop_dns_zone: YOUR_ROUTE53_ZONE
rhsm_username: YOUR_USERNAME
rhsm_password: YOUR_PASSWORD
rhsm_pool: YOUR_RHSM_POOL
```

* ec2_region: the region to deploy your workshop in
* ec2_az: the availability zone to deploy your workshop in
* ec2_name_prefix: a common name for your workshop, typically associated with the customer or location for the workshop
* admin_password: password for the student users, as well as the OpenShift users for the workshop
* student_total: number of students to create for the workshop
* workshop_dns_zone: the Route53 hosted zone to use for the student DNS names and the dynamic page to point the students to their information
* rhsm_username: an RHSM username to use to register the hosts
* rhsm_password: an RHSM password to use to register the hosts
* rhsm_pool: the RHSM pool to attach the hosts to to get their needed OCP repositories

### running the deploy playbook

To deploy a workshop, run the following command:

```
ansible-playbook -e @./provisioner/extra_vars.yml ./provisioner/provision_lab.yml
```

## Lab artifacts

* Each student gets their bastion host and 3 node OCP cluster
* A dynamic web page is created at `http://<ec2_name_prefix>.<workshop_dns_zone>`. This page contains all of the needed information and links for each user in the lab. 
* A customized lab guide deployed on their bastion host on port 8080. This is linked to in the dynamic web page.

## Lab cleanup

Once your workshop is complete, be sure to run the playbook to clean up the lab:

```
ansible-playbook -e @./provisioner/extra_vars.yml ./provisioner/teardown_lab.yml
```

This will delete all of the volumes, vpcs, security groups, as well as the instances. It's much cleaner than just blowing away the instances manually.
