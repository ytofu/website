# Workspacesweb Trust Store

Manage Workspacesweb Trust Store resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_workspacesweb_trust_store:
    example:
      certificate:
        body: file-content
```

## Multiple Certificates

```yaml
resource:
  aws_workspacesweb_trust_store:
    example:
      certificate:
        body: file-content
      certificate:
        body: file-content
      tags:
        Name: example-trust-store
```
