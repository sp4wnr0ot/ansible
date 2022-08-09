# Ansible AAP 2.x WEBUI

Basic launch ec2 instance demo by AAP.
- Setup your Amazon Credentials
- Point your Project trough repository
- Sync
- Create a template

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

ansible-navigator run <your-playbook-here>.yml -m stdout