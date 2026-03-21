# Resource: aws_secretsmanager_tag

Manages an individual AWS Secrets Manager secret tag. This resource should only be used in cases where AWS Secrets Manager secrets are created outside ytofu (e.g., [AWS Secrets Manager secrets managed by other AWS services](https://docs.aws.amazon.com/secretsmanager/latest/userguide/service-linked-secrets.html), such as RDS).

## Basic Example

```yaml
resource:
  aws_secretsmanager_secret:
    test:
      name: example-secret
      lifecycle:
        ignore_changes: 
          - tags

resource:
  aws_secretsmanager_tag:
    test:
      secret_id: ${aws_secretsmanager_secret.test.id}
      key: ExampleKey
      value: ExampleValue
```

## Argument Reference

This resource supports the following arguments:

* `secret_id` - (Required) ID of the AWS Secrets Manager secret to tag.
* `key` - (Required) Tag name.
* `value` - (Required) Tag value.
* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - AWS Secrets Manager secret identifier and key, separated by a comma (`,`)

## Import

```bash
ytofu import aws_secretsmanager_tag.example arn:aws:secretsmanager:us-east-1:123456789012:example-secret,ExampleKey
```
