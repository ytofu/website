# Resource: aws_default_subnet

Provides a resource to manage a [default subnet](http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/default-vpc.html#default-vpc-basics) in the current region.

## Basic Example

```yaml
resource:
  aws_default_subnet:
    default_az1:
      availability_zone: us-west-2a
      tags:
        Name: Default subnet for us-west-2a
```

## Argument Reference

This resource supports the following arguments:

The arguments of an `aws_default_subnet` differ slightly from those of [`aws_subnet`](subnet.html):

* `availability_zone` is required
* The `availability_zone_id`, `cidr_block` and `vpc_id` arguments become computed attributes
* The default value for `map_public_ip_on_launch` is `true`

This resource supports the following additional arguments:

* `force_destroy` - (Optional) Whether destroying the resource deletes the default subnet. Default: `false`

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `availability_zone_id` - The AZ ID of the subnet
* `cidr_block` - The IPv4 CIDR block assigned to the subnet
* `vpc_id` - The ID of the VPC the subnet is in

## Import

```bash
ytofu import aws_default_subnet.public_subnet subnet-9d4a7b6c
```
