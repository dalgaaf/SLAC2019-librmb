<!-- .slide: data-state="section-break" id="section-break-6" data-timing="10s" -->
# Placement


<!-- .slide: data-state="normal" id="placement-1" data-timing="20s" data-menu-title="Placement issues" -->
## Issues

### Datacenter <!-- .element: class="fragment" data-fragment-index="0" -->
* <!-- .element: class="fragment" data-fragment-index="1" --> Usually two independent fire compartments (FCs)
* <!-- .element: class="fragment" data-fragment-index="2" --> May additional virtual FCs
* <!-- .element: class="fragment" data-fragment-index="3" --> How to place 3 copies?

### Requirements <!-- .element: class="fragment" data-fragment-index="4" -->
* <!-- .element: class="fragment" data-fragment-index="5" --> Lost of customer data MUST be prevented
* <!-- .element: class="fragment" data-fragment-index="5" --> Data replication at least 3 times (or equivalent)
* <!-- .element: class="fragment" data-fragment-index="5" --> Any server, switch or rack can fail
* <!-- .element: class="fragment" data-fragment-index="5" --> One FC can fail


<!-- .slide: data-state="normal" id="placement-3" data-timing="20s" data-menu-title="3FCs" -->
<div>
  <center><img data-src="images/fc-ceph-EC+3xReplication-color.svg" style="width:85%"></center>
</div>


<!-- .slide: data-state="normal" id="placement-net-2" data-timing="20s" data-menu-title="Network Overview" -->
<div>
  <center><img data-src="images/network-infra-mailplatform.svg" style="width:85%"></center>
</div>

Note: 1G OAM, 4x10G ports per node, SFP+ DAC, MC-LAG/M-LAG for aggregation and failoverm 
      interconnect must not reflect theoretical rack/FC bandwidth, L2 terminated in rack, L3 for rest
