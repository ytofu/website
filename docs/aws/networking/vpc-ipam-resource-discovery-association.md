# Resource: aws_vpc_ipam_resource_discovery_association

Provides an association between an Amazon IP Address Manager (IPAM) and a IPAM Resource Discovery. IPAM Resource Discoveries are resources meant for multi-organization customers. If you wish to use a single IPAM across multiple orgs, a resource discovery can be created and shared from a subordinate organization to the management organizations IPAM delegated admin account.

## Basic Example

```yaml
resource:
  aws_vpc_ipam_resource_discovery_association:
    test:
      ipam_id: ${aws_vpc_ipam.test.id}
      ipam_resource_discovery_id: ${aws_vpc_ipam_resource_discovery.test.id}
      tags: 
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `ipam_id` - (Required) The ID of the IPAM to associate.
* `ipam_resource_discovery_id` - (Required) The ID of the Resource Discovery to associate.
* `tags` - (Optional) A map of tags to add to the IPAM resource discovery association resource.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - The Amazon Resource Name (ARN) of IPAM Resource Discovery Association.
* `id` - The ID of the IPAM Resource Discovery Association.
* `owner_id` - The account ID for the account that manages the Resource Discovery
* `ipam_arn` - The Amazon Resource Name (ARN) of the IPAM.
* `ipam_region` - The home region of the IPAM.
* `is_default` - A boolean to identify if the Resource Discovery is the accounts default resource discovery.
* `state` - The lifecycle state of the association when you associate or disassociate a resource discovery.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Import

```bash
ytofu import aws_vpc_ipam_resource_discovery_association.example ipam-res-disco-assoc-0178368ad2146a492
```
