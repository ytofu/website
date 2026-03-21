# Directory Service Shared Directory

Manage Directory Service Shared Directory resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_directory_service_directory:
    example:
      name: tf-example
      password: SuperSecretPassw0rd
      type: MicrosoftAD
      edition: Standard
      vpc_settings:
        vpc_id: ${aws_vpc.example.id}
        subnet_ids: ${aws_subnet.example[*].id}

resource:
  aws_directory_service_shared_directory:
    example:
      directory_id: ${aws_directory_service_directory.example.id}
      notes: You wanna have a catch?
      target:
        id: ${data.aws_caller_identity.receiver.account_id}
```
