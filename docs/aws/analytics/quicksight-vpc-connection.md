# Quicksight VPC Connection

Manage Quicksight VPC Connection resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_iam_role:
    vpc_connection_role:
      assume_role_policy: '{ "Version": "2012-10-17" "Statement": [ { "Effect": "Allow" "Action": "sts:AssumeRole" "Principal": { "Service": "quicksight.amazonaws.com" } } ] }'
      inline_policy:
        name: QuickSightVPCConnectionRolePolicy
        policy: '{ "Version": "2012-10-17" "Statement": [ { "Effect": "Allow" "Action": [ "ec2:CreateNetworkInterface", "ec2:ModifyNetworkInterfaceAttribute", "ec2:DeleteNetworkInterface", "ec2:DescribeSubnets", "ec2:DescribeSecurityGroups" ] "Resource": ["*"] } ] }'

resource:
  aws_quicksight_vpc_connection:
    example:
      vpc_connection_id: example-connection-id
      name: Example Connection
      role_arn: ${aws_iam_role.vpc_connection_role.arn}
      security_group_ids: 
        - sg-00000000000000000
      subnet_ids:
        - subnet-00000000000000000
        - subnet-00000000000000001
```
