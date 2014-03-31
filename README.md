role_deploy_war
===================

An Ansible role to deploy a WAR file from S3 to Tomcat7

The play needs to look something like this:

```
- name: deploy new war file
  hosts: tag_Name_<tagname>
  user: ubuntu
  gather_facts: False
  vars:
    - war: <filename>
    - bucket: <bucket>
    - aws_access_key: "{{ lookup('env','AWS_ACCESS_KEY') }}"
    - aws_secret_key: "{{ lookup('env','AWS_SECRET_KEY') }}"
  roles:
    - deploy_war
```

Where:
- **tagname** is the name of the EC2 instance(s) that this needs to run on
- **filename** is the file name of the war file to deploy, minus the '.war'
- **bucket** is the name of the AWS S3 bucket that the file lives in

The AWS keys are used to connect from the EC2 instance to S3, and are pulled from the ansible user's local environment.
