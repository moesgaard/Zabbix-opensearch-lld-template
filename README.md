# Zabbix-opensearch-lld-template
This  is  a Low level discovery of an opensearch cluster.

## How to use
Upload / Import the opensearch_complete_templates.yaml to get the base of the template and then you can update each template individually.
The reason for this is to minimize custom edits.
So you can upload the opensearch_complete_templates.yaml as a start and then customize to your liking.
There is a standard alert for if the cluster is healthy.

## TODO
+ create Dashboard template
+ customize trigger for host type

Please come with suggestions that could be useful.
``` 
Recommended version of #Zabbix is 7.0 but 6.0+ should be able to do this aswell.

```

### **Opensearch Cluster Discovery**

* **Template Name:** Opensearch Cluster Discovery
* **Description:** This template creates an LLD host for each node and assigns a template according to the roles, either a dedicated role or mixed roles.
* **Vendor:** moesgaardsdk, version 7.0-0
* **Template Group:** Opensearch

---

#### **Items**

| Name | Key | Type |
| :--- | :--- | :--- |
| Opensearch get index stats | `opensearch.cluster.index.stats` | SCRIPT |
| Docs Count | `opensearch.cluster.indices.stats.docs.count` | DEPENDENT |
| Docs Deleted | `opensearch.cluster.indices.stats.docs.deleted` | DEPENDENT |
| Indexing index failed | `opensearch.cluster.indices.stats.indexing.index_failed` | DEPENDENT |
| Indexing is throttled | `opensearch.cluster.indices.stats.indexing.is_throttled` | DEPENDENT |
| Query Cache cache count | `opensearch.cluster.indices.stats.query_cache.cache_count` | DEPENDENT |
| Query Cache evictions count | `opensearch.cluster.indices.stats.query_cache.evictions` | DEPENDENT |
| Query Cache hit count | `opensearch.cluster.indices.stats.query_cache.hit_count` | DEPENDENT |
| Query Cache miss count | `opensearch.cluster.indices.stats.query_cache.miss_count` | DEPENDENT |
| Request cache count | `opensearch.cluster.indices.stats.request_cache.cache_count` | DEPENDENT |
| Request cache eviction | `opensearch.cluster.indices.stats.request_cache.evictions` | DEPENDENT |
| Request cache hits | `opensearch.cluster.indices.stats.request_cache.hits_count` | DEPENDENT |
| Request cache miss | `opensearch.cluster.indices.stats.request_cache.miss_count` | DEPENDENT |
| Opensearch get fs stats | `opensearch.cluster.nodes.fs.metric` | SCRIPT |
| Opensearch get cluster stats | `opensearch.cluster.stats` | SCRIPT |
| Opensearch Discover nodes in cluster | `opensearch.discover.nodes` | SCRIPT |
| Opensearch Discover nodes LLD in cluster | `opensearch.discover.nodes.list` | SCRIPT |
| Opensearch Discover true master in cluster | `opensearch.discover.true.master` | SCRIPT |

---

#### **Low-Level Discovery (LLD) Rules**

| Name | Key | Item Prototypes | Trigger Prototypes |
| :--- | :--- | :--- | :--- |
| Opensearch file system stats for dashboard | `opensearch.discover.fs.related` | `{#NAME} free in bytes` with key `opensearch.lld.fs.total[{#NAME}]` | None |
| Opensearch information Discovery | `opensearch.discover.status` | `Cluster: {#CLUSTERNAME} - Active primary shards`, `Cluster: {#CLUSTERNAME} - Active shards`, `Cluster: {#CLUSTERNAME} - Active shards percent`, `Cluster: {#CLUSTERNAME} - Number of delayed unassigned shards`, `Cluster: {#CLUSTERNAME} - Number of initializing shards`, `Cluster: {#CLUSTERNAME} - Number of data nodes`, `Cluster: {#CLUSTERNAME} - Number of nodes`, `Cluster: {#CLUSTERNAME} - Number of pending shards`, `Cluster: {#CLUSTERNAME} - Number of relocating shards`, `Cluster: {#CLUSTERNAME} - Health status`, `Cluster: {#CLUSTERNAME} - Number of unassigned shards` | `{#CLUSTERNAME} is in Red state` with expression `last(/Opensearch Cluster Discovery/opensearch.cluster.status[{#CLUSTERNAME}])=2`, `{#CLUSTERNAME} is in Yellow state` with expression `last(/Opensearch Cluster Discovery/opensearch.cluster.status[{#CLUSTERNAME}])=1` |
| Opensearch Discover Coordinating nodes | `opensearch.lld.coordinating` | None | None |
| Opensearch Discover Data nodes | `opensearch.lld.datanodes` | None | None |
| Opensearch Discover nodes by type in cluster | `opensearch.lld.hosts` | `Host : {#HOSTNAME}` with key `hostfound[{#HOSTNAME}]` | None |
| Opensearch Discover Ingest nodes | `opensearch.lld.ingest` | None | None |
| Opensearch Discover Master nodes | `opensearch.lld.master` | None | None |

---

#### **Triggers**

### **Opensearch Basic Node Monitoring**

* **Template Name:** Opensearch Basic Node Monitoring
* **Description:** This template is automatic added to Opensearch LLD discovered hosts. this contains systemwide specs, that is not dependend on the role.
* **Vendor:** moesgaardsdk, version 7.0-0
* **Template Group:** Opensearch

---

#### **Items**

| Name | Key | Type |
| :--- | :--- | :--- |
| Opensearch Discover basic discovery | `opensearch.discover.nodes.basic.stats` | SCRIPT |
| Opensearch tasks | `opensearch.discover.nodes.basic.tasks` | SCRIPT |
| JVM Memory pools old used in bytes | `opensearch.host..jvm.mem.pools.old.used_in_bytes` | DEPENDENT |
| JVM Memory pools survivor used in bytes | `opensearch.host..jvm.mem.pools.survivor.used_in_bytes` | DEPENDENT |
| JVM Memory pools young used in bytes | `opensearch.host..jvm.mem.pools.young.used_in_bytes` | DEPENDENT |
| JVM System Uptime | `opensearch.host..jvm.uptime_in_millis` | DEPENDENT |
| FS IO stats read operrations | `opensearch.host.fs.io_stats.total.read_operations` | DEPENDENT |
| FS IO stats read time in ms | `opensearch.host.fs.io_stats.total.read_time` | DEPENDENT |
| FS IO stats write operrations | `opensearch.host.fs.io_stats.total.write_operations` | DEPENDENT |
| FS IO stat write time in ms | `opensearch.host.fs.io_stats.total.write_time` | DEPENDENT |
| FS total free in bytes | `opensearch.host.fs.total.free_in_bytes` | DEPENDENT |
| JVM Memory Heap Max | `opensearch.host.jvm.mem.heap_max_in_bytes` | DEPENDENT |
| JVM Memory Heap Used | `opensearch.host.jvm.mem.heap_used_in_bytes` | DEPENDENT |
| OS CPU Load avg 1 min | `opensearch.host.os.cpu.load_average.1m` | DEPENDENT |
| OS CPU Load avg 5 min | `opensearch.host.os.cpu.load_average.5m` | DEPENDENT |
| OS CPU Load avg 15 min | `opensearch.host.os.cpu.load_average.15m` | DEPENDENT |
| OS CPU percent used | `opensearch.host.os.cpu.persent` | DEPENDENT |
| OS Memory Used | `opensearch.host.os.mem.used_in_bytes` | DEPENDENT |

---

#### **Low-Level Discovery (LLD) Rules**

| Name | Key | Item Prototypes | Graph Prototypes |
| :--- | :--- | :--- | :--- |
| Thread pool low level discovery | `opensearch.lld.host.thread_pool` | `Thread {#NAME} active size` with key `opensearch.host.thread_pool.active[{#NAME}]`, `Thread {#NAME} queue size` with key `opensearch.host.thread_pool.queue[{#NAME}]`, `Thread {#NAME} rejected size` with key `opensearch.host.thread_pool.rejected[{#NAME}]`, `Thread {#NAME} threads size` with key `opensearch.host.thread_pool.threads[{#NAME}]` | `{#CLUSTERNAME} : Thread {#NAME}` |
| Garbage Collector | `opensearch.lld.jvm.gc.collector` | `Garbage Collector  {#NAME}  collection count` with key `opensearch.lld.host.jvm.gc.collectors.collection_count[{#NAME}]`, `Garbage Collector  {#NAME}  collection time in milliseconds` with key `opensearch.lld.host.jvm.gc.collectors.collection_time_in_millis[{#NAME}]` | None |

---

#### **Triggers**

