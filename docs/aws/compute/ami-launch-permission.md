# AMI Launch Permission

Manage AMI Launch Permission resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ami_launch_permission:
    example:
      image_id: ami-12345678
      account_id: 123456789012
```

## Public Access

```yaml
resource:
  aws_ami_launch_permission:
    example:
      image_id: ami-12345678
      group: all
```

## Organization Access

```yaml
data:
  aws_organizations_organization:
    current:

resource:
  aws_ami_launch_permission:
    example:
      image_id: ami-12345678
      organization_arn: ${data.aws_organizations_organization.current.arn}
```
