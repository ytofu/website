# Datasync Location Smb

Manage Datasync Location Smb resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_datasync_location_smb:
    example:
      server_hostname: smb.example.com
      subdirectory: /exported/path
      user: Guest
      password: ANotGreatPassword
      agent_arns: 
        - ${aws_datasync_agent.example.arn}
```
