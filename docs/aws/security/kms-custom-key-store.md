# KMS Custom Key Store

Manage KMS Custom Key Store resources using ytofu YAML.

## Basic Example

```yaml
resource:
  aws_kms_custom_key_store:
    test:
      cloud_hsm_cluster_id: example-cloud_hsm_cluster_id
      custom_key_store_name: kms-custom-key-store-test
      key_store_password: noplaintextpasswords1
      trust_anchor_certificate: file-content
```

## External Key Store (VPC)

```yaml
resource:
  aws_kms_custom_key_store:
    example:
      custom_key_store_name: example-vpc-xks
      custom_key_store_type: EXTERNAL_KEY_STORE
      xks_proxy_authentication_credential:
        access_key_id: example-ephemeral_access_key_id
        raw_secret_access_key: example-ephemeral_secret_access_key
      xks_proxy_connectivity: VPC_ENDPOINT_SERVICE
      xks_proxy_uri_endpoint: "https://myproxy-private.xks.example.com"
      xks_proxy_uri_path: /kms/xks/v1
      xks_proxy_vpc_endpoint_service_name: com.amazonaws.vpce.us-east-1.vpce-svc-example
```

## External Key Store (Public)

```yaml
resource:
  aws_kms_custom_key_store:
    example:
      custom_key_store_name: example-public-xks
      custom_key_store_type: EXTERNAL_KEY_STORE
      xks_proxy_authentication_credential:
        access_key_id: example-ephemeral_access_key_id
        raw_secret_access_key: example-ephemeral_secret_access_key
      xks_proxy_connectivity: PUBLIC_ENDPOINT
      xks_proxy_uri_endpoint: "https://myproxy.xks.example.com"
      xks_proxy_uri_path: /kms/xks/v1
```
