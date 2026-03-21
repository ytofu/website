# Elastic Beanstalk Environment

Manage Elastic Beanstalk Environment resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_elastic_beanstalk_environment:
    example:
      name: tf-test-name
      application: ${aws_elastic_beanstalk_application.example.name}
      solution_stack_name: 64bit Amazon Linux 2015.03 v2.0.3 running Go 1.4

resource:
  aws_elastic_beanstalk_application:
    example:
      name: tf-test-name
      description: tf-test-desc
```
