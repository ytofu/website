# Resource: aws_dx_connection_confirmation

Provides a confirmation of the creation of the specified hosted connection on an interconnect.

## Basic Example

```yaml
resource:
  aws_dx_connection_confirmation:
    confirmation:
      connection_id: dxcon-ffabc123
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `connection_id` - (Required) The ID of the hosted connection.

### Removing `aws_dx_connection_confirmation` from your configuration

Removing an `aws_dx_connection_confirmation` resource from your configuration will remove it
from your statefile and management, **but will not destroy the Hosted Connection.**

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The ID of the connection.
