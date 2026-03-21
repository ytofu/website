# Codecatalyst Dev Environment

Manage Codecatalyst Dev Environment resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_codecatalyst_dev_environment:
    test:
      alias: devenv
      space_name: myspace
      project_name: myproject
      instance_type: dev.standard1.small
      persistent_storage:
        size: 16
      ides:
        name: PyCharm
        runtime: public.ecr.aws/jetbrains/py
      inactivity_timeout_minutes: 40
      repositories:
        repository_name: terraform-provider-aws
        branch_name: main
```
