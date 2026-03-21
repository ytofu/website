# Resource: aws_ecr_lifecycle_policy

Manages an ECR repository lifecycle policy.

## Basic Example

```yaml
resource:
  aws_ecr_repository:
    example:
      name: example-repo

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
        }```

## Policy on Tagged Images

```yaml
resource:
  aws_ecr_repository:
    example:
      name: example-repo

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
        }```

## Policy to Archive and Delete

```yaml
resource:
  aws_ecr_repository:
    example:
      name: example-repo

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
        }```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `repository` - (Required) Name of the repository to apply the policy.
* `policy` - (Required) The policy document. This is a JSON formatted string. See more details about [Policy Parameters](http://docs.aws.amazon.com/AmazonECR/latest/userguide/LifecyclePolicies.html#lifecycle_policy_parameters) in the official AWS docs. Consider using the `aws_ecr_lifecycle_policy_document` data_source to generate/manage the JSON document used for the `policy` argument.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `repository` - The name of the repository.
* `registry_id` - The registry ID where the repository was created.

## Import

```bash
ytofu import aws_ecr_lifecycle_policy.example tf-example
```
