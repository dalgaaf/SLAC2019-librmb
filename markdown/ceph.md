<!-- .slide: data-state="section-break" id="section-break-3" data-timing="10s" -->
# Ceph


<!-- .slide: data-state="normal" id="ceph-0" data-timing="20s" data-menu-title="Ceph: What" -->
## What is Ceph?

* Unified distributed storage system for <!-- .element: class="fragment" data-fragment-index="0" -->
  * file <!-- .element: class="fragment" data-fragment-index="0" -->
  * block <!-- .element: class="fragment" data-fragment-index="0" -->
  * object <!-- .element: class="fragment" data-fragment-index="0" -->
* Storage platform <!-- .element: class="fragment" data-fragment-index="1" -->
* Software defined storage (SDS) <!-- .element: class="fragment" data-fragment-index="2" -->
* The future of storage <!-- .element: class="fragment" data-fragment-index="3" -->
* The Linux of storage <!-- .element: class="fragment" data-fragment-index="4" -->

Note:
- Slides inspired by Sage's keynote at Cephalocon


<!-- .slide: data-state="normal" id="ceph-1" data-timing="20s" data-menu-title="Ceph: Overview" -->
<div>
	<center><img src="images/ceph-stack.svg" style="width:90%"></center>
</div>


<!-- .slide: data-state="normal" id="ceph-2" data-timing="20s" data-menu-title="Ceph: Why" -->
## Why is Ceph?

### Free and Open Source software <!-- .element class="fragment" -->
* Freedom to use <!-- .element class="fragment" -->
* Freedom from vendor lock-in <!-- .element class="fragment" -->
* Freedom to change and innovate <!-- .element class="fragment" -->
* Freedom to share <!-- .element class="fragment" -->


<!-- .slide: data-state="normal" id="ceph-3" data-timing="20s" data-menu-title="Ceph: Reliability" -->
## Why is Ceph?

### Reliable and durable storage <!-- .element class="fragment" -->
* build out of unreliable components <!-- .element class="fragment" -->
* No single point of failure <!-- .element class="fragment" -->
* Replication and erasure coding <!-- .element class="fragment" -->
* self-monitoring and self-managed <!-- .element class="fragment" -->
* automated re-balance, recovery, and backfill <!-- .element class="fragment" -->

### Consitency and correctness over performance <!-- .element class="fragment" -->


<!-- .slide: data-state="normal" id="ceph-4" data-timing="20s" data-menu-title="Ceph: Scalability" -->
## Why is Ceph?

### Scalability <!-- .element class="fragment" -->
* Elastic infrastructure <!-- .element class="fragment" -->
  * from 10s to 10.000s of nodes <!-- .element class="fragment" -->
  * grow and shrink <!-- .element class="fragment" -->
  * add and remove hardware <!-- .element class="fragment" -->
  * rolling update/upgrade <!-- .element class="fragment" -->
  * all while cluster is online and in use <!-- .element class="fragment" -->
* Scale-up <!-- .element class="fragment" -->
* Scale-out <!-- .element class="fragment" -->
* Multi-cluster federation across sites <!-- .element class="fragment" -->

Note:
- scale-up: bigger/faster HW
- scale-out: within a single cluster or site
- Failure is not the exception, but the norm


<!-- .slide: data-state="normal" id="ceph-5" data-timing="20s" data-menu-title="Ceph: Components" -->
## Components

### MON <!-- .element class="fragment" -->
* lightweight daemon <!-- .element class="fragment" -->
* paxos protocol, odd number <!-- .element class="fragment" -->
* maintains maps of the cluster state <!-- .element class="fragment" -->
* authentication (CephX) <!-- .element class="fragment" -->

### OSD <!-- .element class="fragment" -->
* smart storage daemon, coordinates with peers <!-- .element class="fragment" -->
* handles data replication, recovery, backfilling, and rebalancing <!-- .element class="fragment" -->
* BlueStore <!-- .element class="fragment" -->
  * utilize the raw storage device <!-- .element class="fragment" -->
  * Object data, RocksDB (kv-store), Write-ahead log of RocksDB <!-- .element class="fragment" -->

Note:
- MON: cluster membership, mon-map, osd-map, PG-map, CRUSH-map
- OSD: usually one OSD per physical storage device (sometimes e.g. 2 OSDs per NVMe)


<!-- .slide: data-state="normal" id="ceph-6" data-timing="20s" data-menu-title="Ceph: Components" -->
## Components

### MDS <!-- .element class="fragment" -->
* metadata for posix-compliant shared filesystem (CephFS) <!-- .element class="fragment" -->
  * directory hierachy <!-- .element class="fragment" -->
  * file metadata <!-- .element class="fragment" -->
* multi-MDS support <!-- .element class="fragment" -->
* multi-active, standby, standby-replay, hot-standby <!-- .element class="fragment" -->
* coordinate access <!-- .element class="fragment" -->

### Clients <!-- .element class="fragment" -->
* authenticate with MONs <!-- .element class="fragment" -->
* talk directly to OSDs <!-- .element class="fragment" -->

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

* Pools <!-- .element class="fragment" -->
  * independent cluster namespaces <!-- .element class="fragment" -->
  * subset of the cluster <!-- .element class="fragment" -->
  * resilence configured on pool level <!-- .element class="fragment" -->
  * CRUSH ruleset <!-- .element class="fragment" -->
  * access control <!-- .element class="fragment" -->

* PGs <!-- .element class="fragment" -->
  * namespaces or object collections <!-- .element class="fragment" -->
  * handle data placement based on PGs instead of each object <!-- .element class="fragment" -->
  * base for CRUSH calculations <!-- .element class="fragment" -->
  * base for handling recovery <!-- .element class="fragment" -->

