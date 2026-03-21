# Amplify Branch

Manage Amplify Branch resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_amplify_app:
    example:
      name: app

resource:
  aws_amplify_branch:
    master:
      app_id: ${aws_amplify_app.example.id}
      branch_name: master
      framework: React
      stage: PRODUCTION
      environment_variables:
        REACT_APP_API_SERVER: "https://api.example.com"
```

## Basic Authentication

```yaml
resource:
  aws_amplify_app:
    example:
      name: app

resource:
  aws_amplify_branch:
    master:
      app_id: ${aws_amplify_app.example.id}
      branch_name: master
      enable_basic_auth: true
      basic_auth_credentials: base64-encoded-content
```

## Notifications

```yaml
resource:
  aws_amplify_app:
    example:
      name: app

resource:
  aws_amplify_branch:
    master:
      app_id: ${aws_amplify_app.example.id}
      branch_name: master
      enable_notification: true

resource:
  aws_cloudwatch_event_rule:
    amplify_app_master:
      name: "amplify-${aws_amplify_app.app.id}-${aws_amplify_branch.master.branch_name}-branch-notification"
      description: "AWS Amplify build notifications for :  App: ${aws_amplify_app.app.id} Branch: ${aws_amplify_branch.master.branch_name}"
      event_pattern: '{ "detail" = { "appId" = [ aws_amplify_app.example.id ] "branchName" = [ aws_amplify_branch.master.branch_name ], "jobStatus" = [ "SUCCEED", "FAILED", "STARTED" ] } "detail-type" = [ "Amplify Deployment Status Change" ] "source" = [ "aws.amplify" ] }'

resource:
  aws_cloudwatch_event_target:
    amplify_app_master:
      rule: ${aws_cloudwatch_event_rule.amplify_app_master.name}
      target_id: ${aws_amplify_branch.master.branch_name}
      arn: ${aws_sns_topic.amplify_app_master.arn}
      input_transformer:
        input_paths:
          jobId: $.detail.jobId
          appId: $.detail.appId
          region: $.region
          branch: $.detail.branchName
          status: $.detail.jobStatus
        input_template: "\"Build notification from the AWS Amplify Console for app: https://<branch>.<appId>.amplifyapp.com/. Your build status is <status>. Go to https://console.aws.amazon.com/amplify/home?region=<region>#<appId>/<branch>/<jobId> to view details on your build. \""

resource:
  aws_sns_topic:
    amplify_app_master:
      name: "amplify-${aws_amplify_app.app.id}_${aws_amplify_branch.master.branch_name}"

data:
  aws_iam_policy_document:
    amplify_app_master:
      statement:
        sid: "Allow_Publish_Events ${aws_amplify_branch.master.arn}"
        effect: Allow
        actions:
          - "SNS:Publish"
        principals:
          type: Service
          identifiers:
            - events.amazonaws.com
        resources:
          - ${aws_sns_topic.amplify_app_master.arn}

resource:
  aws_sns_topic_policy:
    amplify_app_master:
      arn: ${aws_sns_topic.amplify_app_master.arn}
      policy: ${data.aws_iam_policy_document.amplify_app_master.json}

resource:
  aws_sns_topic_subscription:
    this:
      topic_arn: ${aws_sns_topic.amplify_app_master.arn}
      protocol: email
      endpoint: user@acme.com
```
