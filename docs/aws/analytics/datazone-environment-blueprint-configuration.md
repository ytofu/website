# Datazone Environment Blueprint Configuration

Manage Datazone Environment Blueprint Configuration resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_datazone_domain:
    example:
      name: example_domain
      domain_execution_role: ${aws_iam_role.domain_execution_role.arn}

data:
  aws_datazone_environment_blueprint:
    default_data_lake:
      domain_id: ${aws_datazone_domain.example.id}
      name: DefaultDataLake
      managed: true

resource:
  aws_datazone_environment_blueprint_configuration:
    example:
      domain_id: ${aws_datazone_domain.example.id}
      environment_blueprint_id: ${data.aws_datazone_environment_blueprint.default_data_lake.id}
      enabled_regions: 
        - us-east-1
      regional_parameters:
        us-east-1: 
          S3Location: "s3://my-amazon-datazone-bucket"
```
