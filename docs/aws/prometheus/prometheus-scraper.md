# Prometheus Scraper

Manage Prometheus Scraper resources using ytofu YAML.

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

resource:
  aws_prometheus_scraper:
    example:
      source:
        eks:
          cluster_arn: ${data.aws_eks_cluster.example.arn}
          subnet_ids: ${data.aws_eks_cluster.example.vpc_config[0].subnet_ids}
      scrape_configuration: ...
      destination:
        amp:
          workspace_arn: ${aws_prometheus_workspace.example.arn}
```

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
