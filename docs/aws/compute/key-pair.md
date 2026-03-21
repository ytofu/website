# Resource: aws_key_pair

Provides an [EC2 key pair](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html) resource. A key pair is used to control login access to EC2 instances.

## Basic Example

```yaml
resource:
  aws_key_pair:
    deployer:
      key_name: deployer-key
      public_key: ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQD3F6tyPEFEzV0LX3X8BsXdMsQz1x2cEikKDEY0aIj41qgxMCP/iteneqXSIFZBp5vizPvaoIR3Um9xK7PGoW8giupGn+EPuxIA4cDM4vzOqOkiMPhz5XK0whEjkVzTo4+S0puvDZuwIsdiW9mxhJc7tgBNL0cYlWSYVkz4G/fslNfRPW5mYAM49f4fhtxPb5ok4Q2Lg9dPKVHO/Bgeu5woMc7RY0p1ej6D4CKFE6lymSDJpW0YHX/wqE9+cfEauh7xZcG0q9t2ta6F6fmX0agvpFyZo8aFbXeUBr7osSCJNgvavWbM/06niWrOvYX2xwWdhXmXSrbX8ZbabVohBK41 email@example.com
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `key_name` - (Optional) The name for the key pair. If neither `key_name` nor `key_name_prefix` is provided, ytofu will create a unique key name using the prefix `terraform-`.
* `key_name_prefix` - (Optional) Creates a unique name beginning with the specified prefix. Conflicts with `key_name`. If neither `key_name` nor `key_name_prefix` is provided, ytofu will create a unique key name using the prefix `terraform-`.
* `public_key` - (Required) The public key material.
* `tags` - (Optional) Key-value map of resource tags. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The key pair name.
* `arn` - The key pair ARN.
* `key_name` - The key pair name.
* `key_pair_id` - The key pair ID.
* `key_type` - The type of key pair.
* `fingerprint` - The MD5 public key fingerprint as specified in section 4 of RFC 4716.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_key_pair.deployer deployer-key
```
