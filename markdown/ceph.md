<!-- .slide: data-state="section-break" id="section-break-3" data-timing="10s" -->
# Ceph


<!-- .slide: data-state="normal" id="ceph-0" data-timing="20s" data-menu-title="Ceph: What" -->
## What is Ceph?

* Unified distributed storage system for
  * file
  * block
  * object
* Storage platform
* Software defined storage (SDS)
* The future of storage
* The Linux of storage

Note:
- Slides inspired by Sage's keynote at Cephalocon


<!-- .slide: data-state="normal" id="ceph-1" data-timing="20s" data-menu-title="Ceph: Overview" -->
<div>
	<center><img src="images/ceph-stack.svg" style="width:90%"></center>
</div>


<!-- .slide: data-state="normal" id="ceph-2" data-timing="20s" data-menu-title="Ceph: Why" -->
## Why is Ceph?

### Free and Open Source software
* Freedom to use
* Freedom from vendor lock-in
* Freedom to change and innovate
* Freedom to share


<!-- .slide: data-state="normal" id="ceph-3" data-timing="20s" data-menu-title="Ceph: Reliability" -->
## Why is Ceph?

### Reliable and durable storage 
* build out of unreliable components
* No single point of failure
* Replication and erasure coding
* self-monitoring and self-managed
* automated re-balance, recovery, and backfill

### Consitency and correctness over performance


<!-- .slide: data-state="normal" id="ceph-4" data-timing="20s" data-menu-title="Ceph: Scalability" -->
## Why is Ceph?

### Scalability
* Elastic infrastructure
  * from 10s to 10.000s of nodes
  * grow and shrink
  * add and remove hardware
  * rolling update/upgrade
  * all while cluster is online and in use
* Scale-up
* Scale-out
* Multi-cluster federation across sites

Note:
- scale-up: bigger/faster HW
- scale-out: within a single cluster or site
- Failure is not the exception, but the norm


<!-- .slide: data-state="normal" id="ceph-5" data-timing="20s" data-menu-title="Ceph: Components" -->
## Components

### MON
* lightweight daemon
* paxos protocol, odd number
* maintains maps of the cluster state
* authentication (CephX)

### OSD
* smart storage daemon, coordinates with peers
* handles data replication, recovery, backfilling, and rebalancing
* BlueStore
  * utilize the raw storage device
  * Object data, RocksDB (kv-store), Write-ahead log of RocksDB

Note:
- MON: cluster membership, mon-map, osd-map, PG-map, CRUSH-map
- OSD: usually one OSD per physical storage device (sometimes e.g. 2 OSDs per NVMe)


<!-- .slide: data-state="normal" id="ceph-6" data-timing="20s" data-menu-title="Ceph: Components" -->
## Components

### MDS
* metadata for posix-compliant shared filesystem (CephFS)
  * directory hierachy
  * file metadata
* multi-MDS support
* multi-active, standby, standby-replay, hot-standby
* coordinate access

### Clients
* authenticate with MONs
* talk directly to OSDs

Note:


<!-- .slide: data-state="normal" id="ceph-7" data-timing="20s" data-menu-title="Ceph: CRUSH" -->
## CRUSH ???
<div>
	<center><img src="images/crush.svg" style="width:35%"></center>
</div>

Note:
- Controlled Replication Under Scalable Hashing
- uniform, weighted distribution
- fast O(log n) calculation, no lists or tables, no lookups
- stable, predictable, bounded migration on changes


<!-- .slide: data-state="normal" id="ceph-8" data-timing="20s" data-menu-title="Ceph: Pools, PGs" -->
## What else?

* Pools
  * independent cluster namespaces
  * subset of the cluster
  * resilence configured on pool level
  * CRUSH ruleset
  * access control

* PGs
  * namespaces or object collections
  * handle data placement based on PGs instead of each object
  * base for CRUSH calculations
  * base for handling recovery

