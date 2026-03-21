# Resource: aws_iam_group

Provides an IAM group.

## Basic Example

```yaml
resource:
  aws_iam_group:
    developers:
      name: developers
      path: /users/
```

## Argument Reference

This resource supports the following arguments:

* `name` - (Required) The group's name. The name must consist of upper and lowercase alphanumeric characters with no spaces. You can also include any of the following characters: `=,.@-_.`. Group names are not distinguished by case. For example, you cannot create groups named both "ADMINS" and "admins".
* `path` - (Optional, default "/") Path in which to create the group.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The group's name.
* `arn` - The ARN assigned by AWS for this group.
* `name` - The group's name.
* `path` - The path of the group in IAM.
* `unique_id` - The [unique ID][1] assigned by AWS.

  [1]: https://docs.aws.amazon.com/IAM/latest/UserGuide/Using_Identifiers.html#GUIDs

## Import

```bash
ytofu import aws_iam_group.developers developers
```
