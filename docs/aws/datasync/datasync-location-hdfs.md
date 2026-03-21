# Datasync Location Hdfs

Manage Datasync Location Hdfs resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_datasync_location_hdfs:
    example:
      agent_arns: 
        - ${aws_datasync_agent.example.arn}
      authentication_type: SIMPLE
      simple_user: example
      name_node:
        hostname: ${aws_instance.example.private_dns}
        port: 80
```

## Kerberos Authentication

```yaml
resource:
  aws_datasync_location_hdfs:
    example:
      agent_arns: 
        - ${aws_datasync_agent.example.arn}
      authentication_type: KERBEROS
      name_node:
        hostname: ${aws_instance.example.private_dns}
        port: 80
      kerberos_principal: user@example.com
      kerberos_keytab_base64: example-value
      kerberos_krb5_conf: file-content
```
