# Resource: aws_iam_outbound_web_identity_federation

Manages an AWS IAM (Identity & Access Management) Outbound Web Identity Federation.

## Basic Example

```yaml
resource:
  aws_iam_outbound_web_identity_federation:
    example:
```

## Argument Reference

This resource does not support any arguments.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `issuer_identifier` - A unique issuer URL for your AWS account that hosts the OpenID Connect (OIDC) discovery endpoints.

## Import

```bash
ytofu import aws_iam_outbound_web_identity_federation.example 123456789012
```
