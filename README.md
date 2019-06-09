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

Any customization you'll need to add for the workshop will be covered as variables in a file called `extra_vars.yml`.

```
extra_vars content goes here
```

### running the deploy playbook

## Lab cleanup

### Tearing down the lab
