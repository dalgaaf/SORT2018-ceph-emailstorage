<!-- .slide: data-state="section-break" id="section-break-2" data-menu-title="Ceph Mimic" data-background-image="images/ceph-mimic_full.jpg" data-background-size="cover" data-timing="10s" -->


<!-- .slide: data-state="normal" id="ceph-mimic-1" data-timing="20s" data-menu-title="RADOS" -->
## RADOS

### Central configuration via ceph-mon <!-- .element class="fragment" data-fragment-index="1"-->

### Further PG peering optimisation <!-- .element class="fragment" data-fragment-index="2"-->

### Major refactor of IO path for scale: async, event-driven <!-- .element class="fragment" data-fragment-index="3"-->

### Further BlueStore/rocksdb optimization <!-- .element class="fragment" data-fragment-index="4"-->
* RocksDB level 0 compaction <!-- .element class="fragment" data-fragment-index="4"-->
* Perhaps alternative KV stores? <!-- .element class="fragment" data-fragment-index="4"-->

### EC plugin improvements <!-- .element class="fragment" data-fragment-index="5"-->
* More efficient recovery from single OSD failures <!-- .element class="fragment" data-fragment-index="5"-->


<!-- .slide: data-state="normal" id="ceph-mimic-2" data-timing="20s" data-menu-title="QoS" -->
## Quality of service

### Continuing development: <!-- .element class="fragment" data-fragment-index="1"-->
* dmclock distributed QoS algorithm <!-- .element class="fragment" data-fragment-index="1"-->
* Minimum reservations, priority weighting <!-- .element class="fragment" data-fragment-index="1"-->

### Workloads require various policies: <!-- .element class="fragment" data-fragment-index="2"-->
* Per-IO type <!-- .element class="fragment" data-fragment-index="2"-->
* Per-pool <!-- .element class="fragment" data-fragment-index="2"-->
* Per-client <!-- .element class="fragment" data-fragment-index="2"-->

### Theory is complex, prototype is promising <!-- .element class="fragment" data-fragment-index="3"-->
### Will require some additional work to enable management <!-- .element class="fragment" data-fragment-index="3"-->


<!-- .slide: data-state="normal" id="ceph-mimic-3" data-timing="20s" data-menu-title="Tiering" -->
## Tiering

### 'redirect' primitive <!-- .element class="fragment" data-fragment-index="1"-->
* like a symlink, use as index to objects in other pools <!-- .element class="fragment" data-fragment-index="1"-->

### Deduplication <!-- .element class="fragment" data-fragment-index="2"-->
* Generalize redirects to “manifests”: map of offsets to object fragments <!-- .element class="fragment" data-fragment-index="2"-->
* Chunk object (fixed size of heuristic on file type) <!-- .element class="fragment" data-fragment-index="2"-->
* Store in content-addressable pool <!-- .element class="fragment" data-fragment-index="2"-->
  * Objects named as sha256 of content <!-- .element class="fragment" data-fragment-index="2"-->
  * Data chunks reference counted <!-- .element class="fragment" data-fragment-index="2"-->
* Still area of research <!-- .element class="fragment" data-fragment-index="2"-->


<!-- .slide: data-state="normal" id="ceph-mimic-4" data-timing="20s" data-menu-title="Ceph MGR" -->
## Ceph Manager daemon

### Infrastructure improvements: <!-- .element class="fragment" data-fragment-index="1"-->
* Integrate with central Ceph configuration store <!-- .element class="fragment" data-fragment-index="1"-->
* Handle module failures <!-- .element class="fragment" data-fragment-index="1"-->
* Enable modules to report health <!-- .element class="fragment" data-fragment-index="1"-->
* Integration with container orchestrator (rook) <!-- .element class="fragment" data-fragment-index="1"-->

### Further integration/monitoring of storage services: <!-- .element class="fragment" data-fragment-index="2"-->
* NFS ganesha, Samba, iSCSI <!-- .element class="fragment" data-fragment-index="2"-->

### Extended prometheus coverage <!-- .element class="fragment" data-fragment-index="3"-->
### Improved rebuild reporting (progress bars) <!-- .element class="fragment" data-fragment-index="4"-->
### Dashboard v2 <!-- .element class="fragment" data-fragment-index="5"-->

