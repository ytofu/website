# Resource: aws_vpc_endpoint_policy

Provides a VPC Endpoint Policy resource.

## Basic Example

```yaml
data:
  aws_vpc_endpoint_service:
    example:
      service: dynamodb

resource:
  aws_vpc:
    example:
      cidr_block: 10.0.0.0/16

  aws_vpc_endpoint:
    example:
      service_name: ${data.aws_vpc_endpoint_service.example.service_name}
      vpc_id: ${aws_vpc.example.id}

  aws_vpc_endpoint_policy:
    example:
      vpc_endpoint_id: ${aws_vpc_endpoint.example.id}
      policy: '{ "Version" : "2012-10-17", "Statement" : [ { "Sid" : "AllowAll", "Effect" : "Allow", "Principal" : { "AWS" : "*" }, "Action" : [ "dynamodb:*" ], "Resource" : "*" } ] }'```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `vpc_endpoint_id` - (Required) The VPC Endpoint ID.
* `policy` - (Optional) A policy to attach to the endpoint that controls access to the service. Defaults to full access. All `Gateway` and some `Interface` endpoints support policies - see the [relevant AWS documentation](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-endpoints-access.html) for more details. For more information about building AWS IAM policy documents with ytofu, see the [AWS IAM Policy Document Guide](https://learn.hashicorp.com/terraform/aws/iam-policy).

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The ID of the VPC endpoint.

## Import

```bash
ytofu import aws_vpc_endpoint_policy.example vpce-3ecf2a57
```
