# Directory Service Region

Manage Directory Service Region resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_region:
    example:

data:
  aws_availability_zones:
    available:
      state: available
      filter:
        name: opt-in-status
        values: 
          - opt-in-not-required

resource:
  aws_vpc:
    example:
      cidr_block: 10.0.0.0/16
      tags:
        Name: Primary

resource:
  aws_subnet:
    example:
      vpc_id: ${aws_vpc.example.id}
      availability_zone: ${data.aws_availability_zones.available.names[count.index]}
      cidr_block: 10.0.1.0/24
      tags:
        Name: Primary

resource:
  aws_directory_service_directory:
    example:
      name: example.com
      password: SuperSecretPassw0rd
      type: MicrosoftAD
      vpc_settings:
        vpc_id: ${aws_vpc.example.id}
        subnet_ids: ${aws_subnet.example[*].id}

data:
  aws_availability_zones:
    available-secondary:
      state: available
      filter:
        name: opt-in-status
        values: 
          - opt-in-not-required

resource:
  aws_vpc:
    example-secondary:
      cidr_block: "10.1.0.0/16" # Can't overlap with primary's VPC.
      tags:
        Name: Secondary

resource:
  aws_subnet:
    example-secondary:
      vpc_id: ${aws_vpc.example-secondary.id}
      availability_zone: ${data.aws_availability_zones.available-secondary.names[count.index]}
      cidr_block: 10.0.1.0/24
      tags:
        Name: Secondary

resource:
  aws_directory_service_region:
    example:
      directory_id: ${aws_directory_service_directory.example.id}
      region_name: ${data.aws_region.example.name}
      vpc_settings:
        vpc_id: ${aws_vpc.example-secondary.id}
        subnet_ids: ${aws_subnet.example-secondary[*].id}
      tags:
        Name: Secondary
```
