# Resource: aws_vpc_endpoint_connection_accepter

Provides a resource to accept a pending VPC Endpoint Connection accept request to VPC Endpoint Service.

## Basic Example

```yaml
resource:
  aws_vpc_endpoint_service:
    example:
      acceptance_required: false
      network_load_balancer_arns: 
        - ${aws_lb.example.arn}

resource:
  aws_vpc_endpoint:
    example:
      vpc_id: ${aws_vpc.test_alternate.id}
      service_name: ${aws_vpc_endpoint_service.test.service_name}
      vpc_endpoint_type: Interface
      private_dns_enabled: false
      security_group_ids:
        - ${aws_security_group.test.id}

resource:
  aws_vpc_endpoint_connection_accepter:
    example:
      vpc_endpoint_service_id: ${aws_vpc_endpoint_service.example.id}
      vpc_endpoint_id: ${aws_vpc_endpoint.example.id}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `vpc_endpoint_id` - (Required) AWS VPC Endpoint ID.
* `vpc_endpoint_service_id` - (Required) AWS VPC Endpoint Service ID.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The ID of the VPC Endpoint Connection.
* `vpc_endpoint_state` - State of the VPC Endpoint.

## Import

```bash
ytofu import aws_vpc_endpoint_connection_accepter.foo vpce-svc-0f97a19d3fa8220bc_vpce-010601a6db371e263
```
