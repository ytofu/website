# Resource: aws_default_vpc

Provides a resource to manage the [default AWS VPC](http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/default-vpc.html)
in the current AWS Region.

## Basic Example

```yaml
resource:
  aws_default_vpc:
    default:
      tags:
        Name: Default VPC
```

## Argument Reference

This resource supports the following arguments:

The arguments of an `aws_default_vpc` differ slightly from those of [`aws_vpc`](vpc.html):

* The `cidr_block` and `instance_tenancy` arguments become computed attributes
* The default value for `enable_dns_hostnames` is `true`

This resource supports the following additional arguments:

* `force_destroy` - (Optional) Whether destroying the resource deletes the default VPC. Default: `false`

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `cidr_block` - The primary IPv4 CIDR block for the VPC
* `instance_tenancy` - The allowed tenancy of instances launched into the VPC

## Import

```bash
ytofu import aws_default_vpc.default vpc-a01106c2
```
