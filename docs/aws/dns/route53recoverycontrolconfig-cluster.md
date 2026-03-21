# Resource: aws_route53recoverycontrolconfig_cluster

Provides an AWS Route 53 Recovery Control Config Cluster.

## Basic Example

```yaml
resource:
  aws_route53recoverycontrolconfig_cluster:
    example:
      name: georgefitzgerald
```

## Argument Reference

This resource supports the following arguments:

* `name` - (Required) Unique name describing the cluster.
* `network_type` - (Optional) Network type of cluster. Valid values are `IPV4` and `DUALSTACK`. Defaults to `IPV4`.

The following arguments are optional:

* `tags` - (Optional) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the cluster
* `cluster_endpoints` - List of 5 endpoints in 5 regions that can be used to talk to the cluster. See below.
* `status` - Status of cluster. `PENDING` when it is being created, `PENDING_DELETION` when it is being deleted and `DEPLOYED` otherwise.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

### cluster_endpoints

* `endpoint` - Cluster endpoint.
* `region` - Region of the endpoint.

## Import

```bash
ytofu import aws_route53recoverycontrolconfig_cluster.mycluster arn:aws:route53-recovery-control::313517334327:cluster/f9ae13be-a11e-4ec7-8522-94a70468e6ea
```
