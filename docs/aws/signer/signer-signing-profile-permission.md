# Signer Signing Profile Permission

Manage Signer Signing Profile Permission resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_signer_signing_profile:
    prod_sp:
      platform_id: AWSLambda-SHA384-ECDSA
      name_prefix: prod_sp_
      signature_validity_period:
        value: 5
        type: YEARS
      tags:
        tag1: value1
        tag2: value2

resource:
  aws_signer_signing_profile_permission:
    sp_permission_1:
      profile_name: ${aws_signer_signing_profile.prod_sp.name}
      action: "signer:StartSigningJob"
      principal: example-aws_account

resource:
  aws_signer_signing_profile_permission:
    sp_permission_2:
      profile_name: ${aws_signer_signing_profile.prod_sp.name}
      action: "signer:GetSigningProfile"
      principal: example-aws_team_role_arn
      statement_id: ProdAccountStartSigningJob_StatementId

resource:
  aws_signer_signing_profile_permission:
    sp_permission_3:
      profile_name: ${aws_signer_signing_profile.prod_sp.name}
      action: "signer:RevokeSignature"
      principal: 123456789012
      profile_version: ${aws_signer_signing_profile.prod_sp.version}
      statement_id_prefix: version-permission-
```
