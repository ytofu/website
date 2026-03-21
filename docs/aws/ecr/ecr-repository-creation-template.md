# ECR Repository Creation Template

Manage ECR Repository Creation Template resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_iam_policy_document:
    example:
      statement:
        sid: new policy
        effect: Allow
        principals:
          type: AWS
          identifiers: 
            - 123456789012
        actions:
          - "ecr:GetDownloadUrlForLayer"
          - "ecr:BatchGetImage"
          - "ecr:BatchCheckLayerAvailability"
          - "ecr:PutImage"
          - "ecr:InitiateLayerUpload"
          - "ecr:UploadLayerPart"
          - "ecr:CompleteLayerUpload"
          - "ecr:DescribeRepositories"
          - "ecr:GetRepositoryPolicy"
          - "ecr:ListImages"
          - "ecr:DeleteRepository"
          - "ecr:BatchDeleteImage"
          - "ecr:SetRepositoryPolicy"
          - "ecr:DeleteRepositoryPolicy"

resource:
  aws_ecr_repository_creation_template:
    example:
      prefix: example
      description: An example template
      image_tag_mutability: IMMUTABLE
      custom_role_arn: "arn:aws:iam::123456789012:role/example"
      applied_for:
        - PULL_THROUGH_CACHE
      encryption_configuration:
        encryption_type: AES256
      repository_policy: ${data.aws_iam_policy_document.example.json}
      lifecycle_policy: |
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
      resource_tags:
        Foo: Bar
```
