# Resource: aws_dms_replication_subnet_group

Provides a DMS (Data Migration Service) replication subnet group resource. DMS replication subnet groups can be created, updated, deleted, and imported.

## Basic Example

```yaml
resource:
  aws_dms_replication_subnet_group:
    example:
      replication_subnet_group_description: Example replication subnet group
      replication_subnet_group_id: example-dms-replication-subnet-group-tf
      subnet_ids:
        - subnet-12345678
        - subnet-12345679
      tags:
        Name: example
```

## Creating special IAM role

```yaml
resource:
  aws_iam_role:
    dms-vpc-role:
      name: dms-vpc-role
      description: Allows DMS to manage VPC
      assume_role_policy: '{ "Version": "2012-10-17" "Statement": [ { "Effect": "Allow" "Principal": { "Service": "dms.amazonaws.com" } "Action": "sts:AssumeRole" }, ] }'

resource:
  aws_iam_role_policy_attachment:
    example:
      role: ${aws_iam_role.dms-vpc-role.name}
      policy_arn: "arn:aws:iam::aws:policy/service-role/AmazonDMSVPCManagementRole"

resource:
  aws_dms_replication_subnet_group:
    example:
      replication_subnet_group_description: Example
      replication_subnet_group_id: example-id
      subnet_ids:
        - subnet-12345678
        - subnet-12345679
      tags:
        Name: example-id
      depends_on: 
        - ${aws_iam_role_policy_attachment.example}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `replication_subnet_group_description` - (Required) Description for the subnet group.
* `replication_subnet_group_id` - (Required) Name for the replication subnet group. This value is stored as a lowercase string. It must contain no more than 255 alphanumeric characters, periods, spaces, underscores, or hyphens and cannot be `default`.
* `subnet_ids` - (Required) List of at least 2 EC2 subnet IDs for the subnet group. The subnets must cover at least 2 availability zones.
* `tags` - (Optional) Map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.
* `vpc_id` - The ID of the VPC the subnet group is in.

## Timeouts

Configuration options:

- `create` - (Default `15m`)
- `update` - (Default `15m`)
- `delete` - (Default `15m`)

## Import

```bash
ytofu import aws_dms_replication_subnet_group.test test-dms-replication-subnet-group-tf
```
