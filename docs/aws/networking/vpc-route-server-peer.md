# VPC Route Server Peer

Manage VPC Route Server Peer resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_vpc_route_server_peer:
    test:
      route_server_endpoint_id: ${aws_vpc_route_server_endpoint.example.route_server_endpoint_id}
      peer_address: 10.0.1.250
      bgp_options:
        peer_asn: 65200
      tags:
        Name: Appliance 1
```

## Complete Configuration

```yaml
resource:
  aws_vpc_route_server:
    test:
      amazon_side_asn: 4294967294
      tags:
        Name: Test

resource:
  aws_vpc_route_server_association:
    test:
      route_server_id: ${aws_vpc_route_server.test.route_server_id}
      vpc_id: ${aws_vpc.test.id}

resource:
  aws_vpc_route_server_endpoint:
    test:
      route_server_id: ${aws_vpc_route_server.test.route_server_id}
      subnet_id: ${aws_subnet.test.id}
      tags:
        Name: Test Endpoint
      depends_on: 
        - ${aws_vpc_route_server_association.test}

resource:
  aws_vpc_route_server_propagation:
    test:
      route_server_id: ${aws_vpc_route_server.test.route_server_id}
      route_table_id: ${aws_route_table.test.id}
      depends_on: 
        - ${aws_vpc_route_server_association.test}

resource:
  aws_vpc_route_server_peer:
    test:
      route_server_endpoint_id: ${aws_vpc_route_server_endpoint.test.route_server_endpoint_id}
      peer_address: 10.0.1.250
      bgp_options:
        peer_asn: 65000
        peer_liveness_detection: bgp-keepalive
      tags:
        Name: Test Appliance
```
