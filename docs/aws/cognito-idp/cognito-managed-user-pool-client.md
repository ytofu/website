# Cognito Managed User Pool Client

Manage Cognito Managed User Pool Client resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cognito_managed_user_pool_client:
    example:
      name_prefix: AmazonOpenSearchService-example-
      user_pool_id: ${aws_cognito_user_pool.example.id}
      depends_on:
        - ${aws_opensearch_domain.example}

resource:
  aws_cognito_user_pool:
    example:
      name: example

resource:
  aws_cognito_user_pool_domain:
    example:
      domain: example
      user_pool_id: ${aws_cognito_user_pool.example.id}

resource:
  aws_cognito_identity_pool:
    example:
      identity_pool_name: example
      lifecycle:
        ignore_changes: 
          - cognito_identity_providers

resource:
  aws_opensearch_domain:
    example:
      domain_name: example
      cognito_options:
        enabled: true
        user_pool_id: ${aws_cognito_user_pool.example.id}
        identity_pool_id: ${aws_cognito_identity_pool.example.id}
        role_arn: ${aws_iam_role.example.arn}
      ebs_options:
        ebs_enabled: true
        volume_size: 10
      depends_on:
        - ${aws_cognito_user_pool_domain.example}
        - ${aws_iam_role_policy_attachment.example}

resource:
  aws_iam_role:
    example:
      name: example-role
      path: /service-role/
      assume_role_policy: ${data.aws_iam_policy_document.example.json}

data:
  aws_iam_policy_document:
    example:
      statement:
        sid: 
        actions: 
          - "sts:AssumeRole"
        effect: Allow
        principals:
          type: Service
          identifiers:
            - "es.${data.aws_partition.current.dns_suffix}"

resource:
  aws_iam_role_policy_attachment:
    example:
      role: ${aws_iam_role.example.name}
      policy_arn: "arn:${data.aws_partition.current.partition}:iam::aws:policy/AmazonESCognitoAccess"
      depends_on:
        - ${aws_opensearch_domain.example}

data:
  aws_partition:
    current:
```

## Using Name Pattern

```yaml
resource:
  aws_cognito_managed_user_pool_client:
    example:
      name_pattern: ^AmazonOpenSearchService-example-(\\w+)$
      user_pool_id: ${aws_cognito_user_pool.example.id}
```
