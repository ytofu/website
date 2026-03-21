# Vpclattice Resource Policy

Manage Vpclattice Resource Policy resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_caller_identity:
    current:

data:
  aws_partition:
    current:

resource:
  aws_vpclattice_service_network:
    example:
      name: example-vpclattice-service-network

resource:
  aws_vpclattice_resource_policy:
    example:
      resource_arn: ${aws_vpclattice_service_network.example.arn}
      policy: '{ "Version": "2012-10-17", "Statement": [{ "Sid": "test-pol-principals-6" "Effect": "Allow" "Principal": { "AWS" = "arn:${data.aws_partition.current.partition}:iam::${data.aws_caller_identity.current.account_id}:root" } "Action": [ "vpc-lattice:CreateServiceNetworkVpcAssociation", "vpc-lattice:CreateServiceNetworkServiceAssociation", "vpc-lattice:GetServiceNetwork" ] "Resource": aws_vpclattice_service_network.example.arn }] }'
```
