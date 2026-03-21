# Devicefarm Upload

Manage Devicefarm Upload resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_devicefarm_project:
    example:
      name: example

resource:
  aws_devicefarm_upload:
    example:
      name: example
      project_arn: ${aws_devicefarm_project.example.arn}
      type: APPIUM_JAVA_TESTNG_TEST_SPEC
```
