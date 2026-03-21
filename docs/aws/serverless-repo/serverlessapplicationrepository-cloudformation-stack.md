# Resource: aws_serverlessapplicationrepository_cloudformation_stack

Deploys an Application CloudFormation Stack from the Serverless Application Repository.

## Basic Example

```yaml
resource:
  aws_serverlessapplicationrepository_cloudformation_stack:
    postgres-rotator:
      name: postgres-rotator
      application_id: "arn:aws:serverlessrepo:us-east-1:297356227824:applications/SecretsManagerRDSPostgreSQLRotationSingleUser"
      capabilities:
        - CAPABILITY_IAM
        - CAPABILITY_RESOURCE_POLICY
      parameters:
        functionName: func-postgres-rotator
        endpoint: "secretsmanager.${data.aws_region.current.region}.${data.aws_partition.current.dns_suffix}"

data:
  aws_partition:
    current:

data:
  aws_region:
    current:
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) The name of the stack to create. The resource deployed in AWS will be prefixed with `serverlessrepo-`
* `application_id` - (Required) The ARN of the application from the Serverless Application Repository.
* `capabilities` - (Required) A list of capabilities. Valid values are `CAPABILITY_IAM`, `CAPABILITY_NAMED_IAM`, `CAPABILITY_RESOURCE_POLICY`, or `CAPABILITY_AUTO_EXPAND`
* `parameters` - (Optional) A map of Parameter structures that specify input parameters for the stack.
* `semantic_version` - (Optional) The version of the application to deploy. If not supplied, deploys the latest version.
* `tags` - (Optional) A list of tags to associate with this stack. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - A unique identifier of the stack.
* `outputs` - A map of outputs from the stack.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_serverlessapplicationrepository_cloudformation_stack.example serverlessrepo-postgres-rotator
```
