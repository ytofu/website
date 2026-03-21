# Globalaccelerator Cross Account Attachment

Manage Globalaccelerator Cross Account Attachment resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_globalaccelerator_cross_account_attachment:
    example:
      name: example-cross-account-attachment
```

## Usage with Optional Arguments

```yaml
resource:
  aws_globalaccelerator_cross_account_attachment:
    example:
      name: example-cross-account-attachment
      principals: 
        - 123456789012
      resource:
        endpoint_id: "arn:aws:elasticloadbalancing:us-west-2:123456789012:loadbalancer/app/my-load-balancer/50dc6c495c0c9188"
        region: us-west-2
```
