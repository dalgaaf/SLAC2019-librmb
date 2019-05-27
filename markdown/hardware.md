<!-- .slide: data-state="section-break" id="section-break-5" data-timing="10s" -->
# Hardware


<!-- .slide: data-state="normal" id="hardware-1" data-timing="20s" data-menu-title="Hardware Server specs" -->
## Commodity x86_64 server
<div>
     <img style="position: absolute; width: 35%; left: 60%; " alt="librmb architecture overview"
          data-src="images/HPE-DL380Gen9.jpg" />
</div>

* <!-- .element: class="fragment" data-fragment-index="1" --> HPE ProLiant DL380 Gen9/10
* <!-- .element: class="fragment" data-fragment-index="1" --> 2x Dual-port 10G, SSD for boot, HBA only

### CephFS Nodes (MDS, OSDs) <!-- .element: class="fragment" data-fragment-index="2" -->
* <!-- .element: class="fragment" data-fragment-index="2" --> <b>CPU:</b> 2x E5-2643v4 @ 3.4 GHz, 6 Cores, turbo 3.7GHz
* <!-- .element: class="fragment" data-fragment-index="2" --> <b>RAM:</b> 256 GByte, DDR4, ECC
* <!-- .element: class="fragment" data-fragment-index="2" --> <b>OSDs:</b> 8x 1.6 TB SSD, 3 DWPD, SAS, RR/RW 125k/92k iops

### Rados Nodes (OSDs) <!-- .element: class="fragment" data-fragment-index="3" -->
* <!-- .element: class="fragment" data-fragment-index="3" --> <b>CPU:</b> 2x E5-2640v4 @ 2.4 GHz, 10 Cores, turbo 3.4GHz
* <!-- .element: class="fragment" data-fragment-index="3" --> <b>RAM:</b> 128 GByte, DDR4, ECC
* <!-- .element: class="fragment" data-fragment-index="3" --> <b>SSD:</b> 2x 400 GByte, 3 DWPD, SAS, RR/RW 108k/49k iops (for BlueStore database)
* <!-- .element: class="fragment" data-fragment-index="3" --> <b>HDD:</b> 10x 4 TByte, 7.2K, 128 MB cache, SAS


<!-- .slide: data-state="normal" id="hardware-3" data-timing="20s" data-menu-title="Hardware specs" -->
## Why this specific HW?

### Community min. recommendations? <!-- .element: class="fragment" data-fragment-index="0" -->
* <!-- .element: class="fragment" data-fragment-index="0" --> OSD: 1x 64-bit AMD-64, 1GB RAM/1TB of storage, 2x 1GBit NICs
* <!-- .element: class="fragment" data-fragment-index="0" --> MDS: 1x 64-bit AMD-64 quad-core, 1 GB RAM minimum per MDS, 2x 1GBit NICs

<br>
### NUMA, high clocked CPUs and large RAM overkill? <!-- .element: class="fragment" data-fragment-index="1" -->
* <!-- .element: class="fragment" data-fragment-index="2" --> It's PoC hardware! Better save than sorry!
* <!-- .element: class="fragment" data-fragment-index="3" --> Vendor did not offer single CPU nodes for number of drives
* <!-- .element: class="fragment" data-fragment-index="4" --> MDS performance is mostly CPU clock bound and partly single threaded
  * <!-- .element: class="fragment" data-fragment-index="4" --> High clocked CPUs for fast single thread performance
* <!-- .element: class="fragment" data-fragment-index="5" --> Large RAM: better caching!

