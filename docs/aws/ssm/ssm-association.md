# SSM Association

Manage SSM Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ssm_association:
    example:
      name: ${aws_ssm_document.example.name}
      targets:
        key: InstanceIds
        values: 
          - ${aws_instance.example.id}
```

## Create an association for all managed instances in an AWS account

```yaml
resource:
  aws_ssm_association:
    example:
      name: AmazonCloudWatch-ManageAgent
      targets:
        key: InstanceIds
        values: 
          - "*"
```

## Create an association for a specific tag

```yaml
resource:
  aws_ssm_association:
    example:
      name: AmazonCloudWatch-ManageAgent
      targets:
        key: "tag:Environment"
        values: 
          - Development
```

## Create an association with a specific schedule

```yaml
resource:
  aws_ssm_association:
    example:
      name: ${aws_ssm_document.example.name}
      schedule_expression: "cron(0 2 ? * SUN *)"
      targets:
        key: InstanceIds
        values: 
          - ${aws_instance.example.id}
```

## Create an association with multiple instances with their instance ids

```yaml
resource:
  aws_ssm_association:
    system_update:
      name: AWS-RunShellScript
      targets:
        key: InstanceIds
        values:
          - ${aws_instance.web_server_1.id}
          - ${aws_instance.web_server_2.id}
      schedule_expression: "cron(0 2 ? * SUN *)"
      parameters:
        commands: "yum update -y"
        workingDirectory: /tmp
        executionTimeout: 3600
      association_name: weekly-system-update
      compliance_severity: MEDIUM
      max_concurrency: "1" # Run on one instance at a time
      max_errors: "0" # Stop if any instance fails
      tags:
        Name: Weekly System Update
        Environment: demo
        Purpose: maintenance

resource:
  aws_instance:
    web_server_1:
      ami: ${data.aws_ami.amazon_linux.id}
      instance_type: t3.micro
      subnet_id: ${aws_subnet.public.id}
      vpc_security_group_ids: 
        - ${aws_security_group.ec2_sg.id}
      iam_instance_profile: ${aws_iam_instance_profile.ec2_ssm_profile.name}
      user_data: |
        #!/bin/bash
        yum update -y
        yum install -y amazon-ssm-agent
        systemctl enable amazon-ssm-agent
        systemctl start amazon-ssm-agent

resource:
  aws_instance:
    web_server_2:
      ami: ${data.aws_ami.amazon_linux.id}
      instance_type: t3.micro
      subnet_id: ${aws_subnet.public.id}
      vpc_security_group_ids: 
        - ${aws_security_group.ec2_sg.id}
      iam_instance_profile: ${aws_iam_instance_profile.ec2_ssm_profile.name}
      user_data: |
        #!/bin/bash
        yum update -y
        yum install -y amazon-ssm-agent
        systemctl enable amazon-ssm-agent
        systemctl start amazon-ssm-agent
```

## Create an association with multiple instances with their values matching their tags

```yaml
resource:
  aws_ssm_association:
    database_association:
      name: ${aws_ssm_document.system_update.name}
      targets:
        key: "tag:Role"
        values: 
          - WebServer
          - Database
      parameters:
        restartServices: true
      schedule_expression: "cron(0 3 ? * SUN *)" # Run every Sunday at 3 AM

resource:
  aws_instance:
    web_server:
      ami: ${data.aws_ami.amazon_linux.id}
      instance_type: t3.micro
      subnet_id: ${data.aws_subnet.default.id}
      vpc_security_group_ids: 
        - ${aws_security_group.ec2_sg.id}
      iam_instance_profile: ${aws_iam_instance_profile.ec2_ssm_profile.name}
      user_data: |
        #!/bin/bash
        yum update -y
        yum install -y amazon-ssm-agent
        systemctl enable amazon-ssm-agent
        systemctl start amazon-ssm-agent
        yum install -y httpd
        systemctl enable httpd
        systemctl start httpd
      tags:
        Name: "example-web-server"
        ServerType: WebServer
        Role: WebServer
        Environment: production
        Owner: team

resource:
  aws_instance:
    database_server:
      ami: ${data.aws_ami.amazon_linux.id}
      instance_type: t3.micro
      subnet_id: ${data.aws_subnet.default.id}
      vpc_security_group_ids: 
        - ${aws_security_group.ec2_sg.id}
      iam_instance_profile: ${aws_iam_instance_profile.ec2_ssm_profile.name}
      user_data: |
        #!/bin/bash
        yum update -y
        yum install -y amazon-ssm-agent
        systemctl enable amazon-ssm-agent
        systemctl start amazon-ssm-agent
        yum install -y mysql-server
        systemctl enable mysqld
        systemctl start mysqld
      tags:
        Name: "example-database-server"
        Role: Database
        Environment: production
        Owner: team
```
