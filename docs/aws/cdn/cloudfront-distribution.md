# Cloudfront Distribution

Manage Cloudfront Distribution resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_s3_bucket:
    b:
      bucket: mybucket
      tags:
        Name: My bucket

data:
  aws_iam_policy_document:
    origin_bucket_policy:
      statement:
        sid: AllowCloudFrontServicePrincipalReadWrite
        effect: Allow
        principals:
          type: Service
          identifiers: 
            - cloudfront.amazonaws.com
        actions:
          - "s3:GetObject"
          - "s3:PutObject"
        resources:
          - "${aws_s3_bucket.b.arn}/*"
        condition:
          test: StringEquals
          values: 
            - ${aws_cloudfront_distribution.s3_distribution.arn}

resource:
  aws_s3_bucket_policy:
    b:
      bucket: ${aws_s3_bucket.b.bucket}
      policy: ${data.aws_iam_policy_document.origin_bucket_policy.json}

data:
  aws_acm_certificate:
    my_domain:
      region: us-east-1
      domain: "*.example-my_domain"
      statuses: 
        - ISSUED

resource:
  aws_cloudfront_origin_access_control:
    default:
      name: default-oac
      origin_access_control_origin_type: s3
      signing_behavior: always
      signing_protocol: sigv4

resource:
  aws_cloudfront_distribution:
    s3_distribution:
      origin:
        domain_name: ${aws_s3_bucket.b.bucket_regional_domain_name}
        origin_access_control_id: ${aws_cloudfront_origin_access_control.default.id}
        origin_id: example-s3_origin_id
      enabled: true
      is_ipv6_enabled: true
      comment: Some comment
      default_root_object: index.html
      aliases: 
        - "mysite.example-my_domain"
        - "yoursite.example-my_domain"
      default_cache_behavior:
        allowed_methods: 
          - DELETE
          - GET
          - HEAD
          - OPTIONS
          - PATCH
          - POST
          - PUT
        cached_methods: 
          - GET
          - HEAD
        target_origin_id: example-s3_origin_id
        forwarded_values:
          query_string: false
          cookies:
            forward: none
        viewer_protocol_policy: allow-all
        min_ttl: 0
        default_ttl: 3600
        max_ttl: 86400
      ordered_cache_behavior:
        path_pattern: "/content/immutable/*"
        allowed_methods: 
          - GET
          - HEAD
          - OPTIONS
        cached_methods: 
          - GET
          - HEAD
          - OPTIONS
        target_origin_id: example-s3_origin_id
        forwarded_values:
          query_string: false
          headers: 
            - Origin
          cookies:
            forward: none
        min_ttl: 0
        default_ttl: 86400
        max_ttl: 31536000
        compress: true
        viewer_protocol_policy: redirect-to-https
      ordered_cache_behavior:
        path_pattern: "/content/*"
        allowed_methods: 
          - GET
          - HEAD
          - OPTIONS
        cached_methods: 
          - GET
          - HEAD
        target_origin_id: example-s3_origin_id
        forwarded_values:
          query_string: false
          cookies:
            forward: none
        min_ttl: 0
        default_ttl: 3600
        max_ttl: 86400
        compress: true
        viewer_protocol_policy: redirect-to-https
      price_class: PriceClass_200
      restrictions:
        geo_restriction:
          restriction_type: whitelist
          locations: 
            - US
            - CA
            - GB
            - DE
      tags:
        Environment: production
      viewer_certificate:
        acm_certificate_arn: ${data.aws_acm_certificate.my_domain.arn}
        ssl_support_method: sni-only

data:
  aws_route53_zone:
    my_domain:
      name: example-my_domain

resource:
  aws_route53_record:
    cloudfront:
      zone_id: ${data.aws_route53_zone.my_domain.zone_id}
      name: example-value
      type: A
      alias:
        name: ${aws_cloudfront_distribution.s3_distribution.domain_name}
        zone_id: ${aws_cloudfront_distribution.s3_distribution.hosted_zone_id}
        evaluate_target_health: false
```

## With Failover Routing

```yaml
resource:
  aws_cloudfront_distribution:
    s3_distribution:
      origin_group:
        origin_id: groupS3
        failover_criteria:
          status_codes: 
            - 403
            - 404
            - 500
            - 502
        member:
          origin_id: primaryS3
        member:
          origin_id: failoverS3
      origin:
        domain_name: ${aws_s3_bucket.primary.bucket_regional_domain_name}
        origin_id: primaryS3
        s3_origin_config:
          origin_access_identity: ${aws_cloudfront_origin_access_identity.default.cloudfront_access_identity_path}
      origin:
        domain_name: ${aws_s3_bucket.failover.bucket_regional_domain_name}
        origin_id: failoverS3
        s3_origin_config:
          origin_access_identity: ${aws_cloudfront_origin_access_identity.default.cloudfront_access_identity_path}
      default_cache_behavior:
        target_origin_id: groupS3
```

## With Managed Caching Policy

```yaml
resource:
  aws_cloudfront_distribution:
    s3_distribution:
      origin:
        domain_name: ${aws_s3_bucket.primary.bucket_regional_domain_name}
        origin_id: myS3Origin
        s3_origin_config:
          origin_access_identity: ${aws_cloudfront_origin_access_identity.default.cloudfront_access_identity_path}
      enabled: true
      is_ipv6_enabled: true
      comment: Some comment
      default_root_object: index.html
      default_cache_behavior:
        cache_policy_id: 4135ea2d-6df8-44a3-9df3-4b5a84be39ad
        allowed_methods: 
          - GET
          - HEAD
          - OPTIONS
        cached_methods: 
          - GET
          - HEAD
        target_origin_id: example-s3_origin_id
        viewer_protocol_policy: allow-all
      restrictions:
        geo_restriction:
          restriction_type: whitelist
          locations: 
            - US
            - CA
            - GB
            - DE
      viewer_certificate:
        cloudfront_default_certificate: true
```

## With V2 logging to S3

```yaml
resource:
  aws_cloudfront_distribution:
    example:

resource:
  aws_cloudwatch_log_delivery_source:
    example:
      region: us-east-1
      name: example
      log_type: ACCESS_LOGS
      resource_arn: ${aws_cloudfront_distribution.example.arn}

resource:
  aws_s3_bucket:
    example:
      bucket: testbucket
      force_destroy: true

resource:
  aws_cloudwatch_log_delivery_destination:
    example:
      region: us-east-1
      name: s3-destination
      output_format: parquet
      delivery_destination_configuration:
        destination_resource_arn: "${aws_s3_bucket.example.arn}/prefix"

resource:
  aws_cloudwatch_log_delivery:
    example:
      region: us-east-1
      delivery_source_name: ${aws_cloudwatch_log_delivery_source.example.name}
      delivery_destination_arn: ${aws_cloudwatch_log_delivery_destination.example.arn}
      s3_delivery_configuration:
        suffix_path: "/123456678910/{DistributionId}/{yyyy}/{MM}/{dd}/{HH}"
```

## With V2 logging to Data Firehose

```yaml
resource:
  aws_cloudfront_distribution:
    example:

resource:
  aws_kinesis_firehose_delivery_stream:
    cloudfront_logs:
      region: us-east-1
      tags:
        LogDeliveryEnabled: true

resource:
  aws_cloudwatch_log_delivery_source:
    example:
      region: us-east-1
      name: cloudfront-logs-source
      log_type: ACCESS_LOGS
      resource_arn: ${aws_cloudfront_distribution.example.arn}

resource:
  aws_cloudwatch_log_delivery_destination:
    example:
      region: us-east-1
      name: firehose-destination
      output_format: json
      delivery_destination_configuration:
        destination_resource_arn: ${aws_kinesis_firehose_delivery_stream.cloudfront_logs.arn}

resource:
  aws_cloudwatch_log_delivery:
    example:
      region: us-east-1
      delivery_source_name: ${aws_cloudwatch_log_delivery_source.example.name}
      delivery_destination_arn: ${aws_cloudwatch_log_delivery_destination.example.arn}
```

## With Connection Function and Viewer mTLS

```yaml
resource:
  aws_cloudfront_connection_function:
    example:
      name: example-connection-function

resource:
  aws_cloudfront_trust_store:
    example:
      name: example-trust-store

resource:
  aws_cloudfront_distribution:
    example:
      connection_function_association:
        id: ${aws_cloudfront_connection_function.example.id}
      viewer_mtls_config:
        mode: verify
        trust_store_config:
          trust_store_id: ${aws_cloudfront_trust_store.example.id}
          advertise_trust_store_ca_names: true
          ignore_certificate_expiry: false
```
