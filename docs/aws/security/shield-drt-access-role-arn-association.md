# Resource: aws_shield_drt_access_role_arn_association

Authorizes the Shield Response Team (SRT) using the specified role, to access your AWS account to assist with DDoS attack mitigation during potential attacks.
For more information see [Configure AWS SRT Support](https://docs.aws.amazon.com/waf/latest/developerguide/authorize-srt.html)

## Basic Example

```yaml
resource:
  aws_shield_drt_access_role_arn_association:
    example:
      role_arn: ${aws_iam_role.example.arn}

  aws_iam_role:
    example:
      name: example-role
      assume_role_policy: '{ "Version": "2012-10-17" "Statement": [ { "Sid" : "", "Effect" : "Allow", "Principal" : { "Service" : "drt.shield.amazonaws.com" }, "Action" : "sts:AssumeRole" }, ] }'

  aws_iam_role_policy_attachment:
    example:
      role: ${aws_iam_role.example.name}
      policy_arn: "arn:aws:iam::aws:policy/service-role/AWSShieldDRTAccessPolicy"```

## Argument Reference

The following arguments are required:

* `role_arn` - (Required) The Amazon Resource Name (ARN) of the role the SRT will use to access your AWS account. Prior to making the AssociateDRTRole request, you must attach the `AWSShieldDRTAccessPolicy` managed policy to this role.

## Attribute Reference

This resource exports no additional attributes.

## Timeouts

Configuration options:

* `create` - (Default `30m`)
* `update` - (Default `30m`)
* `delete` - (Default `30m`)

## Import

```bash
ytofu import aws_shield_drt_access_role_arn_association.example 123456789012
```
