# Apprunner Service

Manage Apprunner Service resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_apprunner_service:
    example:
      service_name: example
      source_configuration:
        authentication_configuration:
          connection_arn: ${aws_apprunner_connection.example.arn}
        code_repository:
          code_configuration:
            code_configuration_values:
              build_command: python setup.py develop
              port: 8000
              runtime: PYTHON_3
              start_command: python runapp.py
            configuration_source: API
          repository_url: "https://github.com/example/my-example-python-app"
          source_code_version:
            type: BRANCH
            value: main
      network_configuration:
        egress_configuration:
          egress_type: VPC
          vpc_connector_arn: ${aws_apprunner_vpc_connector.connector.arn}
      tags:
        Name: example-apprunner-service
```

## Service with an Image Repository Source

```yaml
resource:
  aws_apprunner_service:
    example:
      service_name: example
      source_configuration:
        image_repository:
          image_configuration:
            port: 8000
          image_identifier: "public.ecr.aws/aws-containers/hello-app-runner:latest"
          image_repository_type: ECR_PUBLIC
        auto_deployments_enabled: false
      tags:
        Name: example-apprunner-service
```

## Service with Observability Configuration

```yaml
resource:
  aws_apprunner_service:
    example:
      service_name: example
      observability_configuration:
        observability_configuration_arn: ${aws_apprunner_observability_configuration.example.arn}
        observability_enabled: true
      source_configuration:
        image_repository:
          image_configuration:
            port: 8000
          image_identifier: "public.ecr.aws/aws-containers/hello-app-runner:latest"
          image_repository_type: ECR_PUBLIC
        auto_deployments_enabled: false
      tags:
        Name: example-apprunner-service

resource:
  aws_apprunner_observability_configuration:
    example:
      observability_configuration_name: example
      trace_configuration:
        vendor: AWSXRAY
```
