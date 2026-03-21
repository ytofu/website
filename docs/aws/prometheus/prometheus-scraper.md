# Resource: aws_prometheus_scraper



## Basic Example

```yaml
resource:
  aws_prometheus_scraper:
    example:
      source:
        eks:
          cluster_arn: ${data.aws_eks_cluster.example.arn}
          subnet_ids: ${data.aws_eks_cluster.example.vpc_config[0].subnet_ids}
      destination:
        amp:
          workspace_arn: ${aws_prometheus_workspace.example.arn}
      scrape_configuration: |
        global:
        scrape_interval: 30s
        scrape_configs:
        # pod metrics
        - job_name: pod_exporter
        kubernetes_sd_configs:
        - role: pod
        # container metrics
        - job_name: cadvisor
        scheme: https
        authorization:
        credentials_file: /var/run/secrets/kubernetes.io/serviceaccount/token
        kubernetes_sd_configs:
        - role: node
        relabel_configs:
        - action: labelmap
        regex: __meta_kubernetes_node_label_(.+)
        - replacement: kubernetes.default.svc:443
        target_label: __address__
        - source_labels: [__meta_kubernetes_node_name]
        regex: (.+)
        target_label: __metrics_path__
        replacement: /api/v1/nodes/$1/proxy/metrics/cadvisor
        # apiserver metrics
        - bearer_token_file: /var/run/secrets/kubernetes.io/serviceaccount/token
        job_name: kubernetes-apiservers
        kubernetes_sd_configs:
        - role: endpoints
        relabel_configs:
        - action: keep
        regex: default;kubernetes;https
        source_labels:
        - __meta_kubernetes_namespace
        - __meta_kubernetes_service_name
        - __meta_kubernetes_endpoint_port_name
        scheme: https
        # kube proxy metrics
        - job_name: kube-proxy
        honor_labels: true
        kubernetes_sd_configs:
        - role: pod
        relabel_configs:
        - action: keep
        source_labels:
        - __meta_kubernetes_namespace
        - __meta_kubernetes_pod_name
        separator: '/'
        regex: 'kube-system/kube-proxy.+'
        - source_labels:
        - __address__
        action: replace
        target_label: __address__
        regex: (.+?)(\\:\\d+)?
        replacement: $1:10249
```

## Use default EKS scraper configuration

```yaml
data:
  aws_prometheus_default_scraper_configuration:
    example:

resource:
  aws_prometheus_scraper:
    example:
      destination:
        amp:
          workspace_arn: ${aws_prometheus_workspace.example.arn}
      scrape_configuration: ${data.aws_prometheus_scraper_configuration.example.configuration}
      source:
        eks:
          cluster_arn: ${data.aws_eks_cluster.example.arn}
          subnet_ids: ${data.aws_eks_cluster.example.vpc_config[0].subnet_ids}
```

## Ignoring changes to Prometheus Workspace destination

```yaml
data:
  aws_eks_cluster:
    this:
      name: example

resource:
  aws_prometheus_workspace:
    example:
      tags:
        AMPAgentlessScraper: 

  aws_prometheus_scraper:
    example:
      source:
        eks:
          cluster_arn: ${data.aws_eks_cluster.example.arn}
          subnet_ids: ${data.aws_eks_cluster.example.vpc_config[0].subnet_ids}
      scrape_configuration: ...
      destination:
        amp:
          workspace_arn: ${aws_prometheus_workspace.example.arn}```

## Cross-Account Configuration

```yaml
resource:
  aws_prometheus_scraper:
    example:
      source:
        eks:
          cluster_arn: ${data.aws_eks_cluster.example.arn}
          subnet_ids: ${data.aws_eks_cluster.example.vpc_config[0].subnet_ids}
      destination:
        amp:
          workspace_arn: <target_account_workspace_arn>
      role_configuration:
        source_role_arn: ${aws_iam_role.source.arn}
        target_role_arn: "arn:aws:iam::ACCOUNT-ID:role/target-role-name"
      scrape_configuration: ...
```

## Argument Reference

This resource supports the following arguments:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `destination` - (Required) Configuration block for the managed scraper to send metrics to. See [`destination`](#destination).
* `scrape_configuration` - (Required) The configuration file to use in the new scraper. For more information, see [Scraper configuration](https://docs.aws.amazon.com/prometheus/latest/userguide/AMP-collector-how-to.html#AMP-collector-configuration).
* `source` - (Required) Configuration block to specify where the managed scraper will collect metrics from. See [`source`](#source).

The following arguments are optional:

* `region` - (Optional) Region where this resource will be [managed](https://docs.aws.amazon.com/general/latest/gr/rande.html#regional-endpoints). Defaults to the Region set in the provider configuration.
* `alias` - (Optional) a name to associate with the managed scraper. This is for your use, and does not need to be unique.

* `role_configuration` - (Optional) Configuration block to enable writing to an Amazon Managed Service for Prometheus workspace in a different account. See [`role_configuration`](#role_configuration) below.

### `destination`

* `amp` - (Required) Configuration block for an Amazon Managed Prometheus workspace destination. See [`amp`](#amp).

### `amp`

* `workspace_arn` - (Required) The Amazon Resource Name (ARN) of the prometheus workspace.

### `source`

* `eks` - (Required) Configuration block for an EKS cluster source. See [`eks`](#eks).

#### `eks`

* `eks_cluster_arn` - (Required) The Amazon Resource Name (ARN) of the source EKS cluster.
* `subnet_ids` - (Required) List of subnet IDs. Must be in at least two different availability zones.
* `security_group_ids` - (Optional) List of the security group IDs for the Amazon EKS cluster VPC configuration.

### `role_configuration`

* `source_role_arn` - (Required) The Amazon Resource Name (ARN) of the source role configuration. Must be an IAM role ARN.
* `target_role_arn` - (Required) The Amazon Resource Name (ARN) of the target role configuration. Must be an IAM role ARN.

## Attribute Reference

This resource exports the following attributes in addition to the arguments above:

* `arn` - The Amazon Resource Name (ARN) of the new scraper.
* `role_arn` - The Amazon Resource Name (ARN) of the IAM role that provides permissions for the scraper to discover, collect, and produce metrics
* `status` - Status of the scraper. One of ACTIVE, CREATING, DELETING, CREATION_FAILED, DELETION_FAILED

## Timeouts

Configuration options:

* `create` - (Default `30m`)
* `update` - (Default `2m`)
* `delete` - (Default `20m`)

## Import

```bash
ytofu import aws_prometheus_scraper.example s-0123abc-0000-0123-a000-000000000000
```
