# M2 Application

Manage M2 Application resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_m2_application:
    example:
      name: Example
      engine_type: bluage
      definition:
        content: |
          {
          "definition": {
          "listeners": [
          {
          "port": 8196,
          "type": "http"
          }
          ],
          "ba-application": {
          "app-location": "${s3-source}/PlanetsDemo-v1.zip"
          }
          },
          "source-locations": [
          {
          "source-id": "s3-source",
          "source-type": "s3",
          "properties": {
          "s3-bucket": "example-bucket",
          "s3-key-prefix": "v1"
          }
          }
          ],
          "template-version": "2.0"
          }
          
```
