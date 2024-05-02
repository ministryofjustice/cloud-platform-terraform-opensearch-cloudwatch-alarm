# cloud-platform-terraform-opensearch-cloudwatch-alarm

[![Releases](https://img.shields.io/github/release/ministryofjustice/cloud-platform-terraform-opensearch-cloudwatch-alarm/all.svg?style=flat-square)](https://github.com/ministryofjustice/cloud-platform-terraform-opensearch-cloudwatch-alarm/releases)

This Terraform module will create [OpenSearch CloudWatch alarm](https://docs.aws.amazon.com/opensearch-service/latest/developerguide/cloudwatch-alarms.html) for use on the Cloud Platform.

## Usage

```hcl
module "opensearch_cloudwatch_alarm" {
  source              = "github.com/ministryofjustice/cloud-platform-terraform-opensearch-cloudwatch-alarm?ref=version" # use the latest release

  alarm_name_prefix   = local.<os_domain_name>
  domain_name         = local.<os_domain_name>
  sns_topic           = module.baselines.slack_sns_topic
  min_available_nodes = aws_opensearch_domain.<os_domain_name>.cluster_config[0].instance_count
  tags                = local.logs_tags
}
```


| Metric name                    | Statistic | Period (second) | ComparisonOperator            | Threshold | EvaluationPeriods |
|--------------------------------|-----------|-----------------| ------------------------------|-----------|-------------------|
| ClusterStatus.red              | Maximum   | 60              | GreaterThanOrEqualToThreshold | 1         | 1                 |
| ClusterStatus.yellow           | Maximum   | 60              | GreaterThanOrEqualToThreshold | 1         | 1                 |
| FreeStorageSpace               | Minimum   | 60              | LessThanOrEqualToThreshold    | 20480     | 1                 |
| ClusterIndexWritesBlocked      | Maximum   | 300             | GreaterThanOrEqualToThreshold | 1         | 1                 |
| Nodes                          | Minimum   | 86400           | LessThanThreshold             | 1         | 1                 |
| AutomatedSnapshotFailure       | Maximum   | 60              | GreaterThanOrEqualToThreshold | 1         | 1                 |
| CPUUtilization                 | Maximum   | 900             | GreaterThanOrEqualToThreshold | 80        | 3                 |
| JVMMemoryPressure              | Maximum   | 60              | GreaterThanOrEqualToThreshold | 95        | 3                 |
| MasterCPUUtilization           | Maximum   | 900             | GreaterThanOrEqualToThreshold | 50        | 3                 |
| MasterJVMMemoryPressure        | Maximum   | 60              | GreaterThanOrEqualToThreshold | 95        | 3                 |
| KMSKeyError                    | Maximum   | 60              | GreaterThanOrEqualToThreshold | 1         | 1                 |
| KMSKeyInaccessible             | Maximum   | 60              | GreaterThanOrEqualToThreshold | 1         | 1                 |
| Shards.active                  | Maximum   | 60              | GreaterThanOrEqualToThreshold | 30000     | 1                 |
| MasterReachableFromNode        | Maximum   | 86400           | LessThanThreshold             | 1         | 1                 |
| ThreadpoolWriteQueue           | Average   | 60              | GreaterThanOrEqualToThreshold | 100       | 3                 |
| ThreadpoolSearchQueue          | Average   | 60              | GreaterThanOrEqualToThreshold | 500       | 1                 |
| ThreadpoolSearchQueue          | Maximum   | 60              | GreaterThanOrEqualToThreshold | 5000      | 1                 |
| ThreadpoolWriteRejected        | Maximum   | 60              | GreaterThanOrEqualToThreshold | 1         | 1                 |
| ThreadpoolSearchRejected       | Maximum   | 60              | GreaterThanOrEqualToThreshold | 1         | 1                 |



<!-- BEGIN_TF_DOCS -->
## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >= 1.2.5 |

## Providers

| Name | Version |
|------|---------|
| <a name="provider_aws"></a> [aws](#provider\_aws) | n/a |

## Modules

No modules.

## Resources

| Name | Type |
|------|------|
| [aws_cloudwatch_metric_alarm.automated_snapshot_failure](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/cloudwatch_metric_alarm) | resource |
| [aws_cloudwatch_metric_alarm.cluster_index_writes_blocked](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/cloudwatch_metric_alarm) | resource |
| [aws_cloudwatch_metric_alarm.cluster_status_is_red](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/cloudwatch_metric_alarm) | resource |
| [aws_cloudwatch_metric_alarm.cluster_status_is_yellow](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/cloudwatch_metric_alarm) | resource |
| [aws_cloudwatch_metric_alarm.cpu_utilization_too_high](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/cloudwatch_metric_alarm) | resource |
| [aws_cloudwatch_metric_alarm.free_storage_space_too_low](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/cloudwatch_metric_alarm) | resource |
| [aws_cloudwatch_metric_alarm.free_storage_space_total_too_low](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/cloudwatch_metric_alarm) | resource |
| [aws_cloudwatch_metric_alarm.insufficient_available_nodes](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/cloudwatch_metric_alarm) | resource |
| [aws_cloudwatch_metric_alarm.jvm_memory_pressure_too_high](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/cloudwatch_metric_alarm) | resource |
| [aws_cloudwatch_metric_alarm.kms_key_error](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/cloudwatch_metric_alarm) | resource |
| [aws_cloudwatch_metric_alarm.kms_key_inaccessible](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/cloudwatch_metric_alarm) | resource |
| [aws_cloudwatch_metric_alarm.master_cpu_utilization_too_high](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/cloudwatch_metric_alarm) | resource |
| [aws_cloudwatch_metric_alarm.master_jvm_memory_pressure_too_high](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/cloudwatch_metric_alarm) | resource |
| [aws_cloudwatch_metric_alarm.shards_active_too_high](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/cloudwatch_metric_alarm) | resource |
| [aws_cloudwatch_metric_alarm.threadpool_search_queue_average](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/cloudwatch_metric_alarm) | resource |
| [aws_cloudwatch_metric_alarm.threadpool_search_queue_max](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/cloudwatch_metric_alarm) | resource |
| [aws_cloudwatch_metric_alarm.threadpool_search_rejected](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/cloudwatch_metric_alarm) | resource |
| [aws_cloudwatch_metric_alarm.threadpool_write_queue_too_high](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/cloudwatch_metric_alarm) | resource |
| [aws_cloudwatch_metric_alarm.threadpool_write_rejected](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/cloudwatch_metric_alarm) | resource |
| [aws_cloudwatch_metric_alarm.unreachable_master_node](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/cloudwatch_metric_alarm) | resource |
| [aws_caller_identity.default](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/caller_identity) | data source |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_alarm_automated_snapshot_failure_period"></a> [alarm\_automated\_snapshot\_failure\_period](#input\_alarm\_automated\_snapshot\_failure\_period) | The period of the automated snapshot failure. The statistics should be applied in seconds | `number` | `60` | no |
| <a name="input_alarm_automated_snapshot_failure_periods"></a> [alarm\_automated\_snapshot\_failure\_periods](#input\_alarm\_automated\_snapshot\_failure\_periods) | The number of periods to alert that automatic snapshots failed.  Default: 1, raise this to be less noisy, as this can occur often for only 1 period | `number` | `1` | no |
| <a name="input_alarm_cluster_index_writes_blocked_period"></a> [alarm\_cluster\_index\_writes\_blocked\_period](#input\_alarm\_cluster\_index\_writes\_blocked\_period) | The period of the cluster index writes being blocked. The statistics should be applied in seconds | `number` | `300` | no |
| <a name="input_alarm_cluster_index_writes_blocked_periods"></a> [alarm\_cluster\_index\_writes\_blocked\_periods](#input\_alarm\_cluster\_index\_writes\_blocked\_periods) | The number of periods to alert that cluster index writes are blocked.  Default: 1, raise this to be less noisy, as this can occur often for only 1 period | `number` | `1` | no |
| <a name="input_alarm_cluster_status_is_red_period"></a> [alarm\_cluster\_status\_is\_red\_period](#input\_alarm\_cluster\_status\_is\_red\_period) | The period of the cluster status is in red. The statistics should be applied in seconds | `number` | `60` | no |
| <a name="input_alarm_cluster_status_is_red_periods"></a> [alarm\_cluster\_status\_is\_red\_periods](#input\_alarm\_cluster\_status\_is\_red\_periods) | The number of periods to alert that cluster status is red.  Default: 1, raise this to be less noisy, as this can occur often for only 1 period | `number` | `1` | no |
| <a name="input_alarm_cluster_status_is_yellow_period"></a> [alarm\_cluster\_status\_is\_yellow\_period](#input\_alarm\_cluster\_status\_is\_yellow\_period) | The period of the cluster status is in yellow. The statistics should be applied in seconds | `number` | `60` | no |
| <a name="input_alarm_cluster_status_is_yellow_periods"></a> [alarm\_cluster\_status\_is\_yellow\_periods](#input\_alarm\_cluster\_status\_is\_yellow\_periods) | The number of periods to alert that cluster status is yellow.  Default: 1, raise this to be less noisy, as this can occur often for only 1 period | `number` | `1` | no |
| <a name="input_alarm_cpu_utilization_too_high_period"></a> [alarm\_cpu\_utilization\_too\_high\_period](#input\_alarm\_cpu\_utilization\_too\_high\_period) | The period of the CPU utilization is too high. The statistics should be applied in seconds | `number` | `900` | no |
| <a name="input_alarm_cpu_utilization_too_high_periods"></a> [alarm\_cpu\_utilization\_too\_high\_periods](#input\_alarm\_cpu\_utilization\_too\_high\_periods) | The number of periods to alert that CPU usage is too high.  Default: 3, raise this to be less noisy, as this can occur often for only 1 period | `number` | `3` | no |
| <a name="input_alarm_free_storage_space_too_low_period"></a> [alarm\_free\_storage\_space\_too\_low\_period](#input\_alarm\_free\_storage\_space\_too\_low\_period) | The period of the per-node free storage is too low. The statistics should be applied in seconds | `number` | `60` | no |
| <a name="input_alarm_free_storage_space_too_low_periods"></a> [alarm\_free\_storage\_space\_too\_low\_periods](#input\_alarm\_free\_storage\_space\_too\_low\_periods) | The number of periods to alert that the per-node free storage space is too low.  Default: 1, raise this to be less noisy, as this can occur often for only 1 period | `number` | `1` | no |
| <a name="input_alarm_free_storage_space_total_too_low_period"></a> [alarm\_free\_storage\_space\_total\_too\_low\_period](#input\_alarm\_free\_storage\_space\_total\_too\_low\_period) | The period of the total cluster free storage is too low. The statistics should be applied in seconds | `number` | `60` | no |
| <a name="input_alarm_free_storage_space_total_too_low_periods"></a> [alarm\_free\_storage\_space\_total\_too\_low\_periods](#input\_alarm\_free\_storage\_space\_total\_too\_low\_periods) | The number of periods to alert that total cluster free storage space is too low.  Default: 1, raise this to be less noisy, as this can occur often for only 1 period | `number` | `1` | no |
| <a name="input_alarm_jvm_memory_pressure_too_high_period"></a> [alarm\_jvm\_memory\_pressure\_too\_high\_period](#input\_alarm\_jvm\_memory\_pressure\_too\_high\_period) | The period of the JVM memory pressure is too high. The statistics should be applied in seconds | `number` | `900` | no |
| <a name="input_alarm_jvm_memory_pressure_too_high_periods"></a> [alarm\_jvm\_memory\_pressure\_too\_high\_periods](#input\_alarm\_jvm\_memory\_pressure\_too\_high\_periods) | The number of periods which it must be in the alarmed state to alert | `number` | `1` | no |
| <a name="input_alarm_kms_period"></a> [alarm\_kms\_period](#input\_alarm\_kms\_period) | The period of the KMS-related metrics. The statistics should be applied in seconds | `number` | `60` | no |
| <a name="input_alarm_kms_periods"></a> [alarm\_kms\_periods](#input\_alarm\_kms\_periods) | The number of periods to alert that kms has failed.  Default: 1, raise this to be less noisy, as this can occur often for only 1 period | `number` | `1` | no |
| <a name="input_alarm_master_cpu_utilization_too_high_period"></a> [alarm\_master\_cpu\_utilization\_too\_high\_period](#input\_alarm\_master\_cpu\_utilization\_too\_high\_period) | The period of the CPU utilization of master nodes are too high. The statistics should be applied in seconds | `number` | `900` | no |
| <a name="input_alarm_master_cpu_utilization_too_high_periods"></a> [alarm\_master\_cpu\_utilization\_too\_high\_periods](#input\_alarm\_master\_cpu\_utilization\_too\_high\_periods) | The number of periods to alert that masters CPU usage is too high.  Default: 3, raise this to be less noisy, as this can occur often for only 1 period | `number` | `3` | no |
| <a name="input_alarm_master_jvm_memory_pressure_too_high_period"></a> [alarm\_master\_jvm\_memory\_pressure\_too\_high\_period](#input\_alarm\_master\_jvm\_memory\_pressure\_too\_high\_period) | The period of the JVM memory pressure of master nodes are too high. The statistics should be applied in seconds | `number` | `900` | no |
| <a name="input_alarm_master_jvm_memory_pressure_too_high_periods"></a> [alarm\_master\_jvm\_memory\_pressure\_too\_high\_periods](#input\_alarm\_master\_jvm\_memory\_pressure\_too\_high\_periods) | The number of periods which it must be in the alarmed state to alert | `number` | `1` | no |
| <a name="input_alarm_min_available_nodes_period"></a> [alarm\_min\_available\_nodes\_period](#input\_alarm\_min\_available\_nodes\_period) | The period of the minimum available nodes. The statistics should be applied in seconds | `number` | `86400` | no |
| <a name="input_alarm_min_available_nodes_periods"></a> [alarm\_min\_available\_nodes\_periods](#input\_alarm\_min\_available\_nodes\_periods) | The number of periods to alert that minimum number of available nodes dropped below a threshold.  Default: 1, raise this to be less noisy, as this can occur often for only 1 period | `number` | `1` | no |
| <a name="input_alarm_name_postfix"></a> [alarm\_name\_postfix](#input\_alarm\_name\_postfix) | Alarm name suffix, used in the naming of alarms created | `string` | `""` | no |
| <a name="input_alarm_name_prefix"></a> [alarm\_name\_prefix](#input\_alarm\_name\_prefix) | Alarm name prefix, used in the naming of alarms created | `string` | `""` | no |
| <a name="input_alarm_shard_active_number_too_high_period"></a> [alarm\_shard\_active\_number\_too\_high\_period](#input\_alarm\_shard\_active\_number\_too\_high\_period) | The period of the active shard number are too high. The statistics should be applied in seconds | `number` | `60` | no |
| <a name="input_alarm_shard_active_number_too_high_periods"></a> [alarm\_shard\_active\_number\_too\_high\_periods](#input\_alarm\_shard\_active\_number\_too\_high\_periods) | The number of periods to alert that active shard number is too high.  Default: 1, raise this to be less noisy, as this can occur often for only 1 period | `number` | `1` | no |
| <a name="input_alarm_threadpool_search_queue_too_high_period"></a> [alarm\_threadpool\_search\_queue\_too\_high\_period](#input\_alarm\_threadpool\_search\_queue\_too\_high\_period) | The period of the threadpool search queue is too high. The statistics should be applied in seconds | `number` | `60` | no |
| <a name="input_alarm_threadpool_search_queue_too_high_periods"></a> [alarm\_threadpool\_search\_queue\_too\_high\_periods](#input\_alarm\_threadpool\_search\_queue\_too\_high\_periods) | The number of periods to alert that threadpool search queue is too high.  Default: 1, raise this to be less noisy, as this can occur often for only 1 period | `number` | `1` | no |
| <a name="input_alarm_threadpool_search_rejected_period"></a> [alarm\_threadpool\_search\_rejected\_period](#input\_alarm\_threadpool\_search\_rejected\_period) | The period of the threadpool search queue rejected is increasing. The statistics should be applied in seconds | `number` | `60` | no |
| <a name="input_alarm_threadpool_search_rejected_periods"></a> [alarm\_threadpool\_search\_rejected\_periods](#input\_alarm\_threadpool\_search\_rejected\_periods) | The number of periods to alert that threadpool write queue rejected is increasing.  Default: 1, raise this to be less noisy, as this can occur often for only 1 period | `number` | `1` | no |
| <a name="input_alarm_threadpool_write_queue_too_high_period"></a> [alarm\_threadpool\_write\_queue\_too\_high\_period](#input\_alarm\_threadpool\_write\_queue\_too\_high\_period) | The period of the threadpool write queue is too high. The statistics should be applied in seconds | `number` | `60` | no |
| <a name="input_alarm_threadpool_write_queue_too_high_periods"></a> [alarm\_threadpool\_write\_queue\_too\_high\_periods](#input\_alarm\_threadpool\_write\_queue\_too\_high\_periods) | The number of periods to alert that threadpool write queue is too high.  Default: 1, raise this to be less noisy, as this can occur often for only 1 period | `number` | `1` | no |
| <a name="input_alarm_threadpool_write_rejected_period"></a> [alarm\_threadpool\_write\_rejected\_period](#input\_alarm\_threadpool\_write\_rejected\_period) | The period of the threadpool write queue rejected is increasing. The statistics should be applied in seconds | `number` | `60` | no |
| <a name="input_alarm_threadpool_write_rejected_periods"></a> [alarm\_threadpool\_write\_rejected\_periods](#input\_alarm\_threadpool\_write\_rejected\_periods) | The number of periods to alert that threadpool write queue rejected is increasing.  Default: 1, raise this to be less noisy, as this can occur often for only 1 period | `number` | `1` | no |
| <a name="input_alarm_unreachable_master_node_period"></a> [alarm\_unreachable\_master\_node\_period](#input\_alarm\_unreachable\_master\_node\_period) | The period of the master node is unreachable. The statistics should be applied in seconds | `number` | `86400` | no |
| <a name="input_alarm_unreachable_master_node_periods"></a> [alarm\_unreachable\_master\_node\_periods](#input\_alarm\_unreachable\_master\_node\_periods) | The number of periods to alert that master node is unreachable.  Default: 1, raise this to be less noisy, as this can occur often for only 1 period | `number` | `1` | no |
| <a name="input_cpu_utilization_threshold"></a> [cpu\_utilization\_threshold](#input\_cpu\_utilization\_threshold) | The maximum percentage of CPU utilization | `number` | `80` | no |
| <a name="input_domain_name"></a> [domain\_name](#input\_domain\_name) | The Elasticsearch domain name you want to monitor | `string` | n/a | yes |
| <a name="input_free_storage_space_threshold"></a> [free\_storage\_space\_threshold](#input\_free\_storage\_space\_threshold) | The minimum amount of available storage space in megabytes.  This is per-node. | `number` | `20480` | no |
| <a name="input_free_storage_space_total_threshold"></a> [free\_storage\_space\_total\_threshold](#input\_free\_storage\_space\_total\_threshold) | The minimum amount of available storage space in megabytes aggregated across your cluster (for multi-node).  This is an aggregate, typically use (free\_storage\_space\_threshold * min\_available\_nodes) | `number` | `20480` | no |
| <a name="input_jvm_memory_pressure_threshold"></a> [jvm\_memory\_pressure\_threshold](#input\_jvm\_memory\_pressure\_threshold) | The maximum percentage of the Java heap used for all data nodes in the cluster | `number` | `80` | no |
| <a name="input_master_cpu_utilization_threshold"></a> [master\_cpu\_utilization\_threshold](#input\_master\_cpu\_utilization\_threshold) | The maximum percentage of CPU utilization of master nodes | `number` | `80` | no |
| <a name="input_master_jvm_memory_pressure_threshold"></a> [master\_jvm\_memory\_pressure\_threshold](#input\_master\_jvm\_memory\_pressure\_threshold) | The maximum percentage of the Java heap used for master nodes in the cluster | `number` | `80` | no |
| <a name="input_min_available_nodes"></a> [min\_available\_nodes](#input\_min\_available\_nodes) | The minimum available (reachable) nodes to have, set to non-zero to enable | `number` | `0` | no |
| <a name="input_monitor_automated_snapshot_failure"></a> [monitor\_automated\_snapshot\_failure](#input\_monitor\_automated\_snapshot\_failure) | Enable monitoring of automated snapshot failure | `bool` | `true` | no |
| <a name="input_monitor_cluster_index_writes_blocked"></a> [monitor\_cluster\_index\_writes\_blocked](#input\_monitor\_cluster\_index\_writes\_blocked) | Enable monitoring of cluster index writes being blocked | `bool` | `true` | no |
| <a name="input_monitor_cluster_status_is_red"></a> [monitor\_cluster\_status\_is\_red](#input\_monitor\_cluster\_status\_is\_red) | Enable monitoring of cluster status is in red | `bool` | `true` | no |
| <a name="input_monitor_cluster_status_is_yellow"></a> [monitor\_cluster\_status\_is\_yellow](#input\_monitor\_cluster\_status\_is\_yellow) | Enable monitoring of cluster status is in yellow | `bool` | `true` | no |
| <a name="input_monitor_cpu_utilization_too_high"></a> [monitor\_cpu\_utilization\_too\_high](#input\_monitor\_cpu\_utilization\_too\_high) | Enable monitoring of CPU utilization is too high | `bool` | `true` | no |
| <a name="input_monitor_free_storage_space_too_low"></a> [monitor\_free\_storage\_space\_too\_low](#input\_monitor\_free\_storage\_space\_too\_low) | Enable monitoring of cluster per-node free storage is too low | `bool` | `true` | no |
| <a name="input_monitor_free_storage_space_total_too_low"></a> [monitor\_free\_storage\_space\_total\_too\_low](#input\_monitor\_free\_storage\_space\_total\_too\_low) | Enable monitoring of cluster total free storage is too low.  Disabled by default, if you set this you must set free\_storage\_space\_total\_threshold also | `bool` | `false` | no |
| <a name="input_monitor_jvm_memory_pressure_too_high"></a> [monitor\_jvm\_memory\_pressure\_too\_high](#input\_monitor\_jvm\_memory\_pressure\_too\_high) | Enable monitoring of JVM memory pressure is too high | `bool` | `true` | no |
| <a name="input_monitor_kms"></a> [monitor\_kms](#input\_monitor\_kms) | Enable monitoring of KMS-related metrics.  Only enable this when using KMS with ElasticSearch | `bool` | `true` | no |
| <a name="input_monitor_master_cpu_utilization_too_high"></a> [monitor\_master\_cpu\_utilization\_too\_high](#input\_monitor\_master\_cpu\_utilization\_too\_high) | Enable monitoring of CPU utilization of master nodes are too high. Only enable this when dedicated master is enabled | `bool` | `true` | no |
| <a name="input_monitor_master_jvm_memory_pressure_too_high"></a> [monitor\_master\_jvm\_memory\_pressure\_too\_high](#input\_monitor\_master\_jvm\_memory\_pressure\_too\_high) | Enable monitoring of JVM memory pressure of master nodes are too high. Only enable this wwhen dedicated master is enabled | `bool` | `true` | no |
| <a name="input_monitor_min_available_nodes"></a> [monitor\_min\_available\_nodes](#input\_monitor\_min\_available\_nodes) | Enable monitoring of minimum available nodes | `bool` | `true` | no |
| <a name="input_monitor_shard"></a> [monitor\_shard](#input\_monitor\_shard) | Enable monitoring of sharding of master nodes are too high. | `bool` | `true` | no |
| <a name="input_monitor_threadpool_search_queue"></a> [monitor\_threadpool\_search\_queue](#input\_monitor\_threadpool\_search\_queue) | Enable monitoring of threadpool search queue number is too high | `bool` | `true` | no |
| <a name="input_monitor_threadpool_search_rejected"></a> [monitor\_threadpool\_search\_rejected](#input\_monitor\_threadpool\_search\_rejected) | Enable monitoring of threadpool search queue rejected number is increasing | `bool` | `true` | no |
| <a name="input_monitor_threadpool_write_queue"></a> [monitor\_threadpool\_write\_queue](#input\_monitor\_threadpool\_write\_queue) | Enable monitoring of threadpool write queue number is too high. | `bool` | `true` | no |
| <a name="input_monitor_threadpool_write_rejected"></a> [monitor\_threadpool\_write\_rejected](#input\_monitor\_threadpool\_write\_rejected) | Enable monitoring of threadpool write queue rejected number is increasing | `bool` | `true` | no |
| <a name="input_monitor_unreachable_master_node"></a> [monitor\_unreachable\_master\_node](#input\_monitor\_unreachable\_master\_node) | Enable monitoring of master nodes are running and reachable. Only enable this wwhen dedicated master is enabled | `bool` | `true` | no |
| <a name="input_shard_active_number_threshold"></a> [shard\_active\_number\_threshold](#input\_shard\_active\_number\_threshold) | The maximum number of active primary and replica shards number | `number` | `30000` | no |
| <a name="input_sns_topic"></a> [sns\_topic](#input\_sns\_topic) | SNS topic you want to specify. If leave empty, it will use a prefix and a timestampe appended | `string` | `""` | no |
| <a name="input_tags"></a> [tags](#input\_tags) | A map of tags to add to all resources | `map(string)` | `{}` | no |
| <a name="input_threadpool_search_queue_average_threshold"></a> [threadpool\_search\_queue\_average\_threshold](#input\_threadpool\_search\_queue\_average\_threshold) | The average number of cluster searching concurrency | `number` | `500` | no |
| <a name="input_threadpool_search_queue_max_threshold"></a> [threadpool\_search\_queue\_max\_threshold](#input\_threadpool\_search\_queue\_max\_threshold) | The maximum number of cluster searching concurrency | `number` | `5000` | no |
| <a name="input_threadpool_search_rejected_threshold"></a> [threadpool\_search\_rejected\_threshold](#input\_threadpool\_search\_rejected\_threshold) | The number of cluster threadpool search rejected threshold. Value 1 means it is increasing | `number` | `1` | no |
| <a name="input_threadpool_write_queue_threshold"></a> [threadpool\_write\_queue\_threshold](#input\_threadpool\_write\_queue\_threshold) | The maximum number of cluster indexing concurrency | `number` | `100` | no |
| <a name="input_threadpool_write_rejected_threshold"></a> [threadpool\_write\_rejected\_threshold](#input\_threadpool\_write\_rejected\_threshold) | The number of cluster threadpool write rejected threshold. Value 1 means it is increasing | `number` | `1` | no |

## Outputs

No outputs.
<!-- END_TF_DOCS -->

## Tags

Some of the inputs for this module are tags. All infrastructure resources must be tagged to meet the MOJ Technical Guidance on [Documenting owners of infrastructure](https://technical-guidance.service.justice.gov.uk/documentation/standards/documenting-infrastructure-owners.html).

You should use your namespace variables to populate these. See the [Usage](#usage) section for more information.

## Reading Material

<!-- Add links to useful documentation -->

- [Cloud Platform user guide](https://user-guide.cloud-platform.service.justice.gov.uk/#cloud-platform-user-guide)
