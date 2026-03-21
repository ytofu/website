# Resource: aws_iot_policy

Provides an IoT policy.

## Basic Example

```yaml
resource:
  aws_iot_policy:
    pubsub:
      name: PubSubToAnyTopic
      policy: '{ "Version": "2012-10-17" "Statement": [ { "Action": [ "iot:*", ] "Effect": "Allow" "Resource": "*" }, ] }'
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) The name of the policy.
* `policy` - (Required) The policy document. This is a JSON formatted string. Use the [IoT Developer Guide](http://docs.aws.amazon.com/iot/latest/developerguide/iot-policies.html) for more information on IoT Policies. For more information about building AWS IAM policy documents with ytofu, see the [AWS IAM Policy Document Guide](https://learn.hashicorp.com/terraform/aws/iam-policy).
* `tags` - (Optional) Key-value mapping of resource tags. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - The ARN assigned by AWS to this policy.
* `name` - The name of this policy.
* `default_version_id` - The default version of this policy.
* `policy` - The policy document.
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Timeouts

Configuration options:

* `update` - (Default `1m`)
* `delete` - (Default `5m`)

## Import

```bash
ytofu import aws_iot_policy.pubsub PubSubToAnyTopic
```
