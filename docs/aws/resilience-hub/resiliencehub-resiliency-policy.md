# Resource: aws_resiliencehub_resiliency_policy

ytofu resource for managing an AWS Resilience Hub Resiliency Policy.

## Basic Example

```yaml
resource:
  aws_resiliencehub_resiliency_policy:
    example:
      name: testexample
      description: testexample
      tier: NonCritical
      data_location_constraint: AnyLocation
      policy:
        region:
          rpo: 24h
          rto: 24h
        az:
          rpo: 24h
          rto: 24h
        hardware:
          rpo: 24h
          rto: 24h
        software:
          rpo: 24h
          rto: 24h
```

## Argument Reference

The following arguments are required:

* `name` (String) Name of Resiliency Policy.
  Must be between 2 and 60 characters long.
  Must start with an alphanumeric character and contain alphanumeric characters, underscores, or hyphens.
* `tier` (String) Resiliency Policy Tier.
  Valid values are `MissionCritical`, `Critical`, `Important`, `CoreServices`, `NonCritical`, and `NotApplicable`.
* `policy` (Attributes) The type of resiliency policy to be created, including the recovery time objective (RTO) and recovery point objective (RPO) in seconds. See [`policy`](#policy).

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `description` (String) Description of Resiliency Policy.
* `data_location_constraint` (String) Data Location Constraint of the Policy.
  Valid values are `AnyLocation`, `SameContinent`, and `SameCountry`.
* `tags` - (Map Of String) A map of tags to assign to the resource. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

### `policy`

The following arguments are required:

* `az` - (Attributes) Specifies Availability Zone failure policy. See [`policy.az`](#policyaz)
* `hardware` - (Attributes) Specifies Infrastructure failure policy. See [`policy.hardware`](#policyhardware)
* `software` - (Attributes) Specifies Application failure policy. See [`policy.software`](#policysoftware)

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `region` - (Attributes) Specifies Region failure policy. [`policy.region`](#policyregion)

### `policy.az`

The following arguments are required:

* `rpo` - (Number) Recovery Point Objective (RPO) as a Go duration.
  Represented by a string such as `1h`, `2h45m`, or `30m15s`.
* `rto` - (Number) Recovery Time Objective (RTO) as a Go duration.
  Represented by a string such as `1h`, `2h45m`, or `30m15s`.

### `policy.hardware`

The following arguments are required:

* `rpo` - (Number) Recovery Point Objective (RPO) as a Go duration.
  Represented by a string such as `1h`, `2h45m`, or `30m15s`.
* `rto` - (Number) Recovery Time Objective (RTO) as a Go duration.
  Represented by a string such as `1h`, `2h45m`, or `30m15s`.

### `policy.software`

The following arguments are required:

* `rpo` - (Number) Recovery Point Objective (RPO) as a Go duration.
  Represented by a string such as `1h`, `2h45m`, or `30m15s`.
* `rto` - (Number) Recovery Time Objective (RTO) as a Go duration.
  Represented by a string such as `1h`, `2h45m`, or `30m15s`.

### `policy.region`

The following arguments are required:

* `rpo` - (Number) Recovery Point Objective (RPO) as a Go duration.
  Represented by a string such as `1h`, `2h45m`, or `30m15s`.
* `rto` - (Number) Recovery Time Objective (RTO) as a Go duration.
  Represented by a string such as `1h`, `2h45m`, or `30m15s`.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - ARN of the Resiliency Policy.
* `estimated_cost_tier` - Estimated Cost Tier of the Resiliency Policy.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

## Timeouts

Configuration options:

* `create` - (Default `30m`)
* `update` - (Default `30m`)
* `delete` - (Default `30m`)

## Import

```bash
ytofu import aws_resiliencehub_resiliency_policy.example arn:aws:resiliencehub:us-east-1:123456789012:resiliency-policy/8c1cfa29-d1dd-4421-aa68-c9f64cced4c2
```
