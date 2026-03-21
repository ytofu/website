# Resource: aws_transfer_ssh_key

Provides a AWS Transfer User SSH Key resource.

## Basic Example

```yaml
resource:
  tls_private_key:
    example:
      algorithm: RSA
      rsa_bits: 4096

  aws_transfer_ssh_key:
    example:
      server_id: ${aws_transfer_server.example.id}
      user_name: ${aws_transfer_user.example.user_name}
      body: ${trimspace(tls_private_key.example.public_key_openssh)}

  aws_transfer_server:
    example:
      identity_provider_type: SERVICE_MANAGED
      tags:
        NAME: tf-acc-test-transfer-server

  aws_transfer_user:
    example:
      server_id: ${aws_transfer_server.example.id}
      user_name: tftestuser
      role: ${aws_iam_role.example.arn}
      tags:
        NAME: tftestuser

  aws_iam_role:
    example:
      name: tf-test-transfer-user-iam-role
      assume_role_policy: ${data.aws_iam_policy_document.assume_role.json}

  aws_iam_role_policy:
    example:
      name: tf-test-transfer-user-iam-policy
      role: ${aws_iam_role.example.id}
      policy: ${data.aws_iam_policy_document.example.json}

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

  aws_iam_policy_document:
    example:
      statement:
        sid: AllowFullAccesstoS3
        effect: Allow
        actions: 
          - "s3:*"
        resources: 
          - "*"```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `server_id` - (Requirement) The Server ID of the Transfer Server (e.g., `s-12345678`)
* `user_name` - (Requirement) The name of the user account that is assigned to one or more servers.
* `body` - (Requirement) The public key portion of an SSH key pair.

## Attribute Reference

This resource exports no additional attributes.

## Import

```bash
ytofu import aws_transfer_ssh_key.bar s-12345678/test-username/key-12345
```
