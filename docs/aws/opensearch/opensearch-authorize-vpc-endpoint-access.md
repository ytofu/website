# Opensearch Authorize VPC Endpoint Access

Manage Opensearch Authorize VPC Endpoint Access resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_caller_identity:
    current:

resource:
  aws_opensearch_authorize_vpc_endpoint_access:
    test:
      domain_name: ${aws_opensearch_domain.test.domain_name}
      account: ${data.aws_caller_identity.current.account_id}
```
