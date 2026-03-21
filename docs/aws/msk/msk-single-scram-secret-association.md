# Resource: aws_msk_single_scram_secret_association

Associates a single SCRAM secret with a Managed Streaming for Kafka (MSK) cluster.

## Basic Example

```yaml
resource:
  aws_msk_single_scram_secret_association:
    example:
      cluster_arn: ${aws_msk_cluster.example.arn}
      secret_arn: ${aws_secretsmanager_secret.example.arn}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `cluster_arn` - (Required, Forces new resource) Amazon Resource Name (ARN) of the MSK cluster.
* `secret_arn` -  (Required, Forces new resource) AWS Secrets Manager secret ARN.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_msk_single_scram_secret_association.example arn:aws:kafka:us-west-2:123456789012:cluster/example/279c0212-d057-4dba-9aa9-1c4e5a25bfc7-3,arn:aws:secretsmanager:us-east-1:123456789012:secret:example-123456
```
