# Resource: aws_sagemaker_servicecatalog_portfolio_status

Manages status of Service Catalog in SageMaker. Service Catalog is used to create SageMaker AI projects.

## Basic Example

```yaml
resource:
  aws_sagemaker_servicecatalog_portfolio_status:
    example:
      status: Enabled
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `status` - (Required) Whether Service Catalog is enabled or disabled in SageMaker. Valid values are `Enabled` and `Disabled`.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The AWS Region the Servicecatalog portfolio status resides in.

## Import

```bash
ytofu import aws_sagemaker_servicecatalog_portfolio_status.example us-east-1
```
