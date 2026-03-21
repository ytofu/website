# Resource: aws_msk_serverless_cluster

Manages an Amazon MSK Serverless cluster.

## Basic Example

```yaml
resource:
  aws_msk_serverless_cluster:
    example:
      cluster_name: Example
      vpc_config:
        subnet_ids: ${aws_subnet.example[*].id}
        security_group_ids: 
          - ${aws_security_group.example.id}
      client_authentication:
        sasl:
          iam:
            enabled: true
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `client_authentication` - (Required) Specifies client authentication information for the serverless cluster. See below.
* `cluster_name` - (Required) The name of the serverless cluster.
* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.
* `vpc_config` - (Required) VPC configuration information. See below.

### client_authentication Argument Reference

* `sasl` - (Required) Details for client authentication using SASL. See below.

### sasl Argument Reference

* `iam` - (Required) Details for client authentication using IAM. See below.

### iam Argument Reference

* `enabled` - (Required) Whether SASL/IAM authentication is enabled or not.

### vpc_config Argument Reference

* `security_group_ids` - (Optional) Specifies up to five security groups that control inbound and outbound traffic for the serverless cluster.
* `subnet_ids` - (Required) A list of subnets in at least two different Availability Zones that host your client applications.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - The ARN of the serverless cluster.
* `bootstrap_brokers_sasl_iam` - One or more DNS names (or IP addresses) and SASL IAM port pairs. For example, `boot-abcdefg.c2.kafka-serverless.eu-central-1.amazonaws.com:9098`. The resource sorts the list alphabetically. AWS may not always return all endpoints so the values may not be stable across applies.
* `cluster_uuid` - UUID of the serverless cluster, for use in IAM policies.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Timeouts

Configuration options:

* `create` - (Default `120m`)
* `delete` - (Default `120m`)

## Import

```bash
ytofu import aws_msk_serverless_cluster.example arn:aws:kafka:us-west-2:123456789012:cluster/example/279c0212-d057-4dba-9aa9-1c4e5a25bfc7-3
```
