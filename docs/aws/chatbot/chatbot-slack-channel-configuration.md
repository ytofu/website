# Resource: aws_chatbot_slack_channel_configuration

ytofu resource for managing an AWS Chatbot Slack Channel Configuration.

## Basic Example

```yaml
resource:
  aws_chatbot_slack_channel_configuration:
    test:
      configuration_name: min-slaka-kanal
      iam_role_arn: ${aws_iam_role.test.arn}
      slack_channel_id: C07EZ1ABC23
      slack_team_id: T07EA123LEP
      tags:
        Name: min-slaka-kanal
```

## Argument Reference

The following arguments are required:

* `configuration_name` - (Required) Name of the Slack channel configuration.
* `iam_role_arn` - (Required) User-defined role that AWS Chatbot assumes. This is not the service-linked role.
* `slack_channel_id` - (Required) ID of the Slack channel. For example, `C07EZ1ABC23`.
* `slack_team_id` - (Required) ID of the Slack workspace authorized with AWS Chatbot. For example, `T07EA123LEP`.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `guardrail_policy_arns` - (Optional) List of IAM policy ARNs that are applied as channel guardrails. The AWS managed `AdministratorAccess` policy is applied by default if this is not set.
* `logging_level` - (Optional) Logging levels include `ERROR`, `INFO`, or `NONE`.
* `sns_topic_arns` - (Optional) ARNs of the SNS topics that deliver notifications to AWS Chatbot.
* `tags` - (Optional) Map of tags assigned to the resource.
* `user_authorization_required` - (Optional) Enables use of a user role requirement in your chat configuration.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `chat_configuration_arn` - ARN of the Slack channel configuration.
* `slack_channel_name` - Name of the Slack channel.
* `slack_team_name` - Name of the Slack team.
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Timeouts

Configuration options:

* `create` - (Default `20m`)
* `update` - (Default `20m`)
* `delete` - (Default `20m`)

## Import

```bash
ytofu import aws_chatbot_slack_channel_configuration.example arn:aws:chatbot::123456789012:chat-configuration/slack-channel/min-slaka-kanal
```
