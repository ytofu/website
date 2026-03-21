# Licensemanager Grant

Manage Licensemanager Grant resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_licensemanager_grant:
    test:
      name: share-license-with-account
      allowed_operations:
        - ListPurchasedLicenses
        - CheckoutLicense
        - CheckInLicense
        - ExtendConsumptionLicense
        - CreateToken
      license_arn: "arn:aws:license-manager::111111111111:license:l-exampleARN"
      principal: "arn:aws:iam::111111111112:root"
      home_region: us-east-1
```
