# Resource: aws_cloudwatch_log_index_policy

ytofu resource for managing an AWS CloudWatch Logs Index Policy.

## Basic Example

```yaml
resource:
  aws_cloudwatch_log_group:
    example:
      name: example

resource:
  aws_cloudwatch_log_index_policy:
    example:
      log_group_name: ${aws_cloudwatch_log_group.example.name}
      policy_document: '{ "Fields": ["eventName"] }'
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `log_group_name` - (Required) Log group name to set the policy for.
* `policy_document` - (Required) JSON policy document. This is a JSON formatted string.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_cloudwatch_log_index_policy.example /aws/log/group/name
```
