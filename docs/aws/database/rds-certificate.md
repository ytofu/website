# Resource: aws_rds_certificate

Provides a resource to override the system-default Secure Sockets Layer/Transport Layer Security (SSL/TLS) certificate for Amazon RDS for new DB instances in the current AWS region.

## Basic Example

```yaml
resource:
  aws_rds_certificate:
    example:
      certificate_identifier: rds-ca-rsa4096-g1
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `certificate_identifier` - (Required) Certificate identifier. For example, `rds-ca-rsa4096-g1`. Refer to [AWS RDS (Relational Database) Certificate Identifier](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/UsingWithRDS.SSL.html#UsingWithRDS.SSL.CertificateIdentifier) for more information.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_rds_certificate.example us-west-2
```
