# OpenSearch Domain

Create and manage OpenSearch domains using ytofu YAML.

## Basic Domain

```yaml
resource:
  aws_opensearch_domain:
    example:
      domain_name: example
      engine_version: OpenSearch_2.11
      cluster_config:
        instance_type: r6g.large.search
      ebs_options:
        ebs_enabled: true
        volume_size: 10
      tags:
        Domain: TestDomain
```

## With VPC

```yaml
resource:
  aws_opensearch_domain:
    example:
      domain_name: example
      engine_version: OpenSearch_2.11
      cluster_config:
        instance_type: r6g.large.search
        instance_count: 2
        zone_awareness_enabled: true
      vpc_options:
        subnet_ids:
          - ${aws_subnet.private_a.id}
          - ${aws_subnet.private_b.id}
        security_group_ids:
          - ${aws_security_group.opensearch.id}
      ebs_options:
        ebs_enabled: true
        volume_size: 20
        volume_type: gp3
```

## With Encryption

```yaml
resource:
  aws_opensearch_domain:
    example:
      domain_name: example
      engine_version: OpenSearch_2.11
      cluster_config:
        instance_type: r6g.large.search
      encrypt_at_rest:
        enabled: true
        kms_key_id: ${aws_kms_key.example.key_id}
      node_to_node_encryption:
        enabled: true
      domain_endpoint_options:
        enforce_https: true
        tls_security_policy: Policy-Min-TLS-1-2-PFS-2023-10
      ebs_options:
        ebs_enabled: true
        volume_size: 10
```

## With Access Policy

```yaml
resource:
  aws_opensearch_domain:
    example:
      domain_name: example
      engine_version: OpenSearch_2.11
      cluster_config:
        instance_type: r6g.large.search
      access_policies: ${data.aws_iam_policy_document.example.json}
      ebs_options:
        ebs_enabled: true
        volume_size: 10

  aws_opensearch_domain_policy:
    example:
      domain_name: ${aws_opensearch_domain.example.domain_name}
      access_policies: ${data.aws_iam_policy_document.example.json}
```

## With Auto-Tune

```yaml
resource:
  aws_opensearch_domain:
    example:
      domain_name: example
      engine_version: OpenSearch_2.11
      cluster_config:
        instance_type: r6g.large.search
      auto_tune_options:
        desired_state: ENABLED
        rollback_on_disable: NO_ROLLBACK
        maintenance_schedule:
          - start_at: 2027-01-01T01:00:00Z
            duration:
              value: 2
              unit: HOURS
            cron_expression_for_recurrence: cron(0 1 ? * MON *)
      ebs_options:
        ebs_enabled: true
        volume_size: 10
```
