<!-- .slide: data-state="section-break" id="section-break-1" data-menu-title="Ceph Luminous" data-background-image="images/ceph-luminous_full.jpg" data-background-size="cover" data-timing="10s" -->


<!-- .slide: data-state="normal" id="ceph-luminous-1" data-timing="20s" data-menu-title="BlueStore" -->
## BlueStore: default

### New OSD backend <!-- .element class="fragment" data-fragment-index="1"-->
* Consumes raw block device instead of FS layer <!-- .element class="fragment" data-fragment-index="1"-->
* Embedded k-v-store (rocksdb) for metadata <!-- .element class="fragment" data-fragment-index="1"-->

### Performance improvements <!-- .element class="fragment" data-fragment-index="2"-->
* HDD: ~2x, SSD: ~1.5x <!-- .element class="fragment" data-fragment-index="2"-->
* NVMe: less, device is not the bottleneck <!-- .element class="fragment" data-fragment-index="2"-->

### Smaller journals <!-- .element class="fragment" data-fragment-index="3"-->
### Data checksums (crc32c, xxhash, ...) <!-- .element class="fragment" data-fragment-index="4"-->
### Inline compression (zlib, snappy, ...) <!-- .element class="fragment" data-fragment-index="5"-->

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


<!-- .slide: data-state="normal" id="ceph-luminous-4.0" data-timing="20s" data-menu-title="Erasure code" -->
## Replication vs. Erasure Coding
<center><img src="images/erasurecoding.svg" style="width:100%"></center>

Note: 3xRepl - 200% overhead, quick recovery / EC - cost-efficiant, 50% overhead, expensive recovery, solves 2FC problems


<!-- .slide: data-state="normal" id="ceph-luminous-4.1" data-timing="20s" data-menu-title="Erasure code" -->
## RBD/CephFS on erasure coded pools

### requires BlueStore <!-- .element class="fragment" data-fragment-index="1"-->
* EC overwrites <!-- .element class="fragment" data-fragment-index="1"-->
* Implementation: every update rewrites a full stripe <!-- .element class="fragment" data-fragment-index="1"-->

### Efficiency, Performance <!-- .element class="fragment" data-fragment-index="2"-->
* Significant better efficiency than 3x replica <!-- .element class="fragment" data-fragment-index="2"-->
  * 2+2 EC -> 2x , 4+2 EC -> 1.5x <!-- .element class="fragment" data-fragment-index="2"-->
* Small writes significant slower than 3x replica <!-- .element class="fragment" data-fragment-index="3"-->
  * 4+2 EC -> 0.5x <!-- .element class="fragment" data-fragment-index="3"-->
* Large writes faster than replication <!-- .element class="fragment" data-fragment-index="4"-->
  * less total data to be written on media <!-- .element class="fragment" data-fragment-index="4"-->


<!-- .slide: data-state="normal" id="ceph-luminous-5" data-timing="20s" data-menu-title="Ceph Manager (ceph-mgr)" -->
## Ceph Manager daemon (ceph-mgr)

### Supplement to ceph-mon <!-- .element class="fragment" data-fragment-index="1"-->
* Management and monitoring features <!-- .element class="fragment" data-fragment-index="1"-->
* Extensible with Python <!-- .element class="fragment" data-fragment-index="1"-->
* Integrated metrics gathering from Ceph daemons <!-- .element class="fragment" data-fragment-index="1"-->

### Improved ceph-mon performance <!-- .element class="fragment" data-fragment-index="2"-->
* Offload pg statistics gathering from mon <!-- .element class="fragment" data-fragment-index="2"-->
* Tested up to 10k OSDs @ CERN “Big Bang 3” <!-- .element class="fragment" data-fragment-index="2"-->

### Built-in web dashboard <!-- .element class="fragment" data-fragment-index="3"-->
### Other modules: zabbix, influxdb, prometheus, restful <!-- .element class="fragment" data-fragment-index="4"-->


<!-- .slide: data-state="normal" id="ceph-luminous-6" data-timing="20s" data-menu-title="AsyncMessenger" -->
## AsyncMessenger

### All Ceph services use “Messenger” classes for communications <!-- .element class="fragment" data-fragment-index="1"-->
* Old “SimpleMessenger” used one thread/connection <!-- .element class="fragment" data-fragment-index="1"-->
* New AsyncMessenger is event driven, fixed size thread pool <!-- .element class="fragment" data-fragment-index="1"-->

### RDMA backend (ibverbs) <!-- .element class="fragment" data-fragment-index="2"-->
* Built by default <!-- .element class="fragment" data-fragment-index="2"-->
* Not heavily tested, but appears to work <!-- .element class="fragment" data-fragment-index="2"-->

### DPDK (userspace packet processing) backend <!-- .element class="fragment" data-fragment-index="3"-->
* Prototype stage <!-- .element class="fragment" data-fragment-index="4"-->


<!-- .slide: data-state="normal" id="ceph-luminous-7" data-timing="20s" data-menu-title="OSD Balance" -->
## Improved OSD balance

### CRUSH choose_args <!-- .element class="fragment" data-fragment-index="1"-->
* Alternate weight sets per-rule <!-- .element class="fragment" data-fragment-index="1"-->
* Flexibility to optimize weights <!-- .element class="fragment" data-fragment-index="1"-->
* Fix imbalances: run numeric optimization to tweak placement <!-- .element class="fragment" data-fragment-index="1"-->
* Fix multipick anomaly: correct for low-weighted branches like empty racks <!-- .element class="fragment" data-fragment-index="1"-->

### Placement group “upmap” <!-- .element class="fragment" data-fragment-index="2"-->
* Explicitly map PG to OSDs <!-- .element class="fragment" data-fragment-index="2"-->
* Configured by included balancer modulem <!-- .element class="fragment" data-fragment-index="2"-->
* Requires >= luminous clients <!-- .element class="fragment" data-fragment-index="2"-->


<!-- .slide: data-state="normal" id="ceph-luminous-8" data-timing="20s" data-menu-title="RADOS improvements" -->
## Other RADOS improvements

* CRUSH device classes: easily map pools to SSDs, HDDs
* Simplified disk replacement procedure
* require_min_compat_client for safer configuration
* Built-in configuration option metadata (docstrings etc)
* Client backoff on stuck PGs/objects
* Improved EIO handling on OSDs
* Faster placement group peering
* Faster OSD failure detection


<!-- .slide: data-state="normal" id="ceph-luminous-9" data-timing="20s" data-menu-title="CephFS" -->
## CephFS

### Multiple active MDS daemons <!-- .element class="fragment" data-fragment-index="1"-->
* scale out metadata performance <!-- .element class="fragment" data-fragment-index="1"-->

### Subtree pinning <!-- .element class="fragment" data-fragment-index="2"-->
* Isolate certain workloads <!-- .element class="fragment" data-fragment-index="2"-->
* Pre-define work distribution if known in advance <!-- .element class="fragment" data-fragment-index="2"-->

### Large directory support <!-- .element class="fragment" data-fragment-index="3"-->
* directory fragmentation now enabled by default <!-- .element class="fragment" data-fragment-index="3"-->

### Many bugs fixed, tests added <!-- .element class="fragment" data-fragment-index="4"-->


<!-- .slide: data-state="normal" id="ceph-luminous-10" data-timing="20s" data-menu-title="RGW" -->
## RGW

* NFS gateway: NFSv4 and v3 <!-- .element class="fragment" -->
* Dynamic bucket index sharding (automatic) <!-- .element class="fragment" -->
* Inline compression <!-- .element class="fragment" -->
* Encryption (S3 encryption API) <!-- .element class="fragment" -->
* Improved S3/Swift API support (odds and ends) <!-- .element class="fragment" -->
* Metadata search <!-- .element class="fragment" -->


<!-- .slide: data-state="normal" id="ceph-luminous-11" data-timing="20s" data-menu-title="RBD" -->
## RBD

### Support for erasure coded pools <!-- .element class="fragment" data-fragment-index="1"-->

### Mirroring improvements <!-- .element class="fragment" data-fragment-index="2"-->
* Cooperative HA daemons <!-- .element class="fragment" data-fragment-index="2"-->
* Improved integration with OpenStack Cinder <!-- .element class="fragment" data-fragment-index="2"-->

### iSCSI <!-- .element class="fragment" data-fragment-index="3"-->
* LIO + tcmu-runner using librbd <!-- .element class="fragment" data-fragment-index="3"-->

### Better Kernel RBD feature coverage <!-- .element class="fragment" data-fragment-index="4"-->
* Exclusive locking <!-- .element class="fragment" data-fragment-index="4"-->
* Object maps <!-- .element class="fragment" data-fragment-index="4"-->
