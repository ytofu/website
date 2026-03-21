# Resource: aws_appmesh_mesh

Provides an AWS App Mesh service mesh resource.

## Basic Example

```yaml
resource:
  aws_appmesh_mesh:
    simple:
      name: simpleapp
```

## Egress Filter

```yaml
resource:
  aws_appmesh_mesh:
    simple:
      name: simpleapp
      spec:
        egress_filter:
          type: ALLOW_ALL
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `name` - (Required) Name to use for the service mesh. Must be between 1 and 255 characters in length.
* `spec` - (Optional) Service mesh specification to apply.
    * `egress_filter`- (Optional) Egress filter rules for the service mesh.
        * `type` - (Optional) Egress filter type. By default, the type is `DROP_ALL`. Valid values are `ALLOW_ALL` and `DROP_ALL`.
    * `service_discovery`- (Optional) The service discovery information for the service mesh.
        * `ip_preference` - (Optional) The IP version to use to control traffic within the mesh. Valid values are `IPv6_PREFERRED`, `IPv4_PREFERRED`, `IPv4_ONLY`, and `IPv6_ONLY`.
* `tags` - (Optional) Map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - ID of the service mesh.
* `arn` - ARN of the service mesh.
* `created_date` - Creation date of the service mesh.
* `last_updated_date` - Last update date of the service mesh.
* `mesh_owner` - AWS account ID of the service mesh's owner.
* `resource_owner` - Resource owner's AWS account ID.
* `tags_all` - Map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_appmesh_mesh.simple simpleapp
```
