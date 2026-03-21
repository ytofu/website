# Appstream Directory Config

Manage Appstream Directory Config resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_appstream_directory_config:
    example:
      directory_name: NAME OF DIRECTORY
      organizational_unit_distinguished_names: 
        - DISTINGUISHED NAME
      service_account_credentials:
        account_name: NAME OF ACCOUNT
        account_password: PASSWORD OF ACCOUNT
      certificate_based_auth_properties:
        certificate_authority_arn: ARN OF CERTIFICATE AUTHORITY
        status: STATUS OF CERTIFICATE BASED AUTHENTICATION
```
