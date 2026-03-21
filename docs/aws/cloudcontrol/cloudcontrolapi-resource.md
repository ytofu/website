# Resource: aws_cloudcontrolapi_resource

Manages a Cloud Control API Resource. The configuration and lifecycle handling of these resources is proxied through Cloud Control API handlers to the backend service.

## Basic Example

```yaml
resource:
  aws_cloudcontrolapi_resource:
    example:
      type_name: "AWS::ECS::Cluster"
      desired_state: '{ "ClusterName": "example" "Tags": [ { "Key": "CostCenter" "Value": "IT" } ] }'
```

## Argument Reference

The following arguments are required:

* `desired_state` - (Required) JSON string matching the CloudFormation resource type schema with desired configuration. ytofu configuration expressions can be converted into JSON using the `jsonencode()` function.
* `type_name` - (Required) CloudFormation resource type name. For example, `AWS::EC2::VPC`.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `role_arn` - (Optional) Amazon Resource Name (ARN) of the IAM Role to assume for operations.
* `schema` - (Optional) JSON string of the CloudFormation resource type schema which is used for plan time validation where possible. Automatically fetched if not provided. In large scale environments with multiple resources using the same `type_name`, it is recommended to fetch the schema once via the `aws_cloudformation_type` data source and use this argument to reduce `DescribeType` API operation throttling. This value is marked sensitive only to prevent large plan differences from showing.
* `type_version_id` - (Optional) Identifier of the CloudFormation resource type version.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `properties` - JSON string matching the CloudFormation resource type schema with current configuration. Underlying attributes can be referenced via the `jsondecode()` function, for example, `jsondecode(data.aws_cloudcontrolapi_resource.example.properties)["example"]`.
