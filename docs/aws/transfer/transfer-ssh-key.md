# Transfer Ssh Key

Manage Transfer Ssh Key resources using ytofu YAML.

## Basic Example

```yaml
resource:
  tls_private_key:
    example:
      algorithm: RSA
      rsa_bits: 4096

resource:
  aws_transfer_ssh_key:
    example:
      server_id: ${aws_transfer_server.example.id}
      user_name: ${aws_transfer_user.example.user_name}
      body: ${trimspace(tls_private_key.example.public_key_openssh)}

resource:
  aws_transfer_server:
    example:
      identity_provider_type: SERVICE_MANAGED
      tags:
        NAME: tf-acc-test-transfer-server

resource:
  aws_transfer_user:
    example:
      server_id: ${aws_transfer_server.example.id}
      user_name: tftestuser
      role: ${aws_iam_role.example.arn}
      tags:
        NAME: tftestuser

data:
  aws_iam_policy_document:
    assume_role:
      statement:
        effect: Allow
        principals:
          type: Service
          identifiers: 
            - transfer.amazonaws.com
        actions: 
          - "sts:AssumeRole"

resource:
  aws_iam_role:
    example:
      name: tf-test-transfer-user-iam-role
      assume_role_policy: ${data.aws_iam_policy_document.assume_role.json}

data:
  aws_iam_policy_document:
    example:
      statement:
        sid: AllowFullAccesstoS3
        effect: Allow
        actions: 
          - "s3:*"
        resources: 
          - "*"

resource:
  aws_iam_role_policy:
    example:
      name: tf-test-transfer-user-iam-policy
      role: ${aws_iam_role.example.id}
      policy: ${data.aws_iam_policy_document.example.json}
```
