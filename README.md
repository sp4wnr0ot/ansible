# Ansbile Automation Platform Demo Purpose AAP 2.x for Amazon AWS


[![Documentation](https://readthedocs.org/projects/ansible-runner/badge/?version=stable)](https://ansible-runner.readthedocs.io/en/latest/)
[![Code of Conduct](https://img.shields.io/badge/Code%20of%20Conduct-Ansible-silver.svg)](https://docs.ansible.com/ansible/latest/community/code_of_conduct.html)


Here you will find some basic tasks to do at Amazon AWS with Ansible
Such as launch ; start ; stop AWS instances


1). launch-ec2-instance.yml

2). start-ec2-instance.yml

3).  stop-ec2-instance.yml


Once you have mapped those playbooks under the AAP Control WEBUI the old "tower", you need to add 
the 'job templates', also the 'surveys' variables regarding the variables:

- launch-instance - tasks - main.yml
```bash
    name: "{{ aws_instance_name }}"
    region: "{{ aws_region }}"
    instance_type: "{{ aws_instance_type }}"
    key_name: "{{ aws_keypair }}"
    image_id: "{{ aws_image }}"
    security_group: "{{ aws_security_group }}"
    vpc_subnet_id: "{{ aws_subnet }}"
```
- start-ec2-instance - tasks - main.yml
```bash
    region: "{{ aws_region }}"
    instance_ids: '{{ instance_ids }}'
    vpc_subnet_id: "{{ aws_subnet }}"
```
- stop-ec2-instance - tasks - main.yml
```bash
    region: "{{ aws_region }}"
    instance_ids: '{{ instance_ids }}'
    vpc_subnet_id: "{{ aws_subnet }}"
```

Below there is a test to execute the launch-ec2-isntance.yml with "ansible-navigator" by CLI.
If you want to run from cli by "ansible-navigator" here is a template as an example.
Don't forget to set up your aws key's.

```bash
- hosts: localhost
  #  connection: local
  gather_facts: False

  tasks:
    - name: Launch instance
      amazon.aws.ec2_instance:
        name: "Demo-1"
        region: "us-west-1"
        aws_access_key: "<your-access-key>"
        aws_secret_key: "<your-secret-key>"
        instance_type: t2.small
        key_name: "<your-master-ssh-key>"
        image_id: "<any-ami>"
        security_group: "<your-sg>"
        vpc_subnet_id: "<your-vpc-subnet-id>"
        network:
          assign_public_ip: no
        tags:
          Environment: Testing
          DeleteBy: Never
      register: result  
```


```bash
$ ansible-navigator run your-playbook-here.yml -m stdout
