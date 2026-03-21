# Cognito Identity Pool Roles Attachment

Manage Cognito Identity Pool Roles Attachment resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cognito_identity_pool:
    main:
      identity_pool_name: identity pool
      allow_unauthenticated_identities: false
      supported_login_providers: 

data:
  aws_iam_policy_document:
    authenticated:
      statement:
        effect: Allow
        principals:
          type: Federated
          identifiers: 
            - cognito-identity.amazonaws.com
        actions: 
          - "sts:AssumeRoleWithWebIdentity"
        condition:
          test: StringEquals
          values: 
            - ${aws_cognito_identity_pool.main.id}
        condition:
          test: "ForAnyValue:StringLike"
          values: 
            - authenticated

resource:
  aws_iam_role:
    authenticated:
      name: cognito_authenticated
      assume_role_policy: ${data.aws_iam_policy_document.authenticated.json}

data:
  aws_iam_policy_document:
    authenticated_role_policy:
      statement:
        effect: Allow
        actions:
          - "mobileanalytics:PutEvents"
          - "cognito-sync:*"
          - "cognito-identity:*"
        resources: 
          - "*"

resource:
  aws_iam_role_policy:
    authenticated:
      name: authenticated_policy
      role: ${aws_iam_role.authenticated.id}
      policy: ${data.aws_iam_policy_document.authenticated_role_policy.json}

resource:
  aws_cognito_identity_pool_roles_attachment:
    main:
      identity_pool_id: ${aws_cognito_identity_pool.main.id}
      role_mapping:
        identity_provider: graph.facebook.com
        ambiguous_role_resolution: AuthenticatedRole
        type: Rules
        mapping_rule:
          claim: isAdmin
          match_type: Equals
          role_arn: ${aws_iam_role.authenticated.arn}
          value: paid
      roles: 
```
