# Resource: aws_backup_region_settings

Provides an AWS Backup Region Settings resource.

## Basic Example

```yaml
resource:
  aws_backup_region_settings:
    test:
      resource_type_opt_in_preference: 
      resource_type_management_preference: 
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `resource_type_opt_in_preference` - (Required) A map of service names to their opt-in preferences for the Region. See [AWS Documentation on which services support backup](https://docs.aws.amazon.com/aws-backup/latest/devguide/backup-feature-availability.html).
* `resource_type_management_preference` - (Optional) A map of service names to their full management preferences for the Region. For more information, see the AWS Documentation on [what full management is](https://docs.aws.amazon.com/aws-backup/latest/devguide/whatisbackup.html#full-management) and [which services support full management](https://docs.aws.amazon.com/aws-backup/latest/devguide/backup-feature-availability.html#features-by-resource).

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The AWS region.

## Import

```bash
ytofu import aws_backup_region_settings.test us-west-2
```
