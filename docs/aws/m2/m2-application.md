# Resource: aws_m2_application

ytofu resource for managing an [AWS Mainframe Modernization Application](https://docs.aws.amazon.com/m2/latest/userguide/applications-m2.html).

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

## Argument Reference

The following arguments are required:

* `description` - (Required) Description of the application.
* `engine_type` - (Required) Engine type must be `microfocus | bluage`.
* `name` - (Required) Unique identifier of the application.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `definition` - (Optional) The application definition for this application. You can specify either inline JSON or an S3 bucket location.
* `kms_key_id` - (Optional) KMS Key to use for the Application.
* `role_arn` - (Optional) ARN of role for application to use to access AWS resources.
* `tags` - (Optional) Map of tags assigned to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## definition

This argument is processed in attribute-as-blocks mode.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `content` - (Optional) JSON application definition. Either this or `s3_location` must be specified.
* `s3_location` - (Optional) Location of the application definition in S3. Either this or `content` must be specified.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `application_id` - Id of the Application.
* `arn` - ARN of the Application.
* `current_version` - Current version of the application deployed.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Timeouts

Configuration options:

* `create` - (Default `30m`)
* `update` - (Default `30m`)
* `delete` - (Default `30m`)

## Import

```bash
ytofu import aws_m2_application.example 01234567890abcdef012345678
```
