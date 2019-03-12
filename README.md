# Linklight OCP

## Overview

Linklight-ocp is based on the [Ansible Linklight Workshop Provisioner](https://github.com/network-automation/linklight). Linklight is an incredibly efficient AWS-based workshop tool created by several members of the Red Hat Ansible team and other contributors. Essentially, we've hacked it up to deploy OpenShift workshops instead of Ansible and Ansible Networking workshops.

## Lab Design

Each student is provisioned the following using linklight-ocp:
* bastion host for deploying OpenShift
* 4-node OpenShift cluster
* External database node (primarily for the Dev track of the [])

## Deploying the lab

Deploying linklight-ocp requires:

* AWS account with:
  * quotas to accommodate `$(STUDENT_COUNT) * 6` instances.
  * route53 controlled DNS zone
  * S3 access
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

### running the deploy playbook

## Lab cleanup

### Tearing down the lab
