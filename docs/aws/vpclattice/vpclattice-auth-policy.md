# Vpclattice Auth Policy

Manage Vpclattice Auth Policy resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_vpclattice_service:
    example:
      name: example-vpclattice-service
      auth_type: AWS_IAM
      custom_domain_name: example.com

resource:
  aws_vpclattice_auth_policy:
    example:
      resource_identifier: ${aws_vpclattice_service.example.arn}
      policy: '{ "Version": "2012-10-17" "Statement": [ { "Action": "*" "Effect": "Allow" "Principal": "*" "Resource": "*" "Condition": { "StringNotEqualsIgnoreCase": { "aws:PrincipalType" = "anonymous" } } } ] }'
```
