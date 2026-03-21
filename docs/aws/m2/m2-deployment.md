# Resource: aws_m2_deployment

ytofu resource for managing an [AWS Mainframe Modernization Deployment.](https://docs.aws.amazon.com/m2/latest/userguide/applications-m2-deploy.html)

## Basic Example

```yaml
resource:
  aws_m2_deployment:
    test:
      environment_id: 01234567890abcdef012345678
      application_id: 34567890abcdef012345678012
      application_version: 1
      start: true
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `environment_id` - (Required) Environment to deploy application to.
* `application_id` - (Required) Application to deploy.
* `application_version` - (Required) Version to application to deploy
* `start` - (Required) Start the application once deployed.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

## Timeouts

Configuration options:

* `create` - (Default `60m`)
* `update` - (Default `60m`)
* `delete` - (Default `60m`)

## Import

```bash
ytofu import aws_m2_deployment.example APPLICATION-ID,DEPLOYMENT-ID
```
