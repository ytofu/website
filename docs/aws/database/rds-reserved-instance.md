# RDS Reserved Instance

Manage RDS Reserved Instance resources using ytofu YAML.

## Basic Example

```yaml
data:
  aws_rds_reserved_instance_offering:
    test:
      db_instance_class: db.t2.micro
      duration: 31536000
      multi_az: false
      offering_type: All Upfront
      product_description: mysql

resource:
  aws_rds_reserved_instance:
    example:
      offering_id: ${data.aws_rds_reserved_instance_offering.test.offering_id}
      reservation_id: optionalCustomReservationID
      instance_count: 3
```
