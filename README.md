# Ansible Collection - aws_ec2

This collection creates key-pair, security group and EC2 instance over AWS.

Prerequisite:
-------------

To use this collection, it requires `boto` and `boto3` python library. Make sure you install it first.

```sh
$ pip3 install --upgrade pip #to update pip in your system

$ pip install boto boto3
```

After that, You also need to provide AWS credential so that Ansible fetch the account details. For this, create one IAM account in AWS.
For providing AWS credential, set the **environment variables** for your Secret and Access key:

```sh
$ export AWS_ACCESS_KEY_ID='YOUR_AWS_API_KEY'

$ export AWS_SECRET_ACCESS_KEY='YOUR_AWS_API_SECRET_KEY'
```

Example
-------

### Install the role:

```bash
$ ansible-galaxy collection install gaurav-gupta-gtm.awc_ec2
```

### playbook.yml example

```yaml
- hosts: localhost
  roles:
          - { role: ec2_host , key_dest: "/root/.ssh/key.pem" , region: "ap-south-1" , image_id: "ami-0ebc1ac48dfd14136" , count: "3" , tag_name: "from-ansible" , port: "80" }
```

> **You can override the default variable in roles using above way.**

Ansible Plugins:
----------------

To setup dynamic Inventory `hosts/main_aws_ec2.yml` over AWS, it uses plugin `amazon.aws.aws_ec2`. This dynamically fetch Instance Over AWS and provide tag to them which we set.

```yaml
plugin: amazon.aws.aws_ec2
regions:
  - ap-south-1
keyed_groups:
  # add hosts to tag_Name_value groups for each aws_ec2 host's tags.Name variable
  - key: tags.Name
    prefix: tag_Name_
    separator: ""
hostnames:
  - ip-address
```

Galaxy Link: https://galaxy.ansible.com/gaurav_gupta_gtm/aws_ec2
