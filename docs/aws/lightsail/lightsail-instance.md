# Lightsail Instance

Manage Lightsail Instance resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_lightsail_instance:
    example:
      name: example
      availability_zone: us-east-1b
      blueprint_id: amazon_linux_2
      bundle_id: nano_3_0
      key_pair_name: some_key_name
      tags:
        foo: bar
```

## Example With User Data

```yaml
resource:
  aws_lightsail_instance:
    example:
      name: example
      availability_zone: us-east-1b
      blueprint_id: amazon_linux_2
      bundle_id: nano_3_0
      user_data: "sudo yum install -y httpd && sudo systemctl start httpd && sudo systemctl enable httpd && echo '<h1>Deployed via Terraform</h1>' | sudo tee /var/www/html/index.html"
```

## Enable Auto Snapshots

```yaml
resource:
  aws_lightsail_instance:
    example:
      name: example
      availability_zone: us-east-1b
      blueprint_id: amazon_linux_2
      bundle_id: nano_3_0
      add_on:
        type: AutoSnapshot
        snapshot_time: "06:00"
        status: Enabled
      tags:
        foo: bar
```
