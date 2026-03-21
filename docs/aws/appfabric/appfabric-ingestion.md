# Resource: aws_appfabric_ingestion

ytofu resource for managing an AWS AppFabric Ingestion.

## Basic Example

```yaml
resource:
  aws_appfabric_ingestion:
    example:
      app: OKTA
      app_bundle_arn: ${aws_appfabric_app_bundle.example.arn}
      tenant_id: example.okta.com
      ingestion_type: auditLog
      tags:
        Environment: test
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `app` - (Required) Name of the application.
Refer to the AWS Documentation for the [list of valid values](https://docs.aws.amazon.com/appfabric/latest/api/API_CreateIngestion.html#appfabric-CreateIngestion-request-app)
* `app_bundle_arn` - (Required) Amazon Resource Name (ARN) of the app bundle to use for the request.
* `ingestion_type` - (Required) Ingestion type. Valid values are `auditLog`.
* `tags` - (Optional) Map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.
* `tenant_id` - (Required) ID of the application tenant.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the Ingestion.
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_appfabric_ingestion.example arn:aws:appfabric:[region]:[account]:appbundle/a9b91477-8831-43c0-970c-xxxxxxxxxx,arn:aws:appfabric:[region]:[account]:appbundle/a9b91477-8831-43c0-970c-xxxxxxxxxx/ingestion/32251416-710b-4425-96ca-xxxxxxxxxx
```
