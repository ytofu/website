# Appsync Graphql API

Manage Appsync Graphql API resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_appsync_graphql_api:
    example:
      authentication_type: API_KEY
      name: example
```

## AWS IAM Authentication

```yaml
resource:
  aws_appsync_graphql_api:
    example:
      authentication_type: AWS_IAM
      name: example
```

## AWS Cognito User Pool Authentication

```yaml
resource:
  aws_appsync_graphql_api:
    example:
      authentication_type: AMAZON_COGNITO_USER_POOLS
      name: example
      user_pool_config:
        aws_region: ${data.aws_region.current.region}
        default_action: DENY
        user_pool_id: ${aws_cognito_user_pool.example.id}
```

## OpenID Connect Authentication

```yaml
resource:
  aws_appsync_graphql_api:
    example:
      authentication_type: OPENID_CONNECT
      name: example
      openid_connect_config:
        issuer: "https://example.com"
```

## AWS Lambda Authorizer Authentication

```yaml
resource:
  aws_appsync_graphql_api:
    example:
      authentication_type: AWS_LAMBDA
      name: example
      lambda_authorizer_config:
        authorizer_uri: "arn:aws:lambda:us-east-1:123456789012:function:custom_lambda_authorizer"

resource:
  aws_lambda_permission:
    appsync_lambda_authorizer:
      statement_id: appsync_lambda_authorizer
      action: "lambda:InvokeFunction"
      function_name: custom_lambda_authorizer
      principal: appsync.amazonaws.com
      source_arn: ${aws_appsync_graphql_api.example.arn}
```

## With Multiple Authentication Providers

```yaml
resource:
  aws_appsync_graphql_api:
    example:
      authentication_type: API_KEY
      name: example
      additional_authentication_provider:
        authentication_type: AWS_IAM
```

## With Schema

```yaml
resource:
  aws_appsync_graphql_api:
    example:
      authentication_type: AWS_IAM
      name: example
      schema: |
        schema {
        query: Query
        }
        type Query {
        test: Int
        }
```

## Enabling Logging

```yaml
data:
  aws_iam_policy_document:
    assume_role:
      statement:
        effect: Allow
        principals:
          type: Service
          identifiers: 
            - appsync.amazonaws.com
        actions: 
          - "sts:AssumeRole"

resource:
  aws_iam_role:
    example:
      name: example
      assume_role_policy: ${data.aws_iam_policy_document.assume_role.json}

resource:
  aws_iam_role_policy_attachment:
    example:
      policy_arn: "arn:aws:iam::aws:policy/service-role/AWSAppSyncPushToCloudWatchLogs"
      role: ${aws_iam_role.example.name}

resource:
  aws_appsync_graphql_api:
    example:
      log_config:
        cloudwatch_logs_role_arn: ${aws_iam_role.example.arn}
        field_log_level: ERROR
```

## Associate Web ACL (v2)

```yaml
resource:
  aws_appsync_graphql_api:
    example:
      authentication_type: API_KEY
      name: example

resource:
  aws_wafv2_web_acl_association:
    example:
      resource_arn: ${aws_appsync_graphql_api.example.arn}
      web_acl_arn: ${aws_wafv2_web_acl.example.arn}

resource:
  aws_wafv2_web_acl:
    example:
      name: managed-rule-example
      description: Example of a managed rule.
      scope: REGIONAL
      default_action:
        allow:
        rule:
          name: rule-1
          priority: 1
          override_action:
            block:
            statement:
              managed_rule_group_statement:
                name: AWSManagedRulesCommonRuleSet
                vendor_name: AWS
            visibility_config:
              cloudwatch_metrics_enabled: false
              metric_name: friendly-rule-metric-name
              sampled_requests_enabled: false
          visibility_config:
            cloudwatch_metrics_enabled: false
            metric_name: friendly-metric-name
            sampled_requests_enabled: false
```

## GraphQL run complexity, query depth, and introspection

```yaml
resource:
  aws_appsync_graphql_api:
    example:
      authentication_type: AWS_IAM
      name: example
      introspection_config: ENABLED
      query_depth_limit: 2
      resolver_count_limit: 2
```
