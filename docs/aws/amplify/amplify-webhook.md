# Resource: aws_amplify_webhook

Provides an Amplify Webhook resource.

## Basic Example

```yaml
resource:
  aws_amplify_app:
    example:
      name: app

  aws_amplify_branch:
    master:
      app_id: ${aws_amplify_app.example.id}
      branch_name: master

  aws_amplify_webhook:
    master:
      app_id: ${aws_amplify_app.example.id}
      branch_name: ${aws_amplify_branch.master.branch_name}
      description: triggermaster```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `app_id` - (Required) Unique ID for an Amplify app.
* `branch_name` - (Required) Name for a branch that is part of the Amplify app.
* `description` - (Optional) Description for a webhook.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN for the webhook.
* `url` - URL of the webhook.

## Import

```bash
ytofu import aws_amplify_webhook.master a26b22a0-748b-4b57-b9a0-ae7e601fe4b1
```
