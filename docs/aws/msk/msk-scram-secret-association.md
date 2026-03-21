# MSK Scram Secret Association

Manage MSK Scram Secret Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_msk_scram_secret_association:
    example:
      cluster_arn: ${aws_msk_cluster.example.arn}
      secret_arn_list: 
        - ${aws_secretsmanager_secret.example.arn}
      depends_on: 
        - ${aws_secretsmanager_secret_version.example}

resource:
  aws_msk_cluster:
    example:
      cluster_name: example
      client_authentication:
        sasl:
          scram: true

resource:
  aws_secretsmanager_secret:
    example:
      name: AmazonMSK_example
      kms_key_id: ${aws_kms_key.example.key_id}

resource:
  aws_kms_key:
    example:
      description: Example Key for MSK Cluster Scram Secret Association

resource:
  aws_secretsmanager_secret_version:
    example:
      secret_id: ${aws_secretsmanager_secret.example.id}
      secret_string: example-json-policy

data:
  aws_iam_policy_document:
    example:
      statement:
        sid: AWSKafkaResourcePolicy
        effect: Allow
        principals:
          type: Service
          identifiers: 
            - kafka.amazonaws.com
        actions: 
          - "secretsmanager:getSecretValue"
        resources: 
          - ${aws_secretsmanager_secret.example.arn}

resource:
  aws_secretsmanager_secret_policy:
    example:
      secret_arn: ${aws_secretsmanager_secret.example.arn}
      policy: ${data.aws_iam_policy_document.example.json}
```
