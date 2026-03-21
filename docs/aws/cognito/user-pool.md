# Cognito User Pool

Create and manage Cognito user pools using ytofu YAML.

## Basic User Pool

```yaml
resource:
  aws_cognito_user_pool:
    pool:
      name: mypool
```

## With MFA

```yaml
resource:
  aws_cognito_user_pool:
    example:
      name: example
      mfa_configuration: "ON"
      sms_authentication_message: "Your code is {####}"
      sms_configuration:
        external_id: example
        sns_caller_arn: ${aws_iam_role.example.arn}
      software_token_mfa_configuration:
        enabled: true
```

## With Password Policy and Schema

```yaml
resource:
  aws_cognito_user_pool:
    example:
      name: example
      auto_verified_attributes:
        - email
      password_policy:
        minimum_length: 10
        require_lowercase: true
        require_numbers: true
        require_symbols: true
        require_uppercase: true
        temporary_password_validity_days: 7
      schema:
        - attribute_data_type: String
          developer_only_attribute: false
          mutable: true
          name: email
          required: true
          string_attribute_constraints:
            max_length: "2048"
            min_length: "0"
```

## With Account Recovery

```yaml
resource:
  aws_cognito_user_pool:
    example:
      name: example
      account_recovery_setting:
        recovery_mechanism:
          - name: verified_email
            priority: 1
          - name: verified_phone_number
            priority: 2
```

## With Lambda Triggers

```yaml
resource:
  aws_cognito_user_pool:
    example:
      name: example
      lambda_config:
        pre_sign_up: ${aws_lambda_function.pre_sign_up.arn}
        post_confirmation: ${aws_lambda_function.post_confirmation.arn}
        pre_authentication: ${aws_lambda_function.pre_auth.arn}
        custom_message: ${aws_lambda_function.custom_message.arn}
```
