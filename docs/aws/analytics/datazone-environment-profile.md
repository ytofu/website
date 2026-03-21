# Datazone Environment Profile

Manage Datazone Environment Profile resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_iam_role:
    domain_execution_role:
      name: example-name
      assume_role_policy: '{ "Version": "2012-10-17" "Statement": [ { "Action": ["sts:AssumeRole", "sts:TagSession"] "Effect": "Allow" "Principal": { "Service": "datazone.amazonaws.com" } }, { "Action": ["sts:AssumeRole", "sts:TagSession"] "Effect": "Allow" "Principal": { "Service": "cloudformation.amazonaws.com" } }, ] }'
      inline_policy:
        name: example-name
        policy: '{ "Version": "2012-10-17" "Statement": [ { "Action": [ "datazone:*", "ram:*", "sso:*", "kms:*", ] "Effect": "Allow" "Resource": "*" }, ] }'

resource:
  aws_datazone_domain:
    test:
      name: example-name
      domain_execution_role: ${aws_iam_role.domain_execution_role.arn}

resource:
  aws_security_group:
    test:
      name: example-name

resource:
  aws_datazone_project:
    test:
      domain_identifier: ${aws_datazone_domain.test.id}
      glossary_terms: 
        - 2N8w6XJCwZf
      name: example-name
      description: desc
      skip_deletion_check: true

data:
  aws_caller_identity:
    test:

data:
  aws_region:
    test:

data:
  aws_datazone_environment_blueprint:
    test:
      domain_id: ${aws_datazone_domain.test.id}
      name: DefaultDataLake
      managed: true

resource:
  aws_datazone_environment_blueprint_configuration:
    test:
      domain_id: ${aws_datazone_domain.test.id}
      environment_blueprint_id: ${data.aws_datazone_environment_blueprint.test.id}
      provisioning_role_arn: ${aws_iam_role.domain_execution_role.arn}
      enabled_regions: 
        - ${data.aws_region.test.name}

resource:
  aws_datazone_environment_profile:
    test:
      aws_account_id: ${data.aws_caller_identity.test.account_id}
      aws_account_region: ${data.aws_region.test.name}
      description: description
      environment_blueprint_identifier: ${data.aws_datazone_environment_blueprint.test.id}
      name: example-name
      project_identifier: ${aws_datazone_project.test.id}
      domain_identifier: ${aws_datazone_domain.test.id}
      user_parameters:
        name: consumerGlueDbName
        value: value
```
