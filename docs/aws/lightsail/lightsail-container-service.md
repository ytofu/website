# Lightsail Container Service

Manage Lightsail Container Service resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_lightsail_container_service:
    example:
      name: container-service-1
      power: nano
      scale: 1
      is_disabled: false
      tags:
        foo1: bar1
        foo2: 
```

## Public Domain Names

```yaml
resource:
  aws_lightsail_container_service:
    example:
      public_domain_names:
        certificate:
          certificate_name: example-certificate
          domain_names:
            - www.example.com
            - 
```

## Private Registry Access

```yaml
resource:
  aws_lightsail_container_service:
    example:
      private_registry_access:
        ecr_image_puller_role:
          is_active: true

data:
  aws_iam_policy_document:
    example:
      statement:
        effect: Allow
        principals:
          type: AWS
          identifiers: 
            - ${aws_lightsail_container_service.example.private_registry_access[0].ecr_image_puller_role[0].principal_arn}
        actions:
          - "ecr:BatchGetImage"
          - "ecr:GetDownloadUrlForLayer"

resource:
  aws_ecr_repository_policy:
    example:
      repository: ${aws_ecr_repository.example.name}
      policy: ${data.aws_iam_policy_document.example.json}
```
