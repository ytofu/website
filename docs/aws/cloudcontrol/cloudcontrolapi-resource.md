# Cloudcontrolapi Resource

Manage Cloudcontrolapi Resource resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_cloudcontrolapi_resource:
    example:
      type_name: "AWS::ECS::Cluster"
      desired_state: '{ "ClusterName": "example" "Tags": [ { "Key": "CostCenter" "Value": "IT" } ] }'
```
