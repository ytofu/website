# Resource: aws_sagemaker_model_package_group_policy

Provides a SageMaker AI Model Package Group Policy resource.

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

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `model_package_group_name` - (Required) The name of the model package group.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The name of the Model Package Package Group.

## Import

```bash
ytofu import aws_sagemaker_model_package_group_policy.example example
```
