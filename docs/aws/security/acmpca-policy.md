# Acmpca Policy

Manage Acmpca Policy resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_iam_policy_document:
    example:
      statement:
        sid: 1
        effect: Allow
        principals:
          type: AWS
          identifiers: 
            - ${data.aws_caller_identity.current.account_id}
        actions:
          - "acm-pca:DescribeCertificateAuthority"
          - "acm-pca:GetCertificate"
          - "acm-pca:GetCertificateAuthorityCertificate"
          - "acm-pca:ListPermissions"
          - "acm-pca:ListTags"
        resources: 
          - ${aws_acmpca_certificate_authority.example.arn}
      statement:
        sid: 2
        effect: Allow
        principals:
          type: AWS
          identifiers: 
            - ${data.aws_caller_identity.current.account_id}
        actions: 
          - "acm-pca:IssueCertificate"
        resources: 
          - ${aws_acmpca_certificate_authority.example.arn}
        condition:
          test: StringEquals
          values: 
            - "arn:aws:acm-pca:::template/EndEntityCertificate/V1"

resource:
  aws_acmpca_policy:
    example:
      resource_arn: ${aws_acmpca_certificate_authority.example.arn}
      policy: ${data.aws_iam_policy_document.example.json}
```
