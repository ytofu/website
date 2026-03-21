# ECS Task Definition

Manage ECS Task Definition resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_ecs_task_definition:
    service:
      family: service
      container_definitions: 'example-json-policy'
      volume:
        name: service-storage
        host_path: /ecs/service-storage
      placement_constraints:
        type: memberOf
        expression: "attribute:ecs.availability-zone in [us-west-2a, us-west-2b]"
```

## With AppMesh Proxy

```yaml
resource:
  aws_ecs_task_definition:
    service:
      family: service
      container_definitions: file-content
      proxy_configuration:
        type: APPMESH
        container_name: applicationContainerName
        properties:
          AppPorts: 8080
          EgressIgnoredIPs: 169.254.170.2,169.254.169.254
          IgnoredUID: 1337
          ProxyEgressPort: 15001
          ProxyIngressPort: 15000
```

## Example Using `docker_volume_configuration`

```yaml
resource:
  aws_ecs_task_definition:
    service:
      family: service
      container_definitions: file-content
      volume:
        name: service-storage
        docker_volume_configuration:
          scope: shared
          autoprovision: true
          driver: local
          driver_opts: 
```

## Example Using `efs_volume_configuration`

```yaml
resource:
  aws_ecs_task_definition:
    service:
      family: service
      container_definitions: file-content
      volume:
        name: service-storage
        efs_volume_configuration:
          file_system_id: ${aws_efs_file_system.fs.id}
          root_directory: /opt/data
          transit_encryption: ENABLED
          transit_encryption_port: 2999
          authorization_config:
            access_point_id: ${aws_efs_access_point.test.id}
            iam: ENABLED
```

## Example Using `fsx_windows_file_server_volume_configuration`

```yaml
resource:
  aws_ecs_task_definition:
    service:
      family: service
      container_definitions: file-content
      volume:
        name: service-storage
        fsx_windows_file_server_volume_configuration:
          file_system_id: ${aws_fsx_windows_file_system.test.id}
          root_directory: \\data
          authorization_config:
            credentials_parameter: ${aws_secretsmanager_secret_version.test.arn}
            domain: ${aws_directory_service_directory.test.name}

resource:
  aws_secretsmanager_secret_version:
    test:
      secret_id: ${aws_secretsmanager_secret.test.id}
      secret_string: '{ username : "admin", password : aws_directory_service_directory.test.password }'
```

## Example Using `container_definitions`

```yaml
resource:
  aws_ecs_task_definition:
    test:
      family: test
      container_definitions: |
        [
        {
        "cpu": 10,
        "command": ["sleep", "10"],
        "entryPoint": ["/"],
        "environment": [
        {"name": "VARNAME", "value": "VARVAL"}
        ],
        "essential": true,
        "image": "jenkins",
        "memory": 128,
        "name": "jenkins",
        "portMappings": [
        {
        "containerPort": 80,
        "hostPort": 8080
        }
        ]
        }
        ]
```

## Example Using `runtime_platform` and `fargate`

```yaml
resource:
  aws_ecs_task_definition:
    test:
      family: test
      requires_compatibilities: 
        - FARGATE
      network_mode: awsvpc
      cpu: 1024
      memory: 2048
      container_definitions: |
        [
        {
        "name": "iis",
        "image": "mcr.microsoft.com/windows/servercore/iis",
        "cpu": 1024,
        "memory": 2048,
        "essential": true
        }
        ]
      runtime_platform:
        operating_system_family: WINDOWS_SERVER_2019_CORE
        cpu_architecture: X86_64
```
