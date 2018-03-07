<!-- .slide: data-state="section-break" id="section-break-1" data-menu-title="Ceph Luminous" data-background-image="images/ceph-luminous_full.jpg" data-background-size="cover" data-timing="10s" -->


<!-- .slide: data-state="normal" id="ceph-luminous-1" data-timing="20s" data-menu-title="BlueStore" -->
## BlueStore: default

### New OSD backend
* Consumes raw block device instead of FS layer
* Embedded k-v-store (rocksdb) for metadata

### Performance improvements
* HDD: ~2x, SSD: ~1.5x
* NVMe: less, device is not the bottleneck

### Smaller journals
### Data checksums (crc32c, xxhash, ...)
### Inline compression (zlib, snappy, ...)

Note: May still use SSD or NVMe for journals


<!-- .slide: data-state="normal" id="ceph-luminous-3.1" data-timing="20s" data-menu-title="BlueStore Performance HDD RW" -->
<center><img src="images/bluestore_hdd_rw.svg" style="width:90%"></center>


<!-- .slide: data-state="normal" id="ceph-luminous-3.3" data-timing="20s" data-menu-title="BlueStore Performance HDD RRW" -->
<center><img src="images/bluestore_hdd_rrw.svg" style="width:90%"></center>


<!-- .slide: data-state="normal" id="ceph-luminous-3.2" data-timing="20s" data-menu-title="BlueStore Performance HDD/NVMe RRW" -->
<center><img src="images/bluestore_hdd-nvme_rrw.svg" style="width:90%"></center>


<!-- .slide: data-state="normal" id="ceph-luminous-3.4" data-timing="20s" data-menu-title="BlueStore Performance HDD SW" -->
<center><img src="images/bluestore_hdd_sw.svg" style="width:90%"></center>


<!-- .slide: data-state="normal" id="ceph-luminous-3.5" data-timing="20s" data-menu-title="BlueStore Performance HDD RBD RW" -->
<center><img src="images/bluestore_hdd_rw_rbd.svg" style="width:100%"></center>


<!-- .slide: data-state="normal" id="ceph-luminous-3.6" data-timing="20s" data-menu-title="BlueStore Performance HDD RGW W Repl" -->
<center><img src="images/bluestore_hdd_rgw_w.svg" style="width:95%"></center>


<!-- .slide: data-state="normal" id="ceph-luminous-3.7" data-timing="20s" data-menu-title="BlueStore Performance HDD RGW W EC" -->
<center><img src="images/bluestore_hdd_rgw_wEC.svg" style="width:100%"></center>


<!-- .slide: data-state="normal" id="ceph-luminous-4" data-timing="20s" data-menu-title="Erasure code" -->
## RBD/CephFS on erasure coded pools

### requires BlueStore
* EC overwrites
* Implementation: every update rewrites a full stripe

### Efficiency, Performance
* Significant better efficiency than 3x replica
  * 2+2 EC -> 2x , 4+2 EC -> 1.5x
* Small writes significant slower than 3x replica
  * 4-2 EC -> 0.5x
* Large writes faster than replication
  * less total data to be written on media


<!-- .slide: data-state="normal" id="ceph-luminous-5" data-timing="20s" data-menu-title="Ceph Manager (ceph-mgr)" -->
## Ceph Manager daemon (ceph-mgr)

### Supplement to ceph-mon
* Management and monitoring features
* Extensible with Python
* Integrated metrics gathering from Ceph daemons

### Improved ceph-mon performance
* Offload pg statistics gathering from mon
* Tested up to 10k OSDs @ CERN “Big Bang 3”

### Built-in web dashboard
### Other modules: zabbix, influxdb, prometheus, restful


<!-- .slide: data-state="normal" id="ceph-luminous-6" data-timing="20s" data-menu-title="AsyncMessenger" -->
## AsyncMessenger

### All Ceph services use “Messenger” classes for communications
* Old “SimpleMessenger” used one thread/connection
* New AsyncMessenger is event driven, fixed size thread pool

### RDMA backend (ibverbs)
* Built by default
* Not heavily tested, but appears to work

### DPDK (userspace packet processing) backend
* Prototype stage


<!-- .slide: data-state="normal" id="ceph-luminous-7" data-timing="20s" data-menu-title="OSD Balance" -->
## Improved OSD balance

### CRUSH choose_args
* Alternate weight sets per-rule
* Flexibility to optimize weights
* Fix imbalances: run numeric optimization to tweak placement
* Fix multipick anomaly: correct for low-weighted branches like empty racks

### Placement group “upmap”
* Explicitly map PG to OSDs
* Configured by included balancer module
* Requires >= luminous clients


<!-- .slide: data-state="normal" id="ceph-luminous-8" data-timing="20s" data-menu-title="RADOS improvements" -->
## Other RADOS improvements

* CRUSH device classes: easily map pools to SSDs, HDDs
* Simplified disk replacement procedure
* require_min_compat_client for safer configuration
* Built-in configuration option metadata (docstrings etc)
* Client backoff on stuck Pgs/objects
* Improved EIO handling on OSDs
* Faster placement group peering
* Faster OSD failure detection


<!-- .slide: data-state="normal" id="ceph-luminous-9" data-timing="20s" data-menu-title="CephFS" -->
## CephFS

### Multiple active MDS daemons
* scale out metadata performance

### Subtree pinning
* Isolate certain workloads
* Pre-define work distribution if known in advance

### Large directory support
* directory fragmentation now enabled by default

### Many bugs fixed, tests added


<!-- .slide: data-state="normal" id="ceph-luminous-10" data-timing="20s" data-menu-title="RGW" -->
## RGW

* NFS gateway: NFSv4 and v3
* Dynamic bucket index sharding (automatic)
* Inline compression
* Encryption (S3 encryption API)
* Improved S3/Swift API support (odds and ends)
* Metadata search


<!-- .slide: data-state="normal" id="ceph-luminous-11" data-timing="20s" data-menu-title="RBD" -->
## RBD

### Support for erasure coded pools

### Mirroring improvements
* Cooperative HA daemons
* Improved integration with OpenStack Cinder

### ISCSI
* LIO + tcmu-runner using librbd

### Better Kernel RBD feature coverage
* Exclusive locking
* Object maps
