# Ecrpublic Repository Policy

Manage Ecrpublic Repository Policy resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ecrpublic_repository:
    example:
      repository_name: example

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
  aws_ecrpublic_repository_policy:
    example:
      repository_name: ${aws_ecrpublic_repository.example.repository_name}
      policy: ${data.aws_iam_policy_document.example.json}
```
