# Ansbile Automation Platform Demo Purpose AAP 2.x w/ Amazon AWS

Here you will find some basic tasks to do at Amazon AWS with Ansible
Such as launch ; start ; stop AWS instances

(1) launch-ec2-instance.yml

(2) start-ec2-instance.yml

(3) stop-ec2-instance.yml

Once you have mapped those playbooks under the AAP Control WEBUI the old "tower", you need to add 
the job templates with the surveys variables regarding the following tasks:

- launch-instance - tasks - main.yml
```
    name: "{{ aws_instance_name }}"
    region: "{{ aws_region }}"
    instance_type: "{{ aws_instance_type }}"
    key_name: "{{ aws_keypair }}"
    image_id: "{{ aws_image }}"
    security_group: "{{ aws_security_group }}"
    vpc_subnet_id: "{{ aws_subnet }}"
```
- start-ec2-instance - tasks - main.yml
```
    region: "{{ aws_region }}"
    instance_ids: '{{ instance_ids }}'
    vpc_subnet_id: "{{ aws_subnet }}"
```
- stop-ec2-instance - tasks - main.yml
```
    region: "{{ aws_region }}"
    instance_ids: '{{ instance_ids }}'
    vpc_subnet_id: "{{ aws_subnet }}"
```


Below there is test to execute the launch-ec2-isntance.yml with "ansible-navigator" by CLI.
If you want to run from cli "ansible-navigator" here is a template as example

```
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

$ ansible-navigator run your-playbook-here.yml -m stdout




