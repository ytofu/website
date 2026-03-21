# Connect Routing Profile

Manage Connect Routing Profile resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_connect_routing_profile:
    example:
      instance_id: aaaaaaaa-bbbb-cccc-dddd-111111111111
      name: example
      default_outbound_queue_id: 12345678-1234-1234-1234-123456789012
      description: example description
      media_concurrencies:
        channel: VOICE
        concurrency: 1
        cross_channel_behavior:
          behavior_type: ROUTE_ANY_CHANNEL
      media_concurrencies:
        channel: CHAT
        concurrency: 3
        cross_channel_behavior:
          behavior_type: ROUTE_CURRENT_CHANNEL_ONLY
      queue_configs:
        channel: VOICE
        delay: 2
        priority: 1
        queue_id: 12345678-1234-1234-1234-123456789012
      tags: 
```
