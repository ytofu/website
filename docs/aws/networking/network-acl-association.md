# Resource: aws_network_acl_association

Provides an network ACL association resource which allows you to associate your network ACL with any subnet(s).

## Basic Example

```yaml
resource:
  aws_network_acl_association:
    main:
      network_acl_id: ${aws_network_acl.main.id}
      subnet_id: ${aws_subnet.main.id}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `network_acl_id` - (Required) The ID of the network ACL.
* `subnet_id` - (Required) The ID of the associated Subnet.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The ID of the network ACL association

## Import

```bash
ytofu import aws_network_acl_association.main aclassoc-02baf37f20966b3e6
```
