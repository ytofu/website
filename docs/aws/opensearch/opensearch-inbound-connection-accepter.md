# Resource: aws_opensearch_inbound_connection_accepter

Manages an [AWS Opensearch Inbound Connection Accepter](https://docs.aws.amazon.com/opensearch-service/latest/APIReference/API_AcceptInboundConnection.html). If connecting domains from different AWS accounts, ensure that the accepter is configured to use the AWS account where the _remote_ opensearch domain exists.

## Basic Example

```yaml
data:
  aws_caller_identity:
    current:

data:
  aws_region:
    current:

resource:
  aws_opensearch_outbound_connection:
    foo:
      connection_alias: outbound_connection
      local_domain_info:
        owner_id: ${data.aws_caller_identity.current.account_id}
        region: ${data.aws_region.current.region}
        domain_name: ${aws_opensearch_domain.local_domain.domain_name}
      remote_domain_info:
        owner_id: ${data.aws_caller_identity.current.account_id}
        region: ${data.aws_region.current.region}
        domain_name: ${aws_opensearch_domain.remote_domain.domain_name}

resource:
  aws_opensearch_inbound_connection_accepter:
    foo:
      connection_id: ${aws_opensearch_outbound_connection.foo.id}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `connection_id` - (Required, Forces new resource) Specifies the ID of the connection to accept.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The Id of the connection to accept.
* `connection_status` - Status of the connection request.

## Timeouts

Configuration options:

* `create` - (Default `5m`)
* `delete` - (Default `5m`)

## Import

```bash
ytofu import aws_opensearch_inbound_connection_accepter.foo connection-id
```
