# Datazone Glossary Term

Manage Datazone Glossary Term resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_iam_role:
    example:
      name: example
      assume_role_policy: '{ "Version": "2012-10-17" "Statement": [ { "Action": ["sts:AssumeRole", "sts:TagSession"] "Effect": "Allow" "Principal": { "Service": "datazone.amazonaws.com" } }, { "Action": ["sts:AssumeRole", "sts:TagSession"] "Effect": "Allow" "Principal": { "Service": "cloudformation.amazonaws.com" } }, ] }'
      inline_policy:
        name: example
        policy: '{ "Version": "2012-10-17" "Statement": [ { "Action": [ "datazone:*", "ram:*", "sso:*", "kms:*", ] "Effect": "Allow" "Resource": "*" }, ] }'

resource:
  aws_datazone_domain:
    example:
      name: example_name
      domain_execution_role: ${aws_iam_role.example.arn}

resource:
  aws_security_group:
    example:
      name: example_name

resource:
  aws_datazone_project:
    example:
      domain_identifier: ${aws_datazone_domain.example.id}
      glossary_terms: 
        - 2N8w6XJCwZf
      name: example
      skip_deletion_check: true

resource:
  aws_datazone_glossary:
    example:
      description: description
      name: example
      owning_project_identifier: ${aws_datazone_project.example.id}
      status: ENABLED
      domain_identifier: ${aws_datazone_project.example.domain_identifier}

resource:
  aws_datazone_glossary_term:
    example:
      domain_identifier: ${aws_datazone_domain.example.id}
      glossary_identifier: ${aws_datazone_glossary.example.id}
      name: example
      status: ENABLED
```
