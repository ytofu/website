# Transfer SSH Key

Add SSH public keys to Transfer users using ytofu YAML.

## Basic SSH Key

```yaml
resource:
  aws_transfer_ssh_key:
    example:
      server_id: ${aws_transfer_server.example.id}
      user_name: ${aws_transfer_user.example.user_name}
      body: ssh-rsa AAAAB3NzaC1yc2E... user@example.com
```
