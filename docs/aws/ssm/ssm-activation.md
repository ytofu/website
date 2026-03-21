# Resource: aws_ssm_activation

Registers an on-premises server or virtual machine with Amazon EC2 so that it can be managed using Run Command.

## Basic Example

```yaml
data:
  aws_iam_policy_document:
    assume_role:
      statement:
        effect: Allow
        principals:
          type: Service
          identifiers: 
            - ssm.amazonaws.com
        actions: 
          - "sts:AssumeRole"

resource:
  aws_iam_role:
    test_role:
      name: test_role
      assume_role_policy: ${data.aws_iam_policy_document.assume_role.json}

resource:
  aws_iam_role_policy_attachment:
    test_attach:
      role: ${aws_iam_role.test_role.name}
      policy_arn: "arn:aws:iam::aws:policy/AmazonSSMManagedInstanceCore"

resource:
  aws_ssm_activation:
    foo:
      name: test_ssm_activation
      description: Test
      iam_role: ${aws_iam_role.test_role.id}
      registration_limit: 5
      depends_on: 
        - ${aws_iam_role_policy_attachment.test_attach}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Optional) The default name of the registered managed instance.
* `description` - (Optional) The description of the resource that you want to register.
* `expiration_date` - (Optional) UTC timestamp in [RFC3339 format](https://tools.ietf.org/html/rfc3339#section-5.8) by which this activation request should expire. The default value is 24 hours from resource creation time. ytofu will only perform drift detection of its value when present in a configuration.
* `iam_role` - (Required) The IAM Role to attach to the managed instance.
* `registration_limit` - (Optional) The maximum number of managed instances you want to register. The default value is 1 instance.
* `tags` - (Optional) A map of tags to assign to the object. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The activation ID.
* `activation_code` - The code the system generates when it processes the activation.
* `name` - The default name of the registered managed instance.
* `description` - The description of the resource that was registered.
* `expired` - If the current activation has expired.
* `expiration_date` - The date by which this activation request should expire. The default value is 24 hours.
* `iam_role` - The IAM Role attached to the managed instance.
* `registration_limit` - The maximum number of managed instances you want to be registered. The default value is 1 instance.
* `registration_count` - The number of managed instances that are currently registered using this activation.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_ssm_activation.example e488f2f6-e686-4afb-8a04-ef6dfEXAMPLE
```
