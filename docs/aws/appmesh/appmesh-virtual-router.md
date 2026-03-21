# Resource: aws_appmesh_virtual_router

Provides an AWS App Mesh virtual router resource.

## Basic Example

```yaml
resource:
  aws_appmesh_virtual_router:
    serviceb:
      name: serviceB
      mesh_name: ${aws_appmesh_mesh.simple.id}
      spec:
        listener:
          port_mapping:
            port: 8080
            protocol: http
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) Name to use for the virtual router. Must be between 1 and 255 characters in length.
* `mesh_name` - (Required) Name of the service mesh in which to create the virtual router. Must be between 1 and 255 characters in length.
* `mesh_owner` - (Optional) AWS account ID of the service mesh's owner. Defaults to the account ID the [AWS provider][1] is currently connected to.
* `spec` - (Required) Virtual router specification to apply.
* `tags` - (Optional) Map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

The `spec` object supports the following:

* `listener` - (Optional) Listeners that the virtual router is expected to receive inbound traffic from.
Currently only one listener is supported per virtual router.

The `listener` object supports the following:

* `port_mapping` - (Required) Port mapping information for the listener.

The `port_mapping` object supports the following:

* `port` - (Required) Port used for the port mapping.
* `protocol` - (Required) Protocol used for the port mapping. Valid values are `http`,`http2`, `tcp` and `grpc`.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - ID of the virtual router.
* `arn` - ARN of the virtual router.
* `created_date` - Creation date of the virtual router.
* `last_updated_date` - Last update date of the virtual router.
* `resource_owner` - Resource owner's AWS account ID.
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_appmesh_virtual_router.serviceb simpleapp/serviceB
```
