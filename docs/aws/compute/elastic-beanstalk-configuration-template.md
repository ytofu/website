# Elastic Beanstalk Configuration Template

Manage Elastic Beanstalk Configuration Template resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_elastic_beanstalk_configuration_template:
    example:
      name: tf-test-template-config
      application: ${aws_elastic_beanstalk_application.example.name}
      solution_stack_name: 64bit Amazon Linux 2015.09 v2.0.8 running Go 1.4

resource:
  aws_elastic_beanstalk_application:
    example:
      name: tf-test-name
      description: tf-test-desc
```
