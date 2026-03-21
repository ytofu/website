# Timestreaminfluxdb DB Cluster

Manage Timestreaminfluxdb DB Cluster resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_timestreaminfluxdb_db_cluster:
    example:
      allocated_storage: 20
      bucket: example-bucket-name
      db_instance_type: db.influx.medium
      failover_mode: AUTOMATIC
      username: admin
      password: example-password
      port: 8086
      organization: organization
      vpc_subnet_ids: 
        - ${aws_subnet.example_1.id}
        - ${aws_subnet.example_2.id}
      vpc_security_group_ids: 
        - ${aws_security_group.example.id}
      name: example-db-cluster
```

## Usage with Prerequisite Resources

```yaml
resource:
  aws_vpc:
    example:
      cidr_block: 10.0.0.0/16

resource:
  aws_subnet:
    example_1:
      vpc_id: ${aws_vpc.example.id}
      cidr_block: 10.0.1.0/24

resource:
  aws_subnet:
    example_2:
      vpc_id: ${aws_vpc.example.id}
      cidr_block: 10.0.2.0/24

resource:
  aws_security_group:
    example:
      name: example
      vpc_id: ${aws_vpc.example.id}

resource:
  aws_timestreaminfluxdb_db_cluster:
    example:
      allocated_storage: 20
      bucket: example-bucket-name
      db_instance_type: db.influx.medium
      username: admin
      password: example-password
      organization: organization
      vpc_subnet_ids: 
        - ${aws_subnet.example_1.id}
        - ${aws_subnet.example_2.id}
      vpc_security_group_ids: 
        - ${aws_security_group.example.id}
      name: example-db-cluster
```

## Usage with Public Internet Access Enabled

```yaml
resource:
  aws_vpc:
    example:
      cidr_block: 10.0.0.0/16

resource:
  aws_subnet:
    example_1:
      vpc_id: ${aws_vpc.example.id}
      cidr_block: 10.0.1.0/24

resource:
  aws_subnet:
    example_2:
      vpc_id: ${aws_vpc.example.id}
      cidr_block: 10.0.2.0/24

resource:
  aws_security_group:
    example:
      name: example
      vpc_id: ${aws_vpc.example.id}

resource:
  aws_internet_gateway:
    example:
      vpc_id: ${aws_vpc.example.id}
      tags:
        Name: example

resource:
  aws_route:
    test_route:
      route_table_id: ${aws_vpc.example.main_route_table_id}
      destination_cidr_block: 0.0.0.0/0
      gateway_id: ${aws_internet_gateway.example.id}

resource:
  aws_route_table_association:
    test_route_table_association:
      subnet_id: ${aws_subnet.test_subnet.id}
      route_table_id: ${aws_vpc.example.main_route_table_id}

resource:
  aws_vpc_security_group_ingress_rule:
    example:
      security_group_id: ${aws_security_group.example.id}
      referenced_security_group_id: ${aws_security_group.example.id}
      ip_protocol: -1

resource:
  aws_vpc_security_group_ingress_rule:
    example:
      security_group_id: ${aws_security_group.example.id}
      cidr_ipv4: 0.0.0.0/0
      ip_protocol: tcp
      from_port: 8086
      to_port: 8086

resource:
  aws_timestreaminfluxdb_db_cluster:
    example:
      allocated_storage: 20
      bucket: example-bucket-name
      db_instance_type: db.influx.medium
      username: admin
      password: example-password
      organization: organization
      vpc_subnet_ids: 
        - ${aws_subnet.example_1.id}
        - ${aws_subnet.example_2.id}
      vpc_security_group_ids: 
        - ${aws_security_group.example.id}
      name: example-db-cluster
      publicly_accessible: true
```

## Usage with S3 Log Delivery Enabled

```yaml
resource:
  aws_s3_bucket:
    example:
      bucket: example-s3-bucket
      force_destroy: true

data:
  aws_iam_policy_document:
    example:
      statement:
        actions: 
          - "s3:PutObject"
        principals:
          type: Service
          identifiers: 
            - timestream-influxdb.amazonaws.com
        resources:
          - "${aws_s3_bucket.example.arn}/*"

resource:
  aws_s3_bucket_policy:
    example:
      bucket: ${aws_s3_bucket.example.id}
      policy: ${data.aws_iam_policy_document.example.json}

resource:
  aws_timestreaminfluxdb_db_cluster:
    example:
      allocated_storage: 20
      bucket: example-bucket-name
      db_instance_type: db.influx.medium
      username: admin
      password: example-password
      organization: organization
      vpc_subnet_ids: 
        - ${aws_subnet.example_1.id}
        - ${aws_subnet.example_2.id}
      vpc_security_group_ids: 
        - ${aws_security_group.example.id}
      name: example-db-cluster
      log_delivery_configuration:
        s3_configuration:
          bucket_name: ${aws_s3_bucket.example.bucket}
          enabled: true
```

## Usage with InfluxDB V3

```yaml
resource:
  aws_timestreaminfluxdb_db_cluster:
    example:
      name: example-v3-cluster
      db_instance_type: db.influx.large
      db_parameter_group_identifier: InfluxDBV3Core
      vpc_subnet_ids: 
        - ${aws_subnet.example_1.id}
        - ${aws_subnet.example_2.id}
      vpc_security_group_ids: 
        - ${aws_security_group.example.id}
```
