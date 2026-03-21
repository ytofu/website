# Cognito User Pool Client

Manage Cognito User Pool Client resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cognito_user_pool_client:
    client:
      name: client
      user_pool_id: ${aws_cognito_user_pool.pool.id}

resource:
  aws_cognito_user_pool:
    pool:
      name: pool
```

## Create a user pool client with no SRP authentication

```yaml
resource:
  aws_cognito_user_pool_client:
    client:
      name: client
      user_pool_id: ${aws_cognito_user_pool.pool.id}
      generate_secret: true
      explicit_auth_flows: 
        - ADMIN_NO_SRP_AUTH

resource:
  aws_cognito_user_pool:
    pool:
      name: pool
```

## Create a user pool client with pinpoint analytics

```yaml
resource:
  aws_cognito_user_pool_client:
    test:
      name: pool_client
      user_pool_id: ${aws_cognito_user_pool.test.id}
      analytics_configuration:
        application_id: ${aws_pinpoint_app.test.application_id}
        external_id: some_id
        role_arn: ${aws_iam_role.test.arn}
        user_data_shared: true

resource:
  aws_cognito_user_pool:
    test:
      name: pool

data:
  aws_caller_identity:
    current:

resource:
  aws_pinpoint_app:
    test:
      name: pinpoint

data:
  aws_iam_policy_document:
    assume_role:
      statement:
        effect: Allow
        principals:
          type: Service
          identifiers: 
            - cognito-idp.amazonaws.com
        actions: 
          - "sts:AssumeRole"

resource:
  aws_iam_role:
    test:
      name: role
      assume_role_policy: ${data.aws_iam_policy_document.assume_role.json}

data:
  aws_iam_policy_document:
    test:
      statement:
        effect: Allow
        actions:
          - "mobiletargeting:UpdateEndpoint"
          - "mobiletargeting:PutEvents"
        resources: 
          - "arn:aws:mobiletargeting:*:${data.aws_caller_identity.current.account_id}:apps/${aws_pinpoint_app.test.application_id}*"

resource:
  aws_iam_role_policy:
    test:
      name: role_policy
      role: ${aws_iam_role.test.id}
      policy: ${data.aws_iam_policy_document.test.json}
```

## Create a user pool client with Cognito as the identity provider

```yaml
resource:
  aws_cognito_user_pool_client:
    userpool_client:
      name: client
      user_pool_id: ${aws_cognito_user_pool.pool.id}
      callback_urls: 
        - "https://example.com"
      allowed_oauth_flows_user_pool_client: true
      allowed_oauth_flows: 
        - code
        - implicit
      allowed_oauth_scopes: 
        - email
        - openid
      supported_identity_providers: 
        - COGNITO

resource:
  aws_cognito_user_pool:
    pool:
      name: pool
```

## Create a user pool client with refresh token rotation

```yaml
resource:
  aws_cognito_user_pool_client:
    userpool_client:
      name: client
      user_pool_id: ${aws_cognito_user_pool.pool.id}
      explicit_auth_flows: 
        - ADMIN_NO_SRP_AUTH
      refresh_token_rotation:
        feature: ENABLED
        retry_grace_period_seconds: 10

resource:
  aws_cognito_user_pool:
    pool:
      name: pool
```
