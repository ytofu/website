# Resource: aws_vpclattice_resource_policy

ytofu resource for managing an AWS VPC Lattice Resource Policy.

## Basic Example

```yaml
data:
  aws_caller_identity:
    current:

  aws_partition:
    current:

resource:
  aws_vpclattice_service_network:
    example:
      name: example-vpclattice-service-network

  aws_vpclattice_resource_policy:
    example:
      resource_arn: ${aws_vpclattice_service_network.example.arn}
      policy: '{ "Version": "2012-10-17", "Statement": [{ "Sid": "test-pol-principals-6" "Effect": "Allow" "Principal": { "AWS" = "arn:${data.aws_partition.current.partition}:iam::${data.aws_caller_identity.current.account_id}:root" } "Action": [ "vpc-lattice:CreateServiceNetworkVpcAssociation", "vpc-lattice:CreateServiceNetworkServiceAssociation", "vpc-lattice:GetServiceNetwork" ] "Resource": aws_vpclattice_service_network.example.arn }] }'```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `resource_arn` - (Required) The ID or Amazon Resource Name (ARN) of the service network or service for which the policy is created.
* `policy` - (Required) An IAM policy. The policy string in JSON must not contain newlines or blank lines.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_vpclattice_resource_policy.example rft-8012925589
```
