<!-- .slide: data-state="section-break" id="section-break-2" data-menu-title="Ceph Mimic" data-background-image="images/ceph-mimic_full.jpg" data-background-size="cover" data-timing="10s" -->


<!-- .slide: data-state="normal" id="ceph-mimic-1" data-timing="20s" data-menu-title="RADOS" -->
## RADOS

### Central configuration via ceph-mon

### Further PG peering optimisation

### Major refactor of IO path for scale: async, event-driven

### Further BlueStore/rocksdb optimization
* RocksDB level 0 compaction
* Perhaps alternative KV stores?

### EC plugin improvements
* More efficient recovery from single OSD failures


<!-- .slide: data-state="normal" id="ceph-mimic-2" data-timing="20s" data-menu-title="QoS" -->
## Quality of service

### Continuing development:
* dmclock distributed QoS algorithm
* Minimum reservations, priority weighting

### Workloads require various policies:
* Per-IO type
* Per-pool
* Per-client

### Theory is complex, prototype is promising
### Will require some additional work to enable management


<!-- .slide: data-state="normal" id="ceph-mimic-3" data-timing="20s" data-menu-title="Tiering" -->
## Tiering

### 'redirect' primitive
* like a symlink, use as index to objects in other pools

### Deduplication
* Generalize redirects to “manifests”: map of offsets to object fragments
* Chunk object (fixed size of heuristic on file type)
* Store in content-addressable pool
  * Objects named as sha256 of content
  * Data chunks reference counted
* Still area of research


<!-- .slide: data-state="normal" id="ceph-mimic-4" data-timing="20s" data-menu-title="Ceph MGR" -->
## Ceph Manager daemon

### Infrastructure improvements:
* Integrate with central Ceph configuration store
* Handle module failures
* Enable modules to report health
* Integration with container orchestrator (rook)

### Further integration/monitoring of storage services:
* NFS ganesha, Samba, iSCSI

### Extended prometheus coverage
### Improved rebuild reporting (progress bars)
### Dashboard v2

