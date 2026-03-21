# App Runner Service

Create and manage App Runner services using ytofu YAML.

## From Public ECR Image

```yaml
resource:
  aws_apprunner_service:
    example:
      service_name: example
      source_configuration:
        image_repository:
          image_configuration:
            port: "8000"
          image_identifier: public.ecr.aws/aws-containers/hello-app-runner:latest
          image_repository_type: ECR_PUBLIC
      tags:
        Name: example
```

## From Private ECR

```yaml
resource:
  aws_apprunner_service:
    example:
      service_name: example
      source_configuration:
        authentication_configuration:
          access_role_arn: ${aws_iam_role.apprunner.arn}
        image_repository:
          image_configuration:
            port: "8080"
            runtime_environment_variables:
              ENV: production
          image_identifier: ${aws_ecr_repository.example.repository_url}:latest
          image_repository_type: ECR
        auto_deployments_enabled: true
```

## From GitHub

```yaml
resource:
  aws_apprunner_service:
    example:
      service_name: example
      source_configuration:
        authentication_configuration:
          connection_arn: ${aws_apprunner_connection.example.arn}
        code_repository:
          repository_url: https://github.com/example/app
          source_code_version:
            type: BRANCH
            value: main
          code_configuration:
            configuration_source: API
            code_configuration_values:
              runtime: PYTHON_3
              build_command: pip install -r requirements.txt
              start_command: python app.py
              port: "8080"
```

## With VPC Connector

```yaml
resource:
  aws_apprunner_service:
    example:
      service_name: example
      source_configuration:
        image_repository:
          image_configuration:
            port: "8080"
          image_identifier: ${aws_ecr_repository.example.repository_url}:latest
          image_repository_type: ECR
      network_configuration:
        egress_configuration:
          egress_type: VPC
          vpc_connector_arn: ${aws_apprunner_vpc_connector.connector.arn}
```

## With Instance Config

```yaml
resource:
  aws_apprunner_service:
    example:
      service_name: example
      source_configuration:
        image_repository:
          image_configuration:
            port: "8080"
          image_identifier: public.ecr.aws/aws-containers/hello-app-runner:latest
          image_repository_type: ECR_PUBLIC
      instance_configuration:
        cpu: "1024"
        memory: "2048"
        instance_role_arn: ${aws_iam_role.instance.arn}
      health_check_configuration:
        protocol: HTTP
        path: /health
        healthy_threshold: 1
        unhealthy_threshold: 5
        interval: 10
```
