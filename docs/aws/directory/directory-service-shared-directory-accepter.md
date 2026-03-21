# Directory Service Shared Directory Accepter

Manage Directory Service Shared Directory Accepter resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_directory_service_shared_directory:
    example:
      directory_id: ${aws_directory_service_directory.example.id}
      notes: example
      target:
        id: ${data.aws_caller_identity.receiver.account_id}

resource:
  aws_directory_service_shared_directory_accepter:
    example:
      shared_directory_id: ${aws_directory_service_shared_directory.example.shared_directory_id}
```
