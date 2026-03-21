# Resource: aws_kms_key_policy

Attaches a policy to a KMS Key.

## Basic Example

```yaml
resource:
  aws_kms_key:
    example:
      description: example

resource:
  aws_kms_key_policy:
    example:
      key_id: ${aws_kms_key.example.id}
      policy: '{ "Id": "example" "Statement": [ { "Action": "kms:*" "Effect": "Allow" "Principal": { "AWS": "*" } "Resource": "*" "Sid": "Enable IAM User Permissions" }, ] "Version": "2012-10-17" }'
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `key_id` - (Required) The ID of the KMS Key to attach the policy.
* `policy` - (Required) A valid policy JSON document. Although this is a key policy, not an IAM policy, an `aws_iam_policy_document`, in the form that designates a principal, can be used. For more information about building policy documents with ytofu, see the [AWS IAM Policy Document Guide](https://learn.hashicorp.com/terraform/aws/iam-policy).

* `bypass_policy_lockout_safety_check` - (Optional) A flag to indicate whether to bypass the key policy lockout safety check.
Setting this value to true increases the risk that the KMS key becomes unmanageable. Do not set this value to true indiscriminately. If this value is set, and the resource is destroyed, a warning will be shown, and the resource will be removed from state.
For more information, refer to the scenario in the [Default Key Policy](https://docs.aws.amazon.com/kms/latest/developerguide/key-policies.html#key-policy-default-allow-root-enable-iam) section in the _AWS Key Management Service Developer Guide_.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_kms_key_policy.a 1234abcd-12ab-34cd-56ef-1234567890ab
```
