# Resource: aws_ec2_subnet_cidr_reservation

Provides a subnet CIDR reservation resource.

## Basic Example

```yaml
resource:
  aws_ec2_subnet_cidr_reservation:
    example:
      cidr_block: 10.0.0.16/28
      reservation_type: prefix
      subnet_id: ${aws_subnet.example.id}
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `cidr_block` - (Required) The CIDR block for the reservation.
* `reservation_type` - (Required) The type of reservation to create. Valid values: `explicit`, `prefix`
* `subnet_id` - (Required) The ID of the subnet to create the reservation for.
* `description` - (Optional) A brief description of the reservation.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - ID of the CIDR reservation.
* `owner_id` - ID of the AWS account that owns this CIDR reservation.

## Import

```bash
ytofu import aws_ec2_subnet_cidr_reservation.example subnet-01llsxvsxabqiymcz:scr-4mnvz6wb7otksjcs9
```
