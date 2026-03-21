# Directory Service Trust

Manage Directory Service Trust resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_directory_service_trust:
    one:
      directory_id: ${aws_directory_service_directory.one.id}
      remote_domain_name: ${aws_directory_service_directory.two.name}
      trust_direction: Two-Way
      trust_password: Some0therPassword
      conditional_forwarder_ip_addrs: ${aws_directory_service_directory.two.dns_ip_addresses}

resource:
  aws_directory_service_trust:
    two:
      directory_id: ${aws_directory_service_directory.two.id}
      remote_domain_name: ${aws_directory_service_directory.one.name}
      trust_direction: Two-Way
      trust_password: Some0therPassword
      conditional_forwarder_ip_addrs: ${aws_directory_service_directory.one.dns_ip_addresses}

resource:
  aws_directory_service_directory:
    one:
      name: one.example.com
      type: MicrosoftAD

resource:
  aws_directory_service_directory:
    two:
      name: two.example.com
      type: MicrosoftAD
```

## One-Way Trust

```yaml
resource:
  aws_directory_service_trust:
    one:
      directory_id: ${aws_directory_service_directory.one.id}
      remote_domain_name: ${aws_directory_service_directory.two.name}
      trust_direction: "One-Way: Incoming"
      trust_password: Some0therPassword
      conditional_forwarder_ip_addrs: ${aws_directory_service_directory.two.dns_ip_addresses}

resource:
  aws_directory_service_trust:
    two:
      directory_id: ${aws_directory_service_directory.two.id}
      remote_domain_name: ${aws_directory_service_directory.one.name}
      trust_direction: "One-Way: Outgoing"
      trust_password: Some0therPassword
      conditional_forwarder_ip_addrs: ${aws_directory_service_directory.one.dns_ip_addresses}

resource:
  aws_directory_service_directory:
    one:
      name: one.example.com
      type: MicrosoftAD

resource:
  aws_directory_service_directory:
    two:
      name: two.example.com
      type: MicrosoftAD
```
