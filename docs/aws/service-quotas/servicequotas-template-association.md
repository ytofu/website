# Resource: aws_servicequotas_template_association

ytofu resource for managing an AWS Service Quotas Template Association.

## Basic Example

```yaml
resource:
  aws_servicequotas_template_association:
    example:
```

## Argument Reference

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `skip_destroy` - (Optional) Skip disassociating the quota increase template upon destruction. This will remove the resource from ytofu state, but leave the remote association in place.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - AWS account ID.
* `status` - Association status. Creating this resource will result in an `ASSOCIATED` status, and quota increase requests in the template are automatically applied to new AWS accounts in the organization.

## Import

```bash
ytofu import aws_servicequotas_template_association.example 123456789012
```
