<!-- .slide: data-state="section-break" id="section-break-6" data-timing="10s" -->
# Placement


<!-- .slide: data-state="normal" id="placement-0" data-timing="20s" data-menu-title="Data Center" -->
## Data Center 

### Former assumption <!-- .element: class="fragment" data-fragment-index="0" -->
* Two independent fire compartments (FCs) <!-- .element: class="fragment" data-fragment-index="0" -->
* May additional virtual FCs <!-- .element: class="fragment" data-fragment-index="0" -->

### Updated <!-- .element: class="fragment" data-fragment-index="1" -->
* Production will be placed in a new DC <!-- .element: class="fragment" data-fragment-index="1" -->
* \>3 independent fire compartments <!-- .element: class="fragment" data-fragment-index="1" -->
* Network will fit bandwidth requirements <!-- .element: class="fragment" data-fragment-index="1" -->

Note: 
- requirements adapted since the last presentation


<!-- .slide: data-state="normal" id="placement-3" data-timing="20s" data-menu-title="3FCs" -->
### Current setup
<div>
  <center><img data-src="images/fc-ceph-EC+3xReplication-color.svg" style="width:75%"></center>
</div>

Note: current intermediate state


<!-- .slide: data-state="normal" id="placement-3" data-timing="20s" data-menu-title="3FCs" -->
### PoC Setup
<div>
  <center><img data-src="images/fc-ceph-EC-color_white_v2.svg" style="width:75%"></center>
</div>

Note:
- cluster gets extended 18 HDD nodes on 3 FCs
- for better distribution, especially for EC


<!-- .slide: data-state="normal" id="placement-net-2" data-timing="20s" data-menu-title="Network Overview" -->
<div>
  <center><img data-src="images/network-infra-mailplatform_v1.svg" style="width:85%"></center>
</div>

Note: 
- 1G OAM
- 4x10G ports per node, SFP+ DAC
- MC-LAG/M-LAG for aggregation and failover
- 40 or 80G interconnect between FCs and to spine
- interconnect must not reflect theoretical rack/FC bandwidth
- L2 terminated in rack, L3 for rest


<!-- .slide: data-state="normal" id="placement-1" data-timing="20s" data-menu-title="Data safety" -->
## Requirements for Production

* <!-- .element: class="fragment" data-fragment-index="0" --> Lost of customer data __MUST__ be prevented at any cost 
* At least replica 3 or comparable <!-- .element: class="fragment" data-fragment-index="1" -->

* <!-- .element: class="fragment" data-fragment-index="2" --> Failure scenarios to be covered: 
  * <!-- .element: class="fragment" data-fragment-index="3" --> 1 of 3 fire compartments (FCs)
  * <!-- .element: class="fragment" data-fragment-index="3" --> 1 FC + 1 Server (or HDD/SSD)
  * <!-- .element: class="fragment" data-fragment-index="3" --> 1 FC + 1 Server + 1 HDD/SSD 

* <!-- .element: class="fragment" data-fragment-index="4" --> Cluster __MUST__ be fully operational (R/W) in any scenario 
* <!-- .element: class="fragment" data-fragment-index="5" --> Additonal failure __MUST__ not cause data loss
* Applies to CephFS and Rados part <!-- .element: class="fragment" data-fragment-index="6" -->

Note: 
- additional error sets cluster in hold, no writes to the cluster any more, cause stop of mail system.
- max. failure scenario would be 4 independet errors before cluster stops to be responsive, even then no data loss.
