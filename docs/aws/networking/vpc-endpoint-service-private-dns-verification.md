# Resource: aws_vpc_endpoint_service_private_dns_verification

ytofu resource for managing an AWS VPC (Virtual Private Cloud) Endpoint Service Private DNS Verification.
This resource begins the verification process by calling the [`StartVpcEndpointServicePrivateDnsVerification`](https://docs.aws.amazon.com/AWSEC2/latest/APIReference/API_StartVpcEndpointServicePrivateDnsVerification.html) API.
The service provider should add a record to the DNS server _before_ creating this resource.

## Basic Example

```yaml
resource:
  aws_vpc_endpoint_service_private_dns_verification:
    example:
      service_id: ${aws_vpc_endpoint_service.example.id}
```

## Argument Reference

The following arguments are required:

* `service_id` - (Required) ID of the endpoint service.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `wait_for_verification` - (Optional) Whether to wait until the endpoint service returns a `Verified` status for the configured private DNS name.

## Attribute Reference

This resource exports no additional attributes.

## Timeouts

Configuration options:

* `create` - (Default `30m`)
