# Resource: aws_ssm_association

Associates an SSM Document to an instance or EC2 tag.

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
        systemctl start amazon-ssm-agent```

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
        Owner: team```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) The name of the SSM document to apply.
* `apply_only_at_cron_interval` - (Optional) By default, when you create a new or update associations, the system runs it immediately and then according to the schedule you specified. Enable this option if you do not want an association to run immediately after you create or update it. This parameter is not supported for rate expressions. Default: `false`.
* `association_name` - (Optional) The descriptive name for the association.
* `automation_target_parameter_name` - (Optional) Specify the target for the association. This target is required for associations that use an `Automation` document and target resources by using rate controls. This should be set to the SSM document `parameter` that will define how your automation will branch out.
* `calendar_names` - (Optional) One or more Systems Manager Change Calendar names. The association runs only when the Change Calendar is open.
* `compliance_severity` - (Optional) The compliance severity for the association. Can be one of the following: `UNSPECIFIED`, `LOW`, `MEDIUM`, `HIGH` or `CRITICAL`
* `document_version` - (Optional) The document version you want to associate with the target(s). Can be a specific version or the default version.
* `max_concurrency` - (Optional) The maximum number of targets allowed to run the association at the same time. You can specify a number, for example 10, or a percentage of the target set, for example 10%.
* `max_errors` - (Optional) The number of errors that are allowed before the system stops sending requests to run the association on additional targets. You can specify a number, for example 10, or a percentage of the target set, for example 10%. If you specify a threshold of 3, the stop command is sent when the fourth error is returned. If you specify a threshold of 10% for 50 associations, the stop command is sent when the sixth error is returned.
* `output_location` - (Optional) An output location block. Output Location is documented below.
* `parameters` - (Optional) A block of arbitrary string parameters to pass to the SSM document.
* `schedule_expression` - (Optional) A [cron or rate expression](https://docs.aws.amazon.com/systems-manager/latest/userguide/reference-cron-and-rate-expressions.html) that specifies when the association runs.
* `sync_compliance` - (Optional) The mode for generating association compliance. You can specify `AUTO` or `MANUAL`.
* `tags` - (Optional) A map of tags to assign to the object. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.
* `targets` - (Optional) A block containing the targets of the SSM association. Targets are documented below. AWS currently supports a maximum of 5 targets.
* `wait_for_success_timeout_seconds` - (Optional) The number of seconds to wait for the association status to be `Success`. If `Success` status is not reached within the given time, create opration will fail.

Output Location (`output_location`) is an S3 bucket where you want to store the results of this association:

* `s3_bucket_name` - (Required) The S3 bucket name.
* `s3_key_prefix` - (Optional) The S3 bucket prefix. Results stored in the root if not configured.
* `s3_region` - (Optional) The S3 bucket region.

Targets specify what instance IDs or tags to apply the document to and has these keys:

* `key` - (Required) User-defined criteria for sending commands that target managed nodes that meet the criteria. See the [AWS documentation](https://docs.aws.amazon.com/systems-manager/latest/APIReference/API_Target.html) for the list of available keys.
* `values` - (Required) List of values that correspond to the specified `key`. See the [AWS documentation](https://docs.aws.amazon.com/systems-manager/latest/APIReference/API_Target.html) for details.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - The ARN of the SSM association
* `association_id` - The ID of the SSM association.
* `name` - The name of the SSM document to apply.
* `parameters` - Additional parameters passed to the SSM document.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_ssm_association.example 10abcdef-0abc-1234-5678-90abcdef123456
```
