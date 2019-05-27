<!-- .slide: data-state="section-break" id="section-break-6.1" data-timing="10s" -->
# Data Distribution


<!-- .slide: data-state="normal" id="EC-0" data-timing="20s" data-menu-title="Replication vs EC" -->
## Options

* Replication <!-- .element: class="fragment" data-fragment-index="0" -->
  * copy each object n-times <!-- .element: class="fragment" data-fragment-index="0" -->
  * at least 200% overhead (3x) <!-- .element: class="fragment" data-fragment-index="0" -->
  * fast read <!-- .element: class="fragment" data-fragment-index="0" -->
  * quicker recovery <!-- .element: class="fragment" data-fragment-index="0" -->

* Erasure Coding (EC) <!-- .element: class="fragment" data-fragment-index="1" -->
  * one copy plus parity <!-- .element: class="fragment" data-fragment-index="1" -->
  * space effective <!-- .element: class="fragment" data-fragment-index="1" -->
  * performance impact on small objects <!-- .element: class="fragment" data-fragment-index="1" -->
  * expensive recovery <!-- .element: class="fragment" data-fragment-index="1" -->

Note: 
- read on replication faster due to fact that k objects need to read (latency, CPU)


<!-- .slide: data-state="normal" id="EC-0.1" data-timing="20s" data-menu-title="Replication Diagram" -->
### Replication
<div>
  <center><img data-src="images/replica_explained.svg" style="width:30%"></center>
</div>

Note:


<!-- .slide: data-state="normal" id="EC-0.2" data-timing="20s" data-menu-title="Erasure Coding Diagram" -->
### Erasure Coding
<div>
  <center><img data-src="images/ec_explained_extra.svg" style="width:65%"></center>
</div>

Note:
- Object is split into *k* chunks
- Additonal *m* coding chunks will be created (encoded)
- chunks/shards will be distributed as defined in crush and erasure code profile


<!-- .slide: data-state="normal" id="EC-1" data-timing="20s" data-menu-title="Jerasure Options" -->
## Jerasure

``k = {data chunks}``
* number of chunks the object is cut into

``m = {coding chunks}``
* number of failure domains that can be down

``crush-failure-domain={bucket-type}``
* usually host

``crush-device-class={hdd|ssd}``


<!-- .slide: data-state="normal" id="EC-2" data-timing="20s" data-menu-title="Erasure Coding Crush options" -->
## EC - Crush

``min_size``
* should be >= ``k``

``max_size``
* k + m

``step choose indep 0 type {rack|room|...}``

``step chooseleaf indep {N} type {host}``

Note:
- chooseleaf: N == number of hosts to be picked in e.g. a FC


<!-- .slide: data-state="normal" id="EC-3" data-timing="20s" data-menu-title="Cover" -->
## To Cover

### 3 (+1) failures

### 2 and 3 FC

### Available hardware

### comparable performance and behaviour 
  * Test and PoC
  * PoC and Production

### Even distribution of chunks/copies over FCs

Note:
- 3+1 because next error must not cause data loss
- Test is 2/3 FCs (Rados 6/6 server; CephFS 3/3/3)
- PoC+Production is 3/3 FCs (Rados 6/6/6 server; CephFS 3/3/3), Production more server
- Uneven distribution makes behaviour in error case unpredictable



<!-- .slide: data-state="normal" id="EC-4" data-timing="20s" data-menu-title="Rados - 2 FCs - failures" -->
## Rados Pool

### Failure Scenarios - 2 FCs

<table width="80%">
 <colgroup>
      <col width="20%">
      <col width="20%">
      <col width="20%">
      <col width="20%">
      <col width="20%">
 </colgroup>
 <tr>
     <th height="60"></th>
     <th align="center">1 FC</th>
     <th align="center">+1 Server</th>
     <th align="center">+1 OSD</th>
     <th align="center">min_size=k+1</th>
 </tr>
 <tr>
     <th align="center" height="60">6x</th>
     <td bgcolor="lightgreen"></td>
     <td bgcolor="lightgreen"></td>
     <td bgcolor="#ff9999"></td>
     <td bgcolor="#ff9999"></td>
 </tr>
 <tr>
     <th align="center" height="60">8x</th>
     <td bgcolor="lightgreen"></td>
     <td bgcolor="lightgreen"></td>
     <td bgcolor="lightgreen"></td>
     <td bgcolor="#ff9999"></td>
 </tr>
 <tr>
     <th align="center" height="60">k2m4</th>
     <td bgcolor="lightgreen"></td>
     <td bgcolor="lightgreen"></td>
     <td bgcolor="#ff9999"></td>
     <td bgcolor="#ff9999"></td>
 </tr>
 <tr>
     <th align="center" height="60">k4m8</th>
     <td bgcolor="lightgreen"></td>
     <td bgcolor="lightgreen"></td>
     <td bgcolor="lightgreen"></td>
     <td bgcolor="#ff9999"></td>
 </tr>
 <tr>
     <th align="center" height="60">k3m7</th>
     <td bgcolor="lightgreen"></td>
     <td bgcolor="lightgreen"></td>
     <td bgcolor="lightgreen"></td>
     <td bgcolor="#ff9999"></td>
 </tr>
</table>

Note:
- k+m should be something that can be devided by 2 to get even distribution
- Replication no option, to expensive due to full copies
- k4m8: all server in use -> no recovery
- Issue with both: failure of a FC
- k3m7: 2 server left for recovery with min_size=k


<!-- .slide: data-state="normal" id="EC-5" data-timing="20s" data-menu-title="Rados - 3 FCs" -->
## Rados Pool

### Failure Scenarios - 3 FCs

<table width="80%">
 <colgroup>
      <col width="20%">
      <col width="20%">
      <col width="20%">
      <col width="20%">
      <col width="20%">
 </colgroup>
 <tr>
     <th height="60"></th>
     <th align="center">1 FC</th>
     <th align="center">+1 Server</th>
     <th align="center">+1 OSD</th>
     <th align="center">min_size=k+1</th>
 </tr>
 <tr>
     <th align="center" height="60">k2m4</th>
     <td bgcolor="lightgreen"></td>
     <td bgcolor="lightgreen"></td>
     <td bgcolor="lightgreen"></td>
     <td bgcolor="#ff9999"></td>
 </tr>
 <tr>
     <th align="center" height="60">k3m6</th>
     <td bgcolor="lightgreen"></td>
     <td bgcolor="lightgreen"></td>
     <td bgcolor="lightgreen"></td>
     <td bgcolor="lightgreen"></td>
 </tr>
 <tr>
     <th align="center" height="60">k4m5</th>
     <td bgcolor="lightgreen"></td>
     <td bgcolor="lightgreen"></td>
     <td bgcolor="lightgreen"></td>
     <td bgcolor="#ff9999"></td>
 </tr>
 <tr>
     <th align="center" height="60">k3m8</th>
     <td bgcolor="lightgreen"></td>
     <td bgcolor="lightgreen"></td>
     <td bgcolor="lightgreen"></td>
     <td bgcolor="lightgreen"></td>
 </tr>
 <tr>
     <th align="center" height="60">k6m6</th>
     <td bgcolor="lightgreen"></td>
     <td bgcolor="lightgreen"></td>
     <td bgcolor="lightgreen"></td>
     <td bgcolor="#ff9999"></td>
 </tr>
</table>

Note:
- k+m should be something that can be devided by 3 to get even distribution
- k6m6: 1FC+1OSD not covered, all in use, poor READ performance
- k4m8 and k6m6 need more than 12 server, otherwise in testing no recovery


<!-- .slide: data-state="normal" id="EC-6" data-timing="20s" data-menu-title="CephFS Pool" -->
## CephFS Pools

### Already 3 FCs, limited set of servers

### Replication needed for CephFS metadata pool
* needs also to cover all scenarios
* small pool

### EC for CephFS data pool

Note:
- only 9 SSD server available, in Production max. 15-18


<!-- .slide: data-state="normal" id="EC-7" data-timing="20s" data-menu-title="CephFS Pool - Failues" -->
## CephFS Pools

### Failure Scenarios - 3 FCs

<table width="80%">
 <colgroup>
      <col width="20%">
      <col width="20%">
      <col width="20%">
      <col width="20%">
      <col width="20%">
 </colgroup>
 <tr>
     <th height="60"></th>
     <th align="center">1 FC</th>
     <th align="center">+1 Server</th>
     <th align="center">+1 OSD</th>
     <th align="center">min_size=k+1</th>
 </tr>
 <tr>
     <th align="center" height="60">6x</th>
     <td bgcolor="lightgreen"></td>
     <td bgcolor="lightgreen"></td>
     <td bgcolor="#ff9999"></td>
     <td bgcolor="#ff9999"></td>
 </tr>
 <tr>
     <th align="center" height="60">9x</th>
     <td bgcolor="lightgreen"></td>
     <td bgcolor="lightgreen"></td>
     <td bgcolor="lightgreen"></td>
     <td bgcolor="lightgreen"></td>
 </tr>
 <tr>
     <th align="center" height="60">k2m4</th>
     <td bgcolor="lightgreen"></td>
     <td bgcolor="lightgreen"></td>
     <td bgcolor="lightgreen"></td>
     <td bgcolor="#ff9999"></td>
 </tr>
 <tr>
     <th align="center" height="60">k3m6</th>
     <td bgcolor="lightgreen"></td>
     <td bgcolor="lightgreen"></td>
     <td bgcolor="lightgreen"></td>
     <td bgcolor="lightgreen"></td>
 </tr>
 <tr>
     <th align="center" height="60">k4m5</th>
     <td bgcolor="lightgreen"></td>
     <td bgcolor="lightgreen"></td>
     <td bgcolor="lightgreen"></td>
     <td bgcolor="#ff9999"></td>
 </tr>
</table>

Note:
- 9x replica does not allow recovery, same as the EC except k2m4
- more server needed in production


<!-- .slide: data-state="normal" id="EC-8" data-timing="20s" data-menu-title="Space Overhead" -->
## Space Overhead
<canvas data-chart="bar">
<!--
{
 "data" : {
     "labels": ["NFS", "6x", "8x", "9x", "k2m4", "k3m6", "k3m7", "k4m5", "k4m8", "k6m6"],
     "datasets": [
         {
             "label": "Space Overhead",
             "yAxesGroup": "space",
             "data": [138, 500, 700, 800, 200, 200, 233, 125, 200, 100],
             "backgroundColor": [
                 "rgba(166, 206, 227, 0.3)",
                 "rgba(31, 120, 180, 0.3)",
                 "rgba(178, 223, 138, 0.3)",
                 "rgba(51, 160, 44, 0.3)",
                 "rgba(251, 154, 153, 0.3)",
                 "rgba(227, 26, 28, 0.3)",
                 "rgba(253, 191, 111, 0.3)",
                 "rgba(255, 127, 0, 0.3)",
                 "rgba(202, 178, 214, 0.3)"]
         }
     ]
 },
 "options": {
     "animateScale": "true",
     "responsive": "true",
     "legend": {
           "display": 0
     },
     "layout": {
            "padding": {
                "left": 0,
                "right": 0,
                "top": 40,
                "bottom": 0
            }
     },
     "plugins": {
         "datalabels": {
             "align": "end",
             "anchor": "end"
         }
     },
     "scales": {
         "yAxes": [{
             "gridLines": {
                 "color": "rgba(0, 0, 0, 0)"
             },
             "ticks": {
                 "display": 0
             }
         }],
         "xAxes": [{
             "gridLines": {
                 "color": "rgba(0, 0, 0, 0)"
             }
         }]
     }
 }
}
-->
</canvas>


<!-- .slide: data-state="normal" id="EC-9" data-timing="20s" data-menu-title="Cluster settings" -->
## Settings

### Rados <!-- .element: class="fragment" data-fragment-index="0" -->
* Testing: k3m7 <!-- .element: class="fragment" data-fragment-index="0" -->
* PoC: k4m5 <!-- .element: class="fragment" data-fragment-index="0" -->

### CephFS <!-- .element: class="fragment" data-fragment-index="1" -->
* data: k2m4 <!-- .element: class="fragment" data-fragment-index="1" -->
* meta_data: 6x replication <!-- .element: class="fragment" data-fragment-index="1" -->
* Ops may need to intervene <!-- .element: class="fragment" data-fragment-index="1" -->
* Cluster able to run recovery <!-- .element: class="fragment" data-fragment-index="1" -->

### Production <!-- .element: class="fragment" data-fragment-index="2" -->
* EC/Replication need to change again <!-- .element: class="fragment" data-fragment-index="2" -->

Note:
- Rados settings: comparable regarding chunks written, PoC less overhead
- CephFS settings same for both
- CephFS: k3m6 not selected due to k+m="number of available servers"
- Ceph: In case of max error OPS need to inervene to ensure max_size=k+1 handling.

