# Datazone Glossary

Manage Datazone Glossary resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_iam_role:
    domain_execution_role:
      name: example_name
      assume_role_policy: '{ "Version": "2012-10-17" "Statement": [ { "Action": ["sts:AssumeRole", "sts:TagSession"] "Effect": "Allow" "Principal": { "Service": "datazone.amazonaws.com" } }, { "Action": ["sts:AssumeRole", "sts:TagSession"] "Effect": "Allow" "Principal": { "Service": "cloudformation.amazonaws.com" } }, ] }'
      inline_policy:
        name: example_name
        policy: '{ "Version": "2012-10-17" "Statement": [ { "Action": [ "datazone:*", "ram:*", "sso:*", "kms:*", ] "Effect": "Allow" "Resource": "*" }, ] }'

resource:
  aws_datazone_domain:
    test:
      name: example_name
      domain_execution_role: ${aws_iam_role.domain_execution_role.arn}

resource:
  aws_security_group:
    test:
      name: example_name

resource:
  aws_datazone_project:
    test:
      domain_identifier: ${aws_datazone_domain.test.id}
      glossary_terms: 
        - 2N8w6XJCwZf
      name: example_name
      description: desc
      skip_deletion_check: true

resource:
  aws_datazone_glossary:
    test:
      description: description
      name: example_name
      owning_project_identifier: ${aws_datazone_project.test.id}
      status: DISABLED
      domain_identifier: ${aws_datazone_project.test.domain_identifier}
```

## Basic Usage

```yaml
resource:
  aws_datazone_glossary:
    test:
      description: description
      name: example_name
      owning_project_identifier: ${aws_datazone_project.test.id}
      status: DISABLED
      domain_identifier: ${aws_datazone_project.test.domain_identifier}
```
