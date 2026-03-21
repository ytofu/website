# Ssoadmin Application

Manage Ssoadmin Application resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_ssoadmin_instances:
    example:

resource:
  aws_ssoadmin_application:
    example:
      name: example
      application_provider_arn: "arn:aws:sso::aws:applicationProvider/custom"
      instance_arn: ${data.aws_ssoadmin_instances.example.arns[0]}
```

## With Portal Options

```yaml
data:
  aws_ssoadmin_instances:
    example:

resource:
  aws_ssoadmin_application:
    example:
      name: example
      application_provider_arn: "arn:aws:sso::aws:applicationProvider/custom"
      instance_arn: ${data.aws_ssoadmin_instances.example.arns[0]}
      portal_options:
        visibility: ENABLED
        sign_in_options:
          application_url: "http://example.com"
          origin: APPLICATION
```
