# Resource: aws_imagebuilder_component

Manages an Image Builder Component.

## Basic Example

```yaml
resource:
  aws_imagebuilder_component:
    example:
      data: '# yamlencode content'
      name: example
      platform: Linux
      version: 1.0.0
```

## URI Document

```yaml
resource:
  aws_imagebuilder_component:
    example:
      name: example
      platform: Linux
      uri: "s3://${aws_s3_object.example.bucket}/${aws_s3_object.example.key}"
      version: 1.0.0
```

## Argument Reference

The following arguments are required:

* `name` - (Required) Name of the component.
* `platform` - (Required) Platform of the component.
* `version` - (Required) Version of the component.

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `change_description` - (Optional) Change description of the component.
* `data` - (Optional) Inline YAML string with data of the component. Exactly one of `data` and `uri` can be specified. ytofu will only perform drift detection of its value when present in a configuration.
* `description` - (Optional) Description of the component.
* `kms_key_id` - (Optional) Amazon Resource Name (ARN) of the Key Management Service (KMS) Key used to encrypt the component.
* `skip_destroy` - (Optional) Whether to retain the old version when the resource is destroyed or replacement is necessary. Defaults to `false`.
* `supported_os_versions` - (Optional) Set of Operating Systems (OS) supported by the component.
* `tags` - (Optional) Key-value map of resource tags for the component. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.
* `uri` - (Optional) S3 URI with data of the component. Exactly one of `data` and `uri` can be specified.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - Amazon Resource Name (ARN) of the component.
* `arn` - (Required) Amazon Resource Name (ARN) of the component.
* `date_created` - Date the component was created.
* `encrypted` - Encryption status of the component.
* `owner` - Owner of the component.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.
* `type` - Type of the component.

## Import

```bash
ytofu import aws_imagebuilder_component.example arn:aws:imagebuilder:us-east-1:123456789012:component/example/1.0.0/1
```
