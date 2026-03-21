# Opensearch Domain

Manage Opensearch Domain resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_opensearch_domain:
    example:
      domain_name: example
      engine_version: Elasticsearch_7.10
      cluster_config:
        instance_type: r4.large.search
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

data:
  aws_iam_policy_document:
    example:
      statement:
        effect: Allow
        principals:
          type: "*"
          identifiers: 
            - "*"
        actions: 
          - "es:*"
        resources: 
          - "arn:aws:es:${data.aws_region.current.region}:${data.aws_caller_identity.current.account_id}:domain/example-domain/*"
        condition:
          test: IpAddress
          values: 
            - 66.193.100.22/32

resource:
  aws_opensearch_domain:
    example:
      domain_name: example-domain
      access_policies: ${data.aws_iam_policy_document.example.json}
```

## Log publishing to CloudWatch Logs

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
  aws_opensearch_domain:
    example:
      log_publishing_options:
        cloudwatch_log_group_arn: ${aws_cloudwatch_log_group.example.arn}
        log_type: INDEX_SLOW_LOGS
```

## VPC based OpenSearch

```yaml
data:
  aws_vpc:
    example:
      tags:
        Name: example-vpc

data:
  aws_subnets:
    example:
      filter:
        name: vpc-id
        values: 
          - ${data.aws_vpc.example.id}
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
    example:
      name: "example-vpc-opensearch-example-domain"
      description: Managed by Terraform
      vpc_id: ${data.aws_vpc.example.id}
      ingress:
        from_port: 443
        to_port: 443
        protocol: tcp
        cidr_blocks:
          - ${data.aws_vpc.example.cidr_block}

resource:
  aws_iam_service_linked_role:
    example:
      aws_service_name: opensearchservice.amazonaws.com

data:
  aws_iam_policy_document:
    example:
      statement:
        effect: Allow
        principals:
          type: "*"
          identifiers: 
            - "*"
        actions: 
          - "es:*"
        resources: 
          - "arn:aws:es:${data.aws_region.current.region}:${data.aws_caller_identity.current.account_id}:domain/example-domain/*"

resource:
  aws_opensearch_domain:
    example:
      domain_name: example-domain
      engine_version: OpenSearch_1.0
      cluster_config:
        instance_type: m4.large.search
        zone_awareness_enabled: true
      vpc_options:
        subnet_ids:
          - ${data.aws_subnets.example.ids[0]}
          - ${data.aws_subnets.example.ids[1]}
        security_group_ids: 
          - ${aws_security_group.example.id}
      advanced_options: 
      access_policies: ${data.aws_iam_policy_document.example.json}
      tags:
        Domain: TestDomain
      depends_on: 
        - ${aws_iam_service_linked_role.example}
```

## Enabling fine-grained access control on an existing domain

```yaml
resource:
  aws_opensearch_domain:
    example:
      domain_name: ggkitty
      engine_version: Elasticsearch_7.1
      cluster_config:
        instance_type: r5.large.search
      advanced_security_options:
        enabled: false
        anonymous_auth_enabled: true
        internal_user_database_enabled: true
        master_user_options:
          master_user_name: example
          master_user_password: Barbarbarbar1!
      encrypt_at_rest:
        enabled: true
      domain_endpoint_options:
        enforce_https: true
        tls_security_policy: Policy-Min-TLS-1-2-2019-07
      node_to_node_encryption:
        enabled: true
      ebs_options:
        ebs_enabled: true
        volume_size: 10
```
