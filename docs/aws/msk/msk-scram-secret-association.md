# Resource: aws_msk_scram_secret_association

Associates SCRAM secrets stored in the Secrets Manager service with a Managed Streaming for Kafka (MSK) cluster.

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

  aws_msk_cluster:
    example:
      cluster_name: example
      client_authentication:
        sasl:
          scram: true

  aws_secretsmanager_secret:
    example:
      name: AmazonMSK_example
      kms_key_id: ${aws_kms_key.example.key_id}

  aws_kms_key:
    example:
      description: Example Key for MSK Cluster Scram Secret Association

  aws_secretsmanager_secret_version:
    example:
      secret_id: ${aws_secretsmanager_secret.example.id}
      secret_string: example-json-policy

  aws_secretsmanager_secret_policy:
    example:
      secret_arn: ${aws_secretsmanager_secret.example.arn}
      policy: ${data.aws_iam_policy_document.example.json}

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
          - ${aws_secretsmanager_secret.example.arn}```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `cluster_arn` - (Required, Forces new resource) Amazon Resource Name (ARN) of the MSK cluster.
* `secret_arn_list` - (Required) List of AWS Secrets Manager secret ARNs.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Amazon Resource Name (ARN) of the MSK cluster.

## Import

```bash
ytofu import aws_msk_scram_secret_association.example arn:aws:kafka:us-west-2:123456789012:cluster/example/279c0212-d057-4dba-9aa9-1c4e5a25bfc7-3
```
