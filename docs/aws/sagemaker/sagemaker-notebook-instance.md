# Sagemaker Notebook Instance

Manage Sagemaker Notebook Instance resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_sagemaker_notebook_instance:
    ni:
      name: my-notebook-instance
      role_arn: ${aws_iam_role.role.arn}
      instance_type: ml.t2.medium
      tags:
        Name: foo
```

## Code repository usage

```yaml
resource:
  aws_sagemaker_code_repository:
    example:
      code_repository_name: my-notebook-instance-code-repo
      git_config:
        repository_url: "https://github.com/hashicorp/terraform-provider-aws.git"

resource:
  aws_sagemaker_notebook_instance:
    ni:
      name: my-notebook-instance
      role_arn: ${aws_iam_role.role.arn}
      instance_type: ml.t2.medium
      default_code_repository: ${aws_sagemaker_code_repository.example.code_repository_name}
      tags:
        Name: foo
```
