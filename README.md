# Linklight OCP

## Overview

Linklight-ocp is based on the [Ansible Linklight Workshop Provisioner](https://github.com/network-automation/linklight). Linklight is an incredibly efficient AWS-based workshop tool created by several members of the Red Hat Ansible team and other contributors. Essentially, we've hacked it up to deploy OpenShift workshops instead of Ansible and Ansible Networking workshops.

## Lab Design

## Deploying the lab

Deploying linklight-ocp requires the following:

* AWS account with:
  * quotas to accomodate `$(STUDENT_COUNT) * 6` instances.
  * route53 controlled DNS zone
  * S3 access 
* Basic git knowledge

### AWS Account

### extra_vars.yml

### running the deploy playbook

## Lab cleanup

### Tearing down the lab
