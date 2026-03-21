# Datazone Domain

Manage Datazone Domain resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_iam_role:
    domain_execution_role:
      name: my_domain_execution_role
      assume_role_policy: '{ "Version": "2012-10-17" "Statement": [ { "Action": ["sts:AssumeRole", "sts:TagSession"] "Effect": "Allow" "Principal": { "Service": "datazone.amazonaws.com" } }, { "Action": ["sts:AssumeRole", "sts:TagSession"] "Effect": "Allow" "Principal": { "Service": "cloudformation.amazonaws.com" } }, ] }'

resource:
  aws_iam_role_policy:
    domain_execution_role:
      role: ${aws_iam_role.domain_execution_role.name}
      policy: '{ "Version": "2012-10-17" "Statement": [ { # Consider scoping down "Action": [ "datazone:*", "ram:*", "sso:*", "kms:*", ] "Effect": "Allow" "Resource": "*" }, ] }'

resource:
  aws_datazone_domain:
    example:
      name: example
      domain_execution_role: ${aws_iam_role.domain_execution_role.arn}
```

## V2 Domain

```yaml
data:
  aws_caller_identity:
    current:

data:
  aws_iam_policy_document:
    assume_role_domain_execution:
      statement:
        actions:
          - "sts:AssumeRole"
          - "sts:TagSession"
          - "sts:SetContext"
        principals:
          type: Service
          identifiers: 
            - datazone.amazonaws.com
        condition:
          test: StringEquals
          values: 
            - ${data.aws_caller_identity.current.account_id}
        condition:
          test: "ForAllValues:StringLike"
          values: 
            - "datazone*"

resource:
  aws_iam_role:
    domain_execution:
      assume_role_policy: ${data.aws_iam_policy_document.assume_role_domain_execution.json}
      name: example-domain-execution-role

data:
  aws_iam_policy:
    domain_execution_role:
      name: SageMakerStudioDomainExecutionRolePolicy

resource:
  aws_iam_role_policy_attachment:
    domain_execution:
      policy_arn: ${data.aws_iam_policy.domain_execution_role.arn}
      role: ${aws_iam_role.domain_execution.name}

data:
  aws_iam_policy_document:
    assume_role_domain_service:
      statement:
        actions: 
          - "sts:AssumeRole"
        principals:
          type: Service
          identifiers: 
            - datazone.amazonaws.com
        condition:
          test: StringEquals
          values: 
            - ${data.aws_caller_identity.current.account_id}

resource:
  aws_iam_role:
    domain_service:
      assume_role_policy: ${data.aws_iam_policy_document.assume_role_domain_service.json}
      name: example-domain-service-role

data:
  aws_iam_policy:
    domain_service_role:
      name: SageMakerStudioDomainServiceRolePolicy

resource:
  aws_iam_role_policy_attachment:
    domain_service:
      policy_arn: ${data.aws_iam_policy.domain_service_role.arn}
      role: ${aws_iam_role.domain_service.name}

resource:
  aws_datazone_domain:
    example:
      name: example-domain
      domain_execution_role: ${aws_iam_role.domain_execution.arn}
      domain_version: V2
      service_role: ${aws_iam_role.domain_service.arn}
```
