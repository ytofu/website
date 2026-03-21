# Location Tracker Association

Manage Location Tracker Association resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_location_geofence_collection:
    example:
      collection_name: example

resource:
  aws_location_tracker:
    example:
      tracker_name: example

resource:
  aws_location_tracker_association:
    example:
      consumer_arn: ${aws_location_geofence_collection.example.collection_arn}
      tracker_name: ${aws_location_tracker.example.tracker_name}
```
