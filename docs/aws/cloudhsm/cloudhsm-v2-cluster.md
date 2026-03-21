# Cloudhsm V2 Cluster

Manage Cloudhsm V2 Cluster resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_availability_zones:
    available:

resource:
  aws_vpc:
    cloudhsm_v2_vpc:
      cidr_block: 10.0.0.0/16
      tags:
        Name: example-aws_cloudhsm_v2_cluster

resource:
  aws_subnet:
    cloudhsm_v2_subnets:
      vpc_id: ${aws_vpc.cloudhsm_v2_vpc.id}
      cidr_block: element-value
      map_public_ip_on_launch: false
      availability_zone: element-value
      tags:
        Name: example-aws_cloudhsm_v2_cluster

resource:
  aws_cloudhsm_v2_cluster:
    cloudhsm_v2_cluster:
      hsm_type: hsm1.medium
      subnet_ids: ${aws_subnet.cloudhsm_v2_subnets[*].id}
      tags:
        Name: example-aws_cloudhsm_v2_cluster
```
