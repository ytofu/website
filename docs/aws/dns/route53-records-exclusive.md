# Resource: aws_route53_records_exclusive

ytofu resource for maintaining exclusive management of resource record sets defined in an AWS Route53 hosted zone.

## Basic Example

```yaml
resource:
  aws_route53_zone:
    example:
      name: example.com
      force_destroy: true

  aws_route53_records_exclusive:
    test:
      zone_id: ${aws_route53_zone.test.zone_id}
      resource_record_set:
        name: subdomain.example.com
        type: A
        ttl: 30
        resource_records:
          value: 127.0.0.1
        resource_records:
          value: 127.0.0.27```

## Disallow Record Sets

```yaml
resource:
  aws_route53_records_exclusive:
    test:
      zone_id: ${aws_route53_zone.test.zone_id}
```

## Argument Reference

The following arguments are required:

* `zone_id` - (Required) ID of the hosted zone containing the resource record sets.

The following arguments are optional:

* `resource_record_set` - (Optional) A list of all resource record sets associated with the hosted zone.
See [`resource_record_set`](#resource_record_set) below.

### `resource_record_set`

The following arguments are required:

* `name` - (Required) Name of the record.
* `type` - (Required) Record type.
Valid values are `A`, `AAAA`, `CAA`, `CNAME`, `DS`, `MX`, `NAPTR`, `NS`, `PTR`, `SOA`, `SPF`, `SRV`, `TXT`, `TLSA`, `SSHFP`, `SVCB`, and `HTTPS`.

The following arguments are optional:

* `alias_target` - (Optional) Alias target block.
See [`alias_target`](#alias_target) below.
* `cidr_routing_policy` - (Optional) CIDR routing configuration block.
See [`cidr_routing_config`](#cidr_routing_config) below.
* `failover` - (Optional) Type of failover resource record.
Valid values are `PRIMARY` and `SECONDARY`.
See the [AWS documentation on DNS failover](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/dns-failover.html) for additional details.
* `geolocation` - (Optional) Geolocation block to control how Amazon Route 53 responds to DNS queries based on the geographic origin of the query.
See [`geolocation`](#geolocation) below.
* `geoproximity_location` - (Optional) Geoproximity location block.
See [`geoproximity_location`](#geoproximity_location) below.
* `health_check_id` - (Optional) Health check the record should be associated with.
* `multivalue_answer` - (Optional) Set to `true` to indicate this record is a multivalue answer record and traffic should be routed approximately randomly to multiple resources.
* `region` - (Optional) AWS region of the resource this record set refers to.
Must be a valid AWS region name.
See the [AWS documentation](http://docs.aws.amazon.com/Route53/latest/DeveloperGuide/routing-policy.html#routing-policy-latency) on latency based routing for additional details.
* `resource_records` - (Optional, Required for non-alias records) Information about the resource records to act upon.
See [`resource_records`](#resource_records) below.
* `set_identifier` - (Optional) An identifier that differentiates among multiple resource record sets that have the same combination of name and type.
Required if using `cidr_routing_config`, `failover`, `geolocation`,`geoproximity_location`, `multivalue_answer`, `region`, or `weight`.
* `traffic_policy_instance_id` - (Optional) ID of the traffic policy instance that Route 53 created this resource record set for.
To delete the resource record set that is associated with a traffic policy instance, use the `DeleteTrafficPolicyInstance` API.
Route 53 will delete the resource record set automatically.
If the resource record set is deleted via `ChangeResourceRecordSets` (the API underpinning this ytofu resource), Route 53 doesn't automatically delete the traffic policy instance, and you'll continue to be charged for it.
* `ttl` - (Optional, Required for non-alias records) Resource record cache time to live (TTL), in seconds.
* `weight` - (Optional) Among resource record sets that have the same combination of DNS name and type, a value that determines the proportion of DNS queries that Amazon Route 53 responds to using the current resource record set.

### `alias_target`

* `dns_name` - (Required) DNS domain name for another resource record set in this hosted zone.
* `evaluate_target_health` - (Required) Set to `true` if you want Route 53 to determine whether to respond to DNS queries using this resource record set by checking the health of the resource record set. Some resources have special requirements, see [the AWS documentation](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/resource-record-sets-values.html#rrsets-values-alias-evaluate-target-health) for additional details.
* `hosted_zone_id` - (Required) Hosted zone ID for a CloudFront distribution, S3 bucket, ELB, AWS Global Accelerator, or Route 53 hosted zone. See `resource_elb.zone_id` for an example.

### `cidr_routing_config`

* `collection_id` - (Required) CIDR collection ID.
See the [`aws_route53_cidr_collection` resource](route53_cidr_collection.html) for more details.
* `location_name` - (Required) CIDR collection location name.
See the [`aws_route53_cidr_location` resource](route53_cidr_location.html) for more details.
A `location_name` with an asterisk `"*"` can be used to create a default CIDR record.
`collection_id` is still required for a default record.

### `geolocation`

* `continent` - (Optional) Two-letter continent code.
See the [AWS documentation](http://docs.aws.amazon.com/Route53/latest/APIReference/API_GetGeoLocation.html) for valid values.
* `country` - (Optional) Two-letter country code.
See the ISO standard linked from the [AWS documentation](http://docs.aws.amazon.com/Route53/latest/APIReference/API_GetGeoLocation.html) for valid values.
* `subdivision` - (Optional) Subdivision code.

### `geoproximity_location`

* `aws_region` - (Optional) AWS region of the resource where DNS traffic is directed to.
* `bias` - (Optional) Increases or decreases the size of the geographic region from which Route 53 routes traffic to a resource.
To expand the size of the geographic region from which Route 53 routes traffic to a resource, specify a positive integer from `1` to `99`.
To shrink the size of the geographic region from which Route 53 routes traffic to a resource, specify a negative bias of `-1` to `-99`.
See the [AWS documentation](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/routing-policy-geoproximity.html) for additional details.
* `coordinates` - (Optional) Coordinates for a geoproximity resource record.
See [`coordinates`](#coordinates) below.
* `local_zone_group` - (Optional) AWS local zone group.
Identify the Local Zones Group for a specific Local Zone by using the [`describe-availability-zones` CLI command](https://docs.aws.amazon.com/cli/latest/reference/ec2/describe-availability-zones.html).

#### `coordinates`

* `latitude` - (Required) A coordinate of the north–south position of a geographic point on the surface of the Earth (`-90` - `90`).
* `longitude` - (Required) A coordinate of the east–west position of a geographic point on the surface of the Earth (`-180` - `180`).

### `resource_records`

* `value` - (Required) DNS record value.

## Attribute Reference

This resource exports no additional attributes.

## Timeouts

Configuration options:

* `create` - (Default `45m`)
* `update` - (Default `45m`)

## Import

```bash
ytofu import aws_route53_records_exclusive.example ABCD1234
```
