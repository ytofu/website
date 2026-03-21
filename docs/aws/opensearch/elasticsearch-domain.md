# Elasticsearch Domain

Manage Elasticsearch Domain resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_elasticsearch_domain:
    example:
      domain_name: example
      elasticsearch_version: 7.10
      cluster_config:
        instance_type: r4.large.elasticsearch
      tags:
        Domain: TestDomain
```

## Access Policy

```yaml
data:
  aws_region:
    current:

data:
  aws_caller_identity:
    current:

resource:
  aws_elasticsearch_domain:
    example:
      domain_name: example-domain
      access_policies: |
        {
        "Version": "2012-10-17",
        "Statement": [
        {
        "Action": "es:*",
        "Principal": "*",
        "Effect": "Allow",
        "Resource": "arn:aws:es:${data.aws_region.current.region}:${data.aws_caller_identity.current.account_id}:domain/example-domain/*",
        "Condition": {
        "IpAddress": {"aws:SourceIp": ["66.193.100.22/32"]}
        }
        }
        ]
        }
```

## Log Publishing to CloudWatch Logs

```yaml
resource:
  aws_cloudwatch_log_group:
    example:
      name: example

data:
  aws_iam_policy_document:
    example:
      statement:
        effect: Allow
        principals:
          type: Service
          identifiers: 
            - es.amazonaws.com
        actions:
          - "logs:PutLogEvents"
          - "logs:PutLogEventsBatch"
          - "logs:CreateLogStream"
        resources: 
          - "arn:aws:logs:*"

resource:
  aws_cloudwatch_log_resource_policy:
    example:
      policy_name: example
      policy_document: ${data.aws_iam_policy_document.example.json}

resource:
  aws_elasticsearch_domain:
    example:
      log_publishing_options:
        cloudwatch_log_group_arn: ${aws_cloudwatch_log_group.example.arn}
        log_type: INDEX_SLOW_LOGS
```

## VPC based ES

```yaml
data:
  aws_vpc:
    selected:
      tags:
        Name: example-vpc

data:
  aws_subnets:
    selected:
      filter:
        name: vpc-id
        values: 
          - ${data.aws_vpc.selected.id}
      tags:
        Tier: private

data:
  aws_region:
    current:

data:
  aws_caller_identity:
    current:

resource:
  aws_security_group:
    es:
      name: "example-vpc-elasticsearch-example-domain"
      description: Managed by Terraform
      vpc_id: ${data.aws_vpc.selected.id}
      ingress:
        from_port: 443
        to_port: 443
        protocol: tcp
        cidr_blocks:
          - ${data.aws_vpc.selected.cidr_block}

resource:
  aws_iam_service_linked_role:
    es:
      aws_service_name: opensearchservice.amazonaws.com

resource:
  aws_elasticsearch_domain:
    es:
      domain_name: example-domain
      elasticsearch_version: 6.3
      cluster_config:
        instance_type: m4.large.elasticsearch
        zone_awareness_enabled: true
      vpc_options:
        subnet_ids:
          - ${data.aws_subnets.selected.ids[0]}
          - ${data.aws_subnets.selected.ids[1]}
        security_group_ids: 
          - ${aws_security_group.es.id}
      advanced_options: 
      access_policies: |
        {
        "Version": "2012-10-17",
        "Statement": [
        {
        "Action": "es:*",
        "Principal": "*",
        "Effect": "Allow",
        "Resource": "arn:aws:es:${data.aws_region.current.region}:${data.aws_caller_identity.current.account_id}:domain/example-domain/*"
        }
        ]
        }
      tags:
        Domain: TestDomain
      depends_on: 
        - ${aws_iam_service_linked_role.es}
```
