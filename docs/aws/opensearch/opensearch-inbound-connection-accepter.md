# Opensearch Inbound Connection Accepter

Manage Opensearch Inbound Connection Accepter resources using ytofu YAML.

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
