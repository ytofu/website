# Lambda Code Signing Config

Manage Lambda Code Signing Config resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_signer_signing_profile:
    prod:
      platform_id: AWSLambda-SHA384-ECDSA
      name_prefix: prod_lambda_
      tags:
        Environment: production

resource:
  aws_signer_signing_profile:
    dev:
      platform_id: AWSLambda-SHA384-ECDSA
      name_prefix: dev_lambda_
      tags:
        Environment: development

resource:
  aws_lambda_code_signing_config:
    example:
      description: Code signing configuration for Lambda functions
      allowed_publishers:
        signing_profile_version_arns:
          - ${aws_signer_signing_profile.prod.version_arn}
          - ${aws_signer_signing_profile.dev.version_arn}
      policies:
        untrusted_artifact_on_deployment: "Enforce" # Block deployments that fail code signing validation
      tags:
        Environment: production
        Purpose: code-signing
```

## Warning Only Configuration

```yaml
resource:
  aws_lambda_code_signing_config:
    example:
      description: Development code signing configuration
      allowed_publishers:
        signing_profile_version_arns:
          - ${aws_signer_signing_profile.dev.version_arn}
      policies:
        untrusted_artifact_on_deployment: "Warn" # Allow deployments but log validation failures
      tags:
        Environment: development
        Purpose: code-signing
```

## Multiple Environment Configuration

```yaml
resource:
  aws_lambda_code_signing_config:
    prod:
      description: Production code signing configuration with strict enforcement
      allowed_publishers:
        signing_profile_version_arns:
          - ${aws_signer_signing_profile.prod.version_arn}
      policies:
        untrusted_artifact_on_deployment: Enforce
      tags:
        Environment: production
        Security: strict

resource:
  aws_lambda_code_signing_config:
    dev:
      description: Development code signing configuration with warnings
      allowed_publishers:
        signing_profile_version_arns:
          - ${aws_signer_signing_profile.dev.version_arn}
          - ${aws_signer_signing_profile.test.version_arn}
      policies:
        untrusted_artifact_on_deployment: Warn
      tags:
        Environment: development
        Security: flexible
```
