# Resource: aws_spot_instance_request

Provides an EC2 Spot Instance Request resource. This allows instances to be
requested on the spot market.

## Basic Example

```yaml
resource:
  aws_spot_instance_request:
    cheap_worker:
      ami: ami-1234
      spot_price: 0.03
      instance_type: c4.xlarge
      tags:
        Name: CheapWorker
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.

Spot Instance Requests support all the same arguments as [`aws_instance`](instance.html), with the addition of:

* `spot_price` - (Optional; Default: On-demand price) The maximum price to request on the spot market.
* `wait_for_fulfillment` - (Optional; Default: false) If set, ytofu will
  wait for the Spot Request to be fulfilled, and will throw an error if the
  timeout of 10m is reached.
* `spot_type` - (Optional; Default: `persistent`) If set to `one-time`, after
  the instance is terminated, the spot request will be closed.
* `launch_group` - (Optional) A launch group is a group of spot instances that launch together and terminate together.
  If left empty instances are launched and terminated individually.
* `instance_interruption_behavior` - (Optional) Indicates Spot instance behavior when it is interrupted. Valid values are `terminate`, `stop`, or `hibernate`. Default value is `terminate`.
* `valid_until` - (Optional) The end date and time of the request, in UTC [RFC3339](https://tools.ietf.org/html/rfc3339#section-5.8) format(for example, YYYY-MM-DDTHH:MM:SSZ). At this point, no new Spot instance requests are placed or enabled to fulfill the request. The default end date is 7 days from the current date.
* `valid_from` - (Optional) The start date and time of the request, in UTC [RFC3339](https://tools.ietf.org/html/rfc3339#section-5.8) format(for example, YYYY-MM-DDTHH:MM:SSZ). The default is to start fulfilling the request immediately.
* `tags` - (Optional) A map of tags to assign to the Spot Instance Request. These tags are not automatically applied to the launched Instance. If configured with a provider `default_tags` configuration block present, tags with matching keys will overwrite those defined at the provider-level.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `id` - The Spot Instance Request ID.
* `tags_all` - A map of tags assigned to the resource, including those inherited from the provider `default_tags` configuration block.

The following attributes are exported, but they are expected to change over time and so should only be used for informational purposes, not for resource dependencies:

* `spot_bid_status` - The current [bid
  status](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/spot-bid-status.html)
  of the Spot Instance Request.
* `spot_request_state` The current [request
  state](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/spot-requests.html#creating-spot-request-status)
  of the Spot Instance Request.
* `spot_instance_id` - The Instance ID (if any) that is currently fulfilling
  the Spot Instance request.
* `public_dns` - The public DNS name assigned to the instance. For EC2-VPC, this
  is only available if you've enabled DNS hostnames for your VPC
* `public_ip` - The public IP address assigned to the instance, if applicable.
* `private_dns` - The private DNS name assigned to the instance. Can only be
  used inside the Amazon EC2, and only available if you've enabled DNS hostnames
  for your VPC
* `private_ip` - The private IP address assigned to the instance

## Timeouts

Configuration options:

* `create` - (Default `10m`)
* `read` - (Default `15m`)
* `delete` - (Default `20m`)
