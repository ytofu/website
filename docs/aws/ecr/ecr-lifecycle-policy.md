# ECR Lifecycle Policy

Manage ECR Lifecycle Policy resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ecr_repository:
    example:
      name: example-repo

resource:
  aws_ecr_lifecycle_policy:
    example:
      repository: ${aws_ecr_repository.example.name}
      policy: |
        {
        "rules": [
        {
        "rulePriority": 1,
        "description": "Expire images older than 14 days",
        "selection": {
        "tagStatus": "untagged",
        "countType": "sinceImagePushed",
        "countUnit": "days",
        "countNumber": 14
        },
        "action": {
        "type": "expire"
        }
        }
        ]
        }
```

## Policy on Tagged Images

```yaml
resource:
  aws_ecr_repository:
    example:
      name: example-repo

resource:
  aws_ecr_lifecycle_policy:
    example:
      repository: ${aws_ecr_repository.example.name}
      policy: |
        {
        "rules": [
        {
        "rulePriority": 1,
        "description": "Keep last 30 images",
        "selection": {
        "tagStatus": "tagged",
        "tagPrefixList": ["v"],
        "countType": "imageCountMoreThan",
        "countNumber": 30
        },
        "action": {
        "type": "expire"
        }
        }
        ]
        }
```

## Policy to Archive and Delete

```yaml
resource:
  aws_ecr_repository:
    example:
      name: example-repo

resource:
  aws_ecr_lifecycle_policy:
    example:
      repository: ${aws_ecr_repository.example.name}
      policy: |
        {
        "rules": [
        {
        "rulePriority": 1,
        "description": "Archive images not pulled in 90 days",
        "selection": {
        "tagStatus": "any",
        "countType": "sinceImagePulled",
        "countUnit": "days",
        "countNumber": 90
        },
        "action": {
        "type": "transition",
        "targetStorageClass": "archive"
        }
        },
        {
        "rulePriority": 2,
        "description": "Delete images archived for more than 365 days",
        "selection": {
        "tagStatus": "any",
        "storageClass": "archive",
        "countType": "sinceImageTransitioned",
        "countUnit": "days",
        "countNumber": 365
        },
        "action": {
        "type": "expire"
        }
        }
        ]
        }
```
