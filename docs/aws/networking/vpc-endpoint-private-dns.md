# Resource: aws_vpc_endpoint_private_dns

ytofu resource for enabling private DNS on an AWS VPC (Virtual Private Cloud) Endpoint.

## Basic Example

```yaml
resource:
  aws_vpc_endpoint_private_dns:
    example:
      vpc_endpoint_id: ${aws_vpc_endpoint.example.id}
      private_dns_enabled: true
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `private_dns_enabled` - (Required) Indicates whether a private hosted zone is associated with the VPC. Only applicable for `Interface` endpoints.
* `vpc_endpoint_id` - (Required) VPC endpoint identifier.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_vpc_endpoint_private_dns.example vpce-abcd-1234
```
