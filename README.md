# Zabbix-opensearch-lld-template
This  is  a Low level discovery of an opensearch cluster.

## How to use
 Upload / Import the Template.yaml to get the base of the template and then you can update each template individually.
***

# Zabbix Template Documentation

## Opensearch Basic Node Monitoring

* **Template Name:** Opensearch Basic Node Monitoring
* **Description:** This template is automatically added to Opensearch LLD discovered hosts. It contains system-wide specifications that are not dependent on the node's role.
* **Vendor:** moesgaardsdk, version 7.0-0
* **Template Group:** Opensearch

### Items

| Name | Key | Type | Description/Details |
| :--- | :--- | :--- | :--- |
| Opensearch Discover basic discovery | `opensearch.discover.nodes.basic.stats` | SCRIPT | Retrieves basic node statistics via an HTTP request. Value type is TEXT. |
| Opensearch tasks | `opensearch.discover.nodes.basic.tasks` | SCRIPT | Retrieves tasks for a specific node via an HTTP request. Value type is TEXT. |
| JVM Memory pools old used in bytes | `opensearch.host..jvm.mem.pools.old.used_in_bytes` | DEPENDENT | Monitors the amount of memory used by the JVM's "old" memory pool. |
| JVM Memory pools survivor used in bytes | `opensearch.host..jvm.mem.pools.survivor.used_in_bytes` | DEPENDENT | Monitors the amount of memory used by the JVM's "survivor" memory pool. |
| JVM Memory pools young used in bytes | `opensearch.host..jvm.mem.pools.young.used_in_bytes` | DEPENDENT | Monitors the amount of memory used by the JVM's "young" memory pool. |
| JVM System Uptime | `opensearch.host..jvm.uptime_in_millis` | DEPENDENT | Measures the uptime of the JVM. |
| FS IO stats read operrations | `opensearch.host.fs.io_stats.total.read_operations` | DEPENDENT | Tracks the total number of read operations on the filesystem. |
| FS IO stats read time in ms | `opensearch.host.fs.io_stats.total.read_time` | DEPENDENT | Tracks the total time spent on read operations on the filesystem. |
| FS IO stats write operrations | `opensearch.host.fs.io_stats.total.write_operations` | DEPENDENT | Tracks the total number of write operations on the filesystem. |
| FS IO stat write time in ms | `opensearch.host.fs.io_stats.total.write_time` | DEPENDENT | Tracks the total time spent on write operations on the filesystem. |
| FS total free in bytes | `opensearch.host.fs.total.free_in_bytes` | DEPENDENT | Measures the total free space on the filesystem. |
| JVM Memory Heap Max | `opensearch.host.jvm.mem.heap_max_in_bytes` | DEPENDENT | Monitors the maximum available heap memory for the JVM. |
| JVM Memory Heap Used | `opensearch.host.jvm.mem.heap_used_in_bytes` | DEPENDENT | Monitors the current amount of used heap memory for the JVM. |
| OS CPU Load avg 1 min | `opensearch.host.os.cpu.load_average.1m` | DEPENDENT | Measures the average CPU load over the last 1 minute. |
| OS CPU Load avg 5 min | `opensearch.host.os.cpu.load_average.5m` | DEPENDENT | Measures the average CPU load over the last 5 minutes. |
| OS CPU Load avg 15 min | `opensearch.host.os.cpu.load_average.15m` | DEPENDENT | Measures the average CPU load over the last 15 minutes. |
| OS CPU percent used | `opensearch.host.os.cpu.persent` | DEPENDENT | Measures the percentage of CPU used by the OS. |
| OS Memory Used | `opensearch.host.os.mem.used_in_bytes` | DEPENDENT | Measures the total amount of memory used by the OS. |

### Discovery Rules

| Name | Key | Discovered Items |
| :--- | :--- | :--- |
| Thread pool low level discovery | `opensearch.lld.host.thread_pool` | `opensearch.host.thread_pool.active[{#NAME}]`, `opensearch.host.thread_pool.queue[{#NAME}]`, `opensearch.host.thread_pool.rejected[{#NAME}]`, `opensearch.host.thread_pool.threads[{#NAME}]`. |
| Garbage Collector | `opensearch.lld.jvm.gc.collector` | `opensearch.lld.host.jvm.gc.collectors.collection_count[{#NAME}]`, `opensearch.lld.host.jvm.gc.collectors.collection_time_in_millis[{#NAME}]`. |

***

## Opensearch Cluster Discovery

* **Template Name:** Opensearch Cluster Discovery
* **Description:** This template creates LLD hosts for each node and assigns a template according to their roles, whether dedicated or mixed.
* **Vendor:** moesgaardsdk, version 7.0-0
* **Template Group:** Opensearch

### Items

| Name | Key | Type | Description/Details |
| :--- | :--- | :--- | :--- |
| Opensearch get index stats | `opensearch.cluster.index.stats` | SCRIPT | Retrieves primary index statistics for the cluster. |
| Docs Count | `opensearch.cluster.indices.stats.docs.count` | DEPENDENT | Monitors the number of documents in the cluster. |
| Docs Deleted | `opensearch.cluster.indices.stats.docs.deleted` | DEPENDENT | Monitors the number of documents deleted from the cluster. |
| Indexing index failed | `opensearch.cluster.indices.stats.indexing.index_failed` | DEPENDENT | Tracks the number of failed indexing operations. |
| Indexing is throttled | `opensearch.cluster.indices.stats.indexing.is_throttled` | DEPENDENT | Checks if indexing is being throttled. |
| Query Cache cache count | `opensearch.cluster.indices.stats.query_cache.cache_count` | DEPENDENT | Counts the number of query caches. |
| Query Cache evictions count | `opensearch.cluster.indices.stats.query_cache.evictions` | DEPENDENT | Counts the number of query cache evictions. |
| Query Cache hit count | `opensearch.cluster.indices.stats.query_cache.hit_count` | DEPENDENT | Counts the number of query cache hits. |
| Query Cache miss count | `opensearch.cluster.indices.stats.query_cache.miss_count` | DEPENDENT | Counts the number of query cache misses. |
| Request cache count | `opensearch.cluster.indices.stats.request_cache.cache_count` | DEPENDENT | Counts the number of request caches. |
| Request cache eviction | `opensearch.cluster.indices.stats.request_cache.evictions` | DEPENDENT | Counts the number of request cache evictions. |
| Request cache hits | `opensearch.cluster.indices.stats.request_cache.hits_count` | DEPENDENT | Counts the number of request cache hits. |
| Request cache miss | `opensearch.cluster.indices.stats.request_cache.miss_count` | DEPENDENT | Counts the number of request cache misses. |
| Opensearch get fs stats | `opensearch.cluster.nodes.fs.metric` | SCRIPT | Retrieves filesystem statistics for nodes in the cluster. |
| Opensearch get cluster stats | `opensearch.cluster.stats` | SCRIPT | Retrieves cluster health status. |
| Opensearch Discover nodes in cluster | `opensearch.discover.nodes` | SCRIPT | Discovers nodes within the cluster. |
| Opensearch Discover nodes LLD in cluster | `opensearch.discover.nodes.list` | SCRIPT | Discovers nodes for Low-Level Discovery (LLD) within the cluster. |
| Opensearch Discover true master in cluster | `opensearch.discover.true.master` | SCRIPT | Identifies the active master node in the cluster. |

### Discovery Rules

| Name | Key | Discovered Items |
| :--- | :--- | :--- |
| Opensearch file system stats for dashboard | `opensearch.discover.fs.related` | `opensearch.lld.fs.total[{#NAME}]`. |
| Opensearch information Discovery | `opensearch.discover.status` | `opensearch.cluster.active_primary_shards[{#CLUSTERNAME}]`, `opensearch.cluster.active_shards[{#CLUSTERNAME}]`, `opensearch.cluster.active_shards_percent_as_number[{#CLUSTERNAME}]`, `opensearch.cluster.delayed_unassigned_shards[{#CLUSTERNAME}]`, `opensearch.cluster.initializing_shards[{#CLUSTERNAME}]`, `opensearch.cluster.number_data_nodes[{#CLUSTERNAME}]`, `opensearch.cluster.number_nodes[{#CLUSTERNAME}]`, `opensearch.cluster.number_of_pending_tasks[{#CLUSTERNAME}]`, `opensearch.cluster.relocating_shards[{#CLUSTERNAME}]`, `opensearch.cluster.status[{#CLUSTERNAME}]`. |

***

## Opensearch Data Node

* **Template Name:** Opensearch Data Node
* **Description:** This template is automatically applied to Opensearch data nodes discovered by LLD.
* **Vendor:** moesgaardsdk, version 7.0-0
* **Template Group:** Opensearch

### Items

| Name | Key | Type | Description/Details |
| :--- | :--- | :--- | :--- |
| Disk read in bytes/s | `opensearch.host.fs.total.read_in_bytes` | DEPENDENT | Monitors the rate of disk reads in bytes per second. |
| Disk write in bytes/s | `opensearch.host.fs.total.write_in_bytes` | DEPENDENT | Monitors the rate of disk writes in bytes per second. |
| Shards per node | `opensearch.host.indices.shards` | DEPENDENT | Counts the number of shards on the node. |
| Documents on disk | `opensearch.host.indices.docs.count` | DEPENDENT | Counts the number of documents on disk. |
| Documents on disk deleted | `opensearch.host.indices.docs.deleted` | DEPENDENT | Counts the number of deleted documents on disk. |
| Store size in bytes | `opensearch.host.indices.store.size_in_bytes` | DEPENDENT | Measures the size of the storage in bytes. |
| Indexing index total | `opensearch.host.indices.indexing.index_total` | DEPENDENT | Tracks the total number of indexing operations. |
| Indexing index current | `opensearch.host.indices.indexing.index_current` | DEPENDENT | Tracks the number of current indexing operations. |
| Search query total | `opensearch.host.indices.search.query_total` | DEPENDENT | Tracks the total number of search queries. |
| Search query time in millis | `opensearch.host.indices.search.query_time_in_millis` | DEPENDENT | Measures the time spent on search queries. |
| Search fetch total | `opensearch.host.indices.search.fetch_total` | DEPENDENT | Tracks the total number of fetch operations for searches. |
| Search fetch time in millis | `opensearch.host.indices.search.fetch_time_in_millis` | DEPENDENT | Measures the time spent on fetch operations for searches. |

### Discovery Rules

| Name | Key | Discovered Items |
| :--- | :--- | :--- |
| Opensearch FS stats for dashboard | `opensearch.discover.fs` | `opensearch.lld.fs.total[{#NAME}]`. |

***

## Opensearch Master Node

* **Template Name:** Opensearch Master Node
* **Description:** This template is automatically applied to Opensearch master nodes discovered by LLD.
* **Vendor:** moesgaardsdk, version 7.0-0
* **Template Group:** Opensearch

### Items

| Name | Key | Type | Description/Details |
| :--- | :--- | :--- | :--- |
| Cluster health | `opensearch.cluster.health` | SCRIPT | Retrieves the cluster health status from the master node. |
| Indexing index failed | `opensearch.cluster.indices.stats.indexing.index_failed` | DEPENDENT | Tracks the number of failed indexing operations in the cluster. |
| Pending tasks | `opensearch.cluster.pending_tasks` | SCRIPT | Retrieves the number of pending tasks in the cluster. |

***

## Opensearch Ingest Node

* **Template Name:** Opensearch Ingest Node
* **Description:** This template is automatically applied to Opensearch ingest nodes discovered by LLD.
* **Vendor:** moesgaardsdk, version 7.0-0
* **Template Group:** Opensearch

### Items

| Name | Key | Type | Description/Details |
| :--- | :--- | :--- | :--- |
| Ingest pipelines total | `opensearch.host.ingest.total` | DEPENDENT | Monitors the total number of documents processed by ingest pipelines. |
| Ingest pipelines time in millis | `opensearch.host.ingest.time_in_millis` | DEPENDENT | Measures the total time spent processing ingest pipelines. |
| Ingest pipelines current | `opensearch.host.ingest.current` | DEPENDENT | Tracks the number of documents currently being processed by ingest pipelines. |
| Ingest pipelines failed | `opensearch.host.ingest.failed` | DEPENDENT | Counts the number of failed ingest pipeline operations. |

***

## Opensearch Coordinating Node

* **Template Name:** Opensearch Coordinating Node
* **Description:** This template is automatically applied to Opensearch coordinating nodes discovered by LLD.
* **Vendor:** moesgaardsdk, version 7.0-0
* **Template Group:** Opensearch

### Items

| Name | Key | Type | Description/Details |
| :--- | :--- | :--- | :--- |
| Indexing index total | `opensearch.host.indices.indexing.index_total` | DEPENDENT | Tracks the total number of indexing operations. |
| Indexing index current | `opensearch.host.indices.indexing.index_current` | DEPENDENT | Tracks the number of current indexing operations. |
| Search query total | `opensearch.host.indices.search.query_total` | DEPENDENT | Tracks the total number of search queries. |
| Search query time in millis | `opensearch.host.indices.search.query_time_in_millis` | DEPENDENT | Measures the time spent on search queries. |
| Search fetch total | `opensearch.host.indices.search.fetch_total` | DEPENDENT | Tracks the total number of fetch operations for searches. |
| Search fetch time in millis | `opensearch.host.indices.search.fetch_time_in_millis` | DEPENDENT | Measures the time spent on fetch operations for searches. |
| Disk read in bytes/s | `opensearch.host.fs.total.read_in_bytes` | DEPENDENT | Monitors the rate of disk reads in bytes per second. |
| Disk write in bytes/s | `opensearch.host.fs.total.write_in_bytes` | DEPENDENT | Monitors the rate of disk writes in bytes per second. |
=======
Upload / Import the Template.yaml to get the base of the template and then you can update each template individually.
The reason for this is to minimize custom edits.
So you can upload the Template.yaml as a start and then customize to your liking.
There is a standard alert for if the cluster is healthy.

## TODO
+ create Dashboard template
+ customize trigger for host type

Please come with suggestions that could be useful.
``` 
Recommended version of #Zabbix is 7.0 but 6.0+ should be able to do this aswell.

```
>>>>>>> 4b17fe931ee72f3954812103bc7f922b66924878
