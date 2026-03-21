# Sagemaker Model Package Group Policy

Manage Sagemaker Model Package Group Policy resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_caller_identity:
    current:

data:
  aws_iam_policy_document:
    example:
      statement:
        sid: AddPermModelPackageGroup
        actions: 
          - "sagemaker:DescribeModelPackage"
          - "sagemaker:ListModelPackages"
        resources: 
          - ${aws_sagemaker_model_package_group.example.arn}
        principals:
          identifiers: 
            - ${data.aws_caller_identity.current.account_id}
          type: AWS

resource:
  aws_sagemaker_model_package_group:
    example:
      model_package_group_name: example

resource:
  aws_sagemaker_model_package_group_policy:
    example:
      model_package_group_name: ${aws_sagemaker_model_package_group.example.model_package_group_name}
      resource_policy: example-value
```
