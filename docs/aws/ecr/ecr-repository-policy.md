# ECR Repository Policy

Manage ECR Repository Policy resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ecr_repository:
    example:
      name: example-repo

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
  aws_ecr_repository_policy:
    example:
      repository: ${aws_ecr_repository.example.name}
      policy: ${data.aws_iam_policy_document.example.json}
```
