# Signer Signing Job

Manage Signer Signing Job resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_signer_signing_profile:
    test_sp:
      platform_id: AWSLambda-SHA384-ECDSA

resource:
  aws_signer_signing_job:
    build_signing_job:
      profile_name: ${aws_signer_signing_profile.test_sp.name}
      source:
        s3:
          bucket: s3-bucket-name
          key: object-to-be-signed.zip
          version: jADjFYYYEXAMPLETszPjOmCMFDzd9dN1
      destination:
        s3:
          bucket: s3-bucket-name
          prefix: signed/
      ignore_signing_job_failure: true
```
