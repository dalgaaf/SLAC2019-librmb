<!-- .slide: data-state="section-break" id="section-break-3.1" data-timing="10s" -->
# Ceph and Mails


<!-- .slide: data-state="normal" id="ceph-store-emails-0" data-timing="20s" data-menu-title="Ceph: Option CephFS" -->
## Where to store emails in Ceph?

<div>
    <img style="width: 35%; left: 55%; position: absolute" alt="CephFS"
         data-src="images/cephfs.svg" />
</div>

### CephFS

* POSIX layer adds complexity <!-- .element class="fragment" -->
* suffers from similar issues as NFS <!-- .element class="fragment" -->
* no significant advantage for mail storage <!-- .element class="fragment" -->
* usable for metadata/caches/indexes <!-- .element class="fragment" -->
<br>
<br>

### Security <!-- .element class="fragment" -->
* requires direct access to storage network <!-- .element class="fragment" -->
* only for dedicated platform <!-- .element class="fragment" -->

Note:
- there is no significant advantage to NFS especially with cost and effort to switch from well working systems.


<!-- .slide: data-state="normal" id="ceph-store-emails-1" data-timing="20s" data-menu-title="Ceph: Option RBD" -->
## Where to store emails in Ceph?

<div>
    <img style="width: 35%; left: 55%; position: absolute" alt="RBD"
         data-src="images/rbd.svg" />
</div>

### RBD

* sharding and large RBDs <!-- .element class="fragment" -->
  * account migration <!-- .element class="fragment" -->
  * RBD/fs extend scenarios <!-- .element class="fragment" -->
* still includes POSIX layer like NFS <!-- .element class="fragment" -->
* no sharing between clients <!-- .element class="fragment" -->
* impracticable <!-- .element class="fragment" -->
<br>
<br>

### Security <!-- .element class="fragment" -->
* no direct access to storage network required <!-- .element class="fragment" -->
* secure through hypervisor abstraction (libvirt) <!-- .element class="fragment" -->


<!-- .slide: data-state="normal" id="ceph-store-emails-2" data-timing="20s" data-menu-title="Ceph: Option RadosGW" -->
## Where to store emails in Ceph?

<div>
    <img style="width: 35%; left: 55%; position: absolute" alt="RGW"
         data-src="images/rgw.svg" />
</div>

### RadosGW
* store emails as objects <!-- .element class="fragment" -->
* additional server/service <!-- .element class="fragment" --> 
* extra network hops <!-- .element class="fragment" -->
* potential bottleneck <!-- .element class="fragment" -->
* very likely not fast enough <!-- .element class="fragment" -->
<br>
<br>

#### <b>Security</b> <!-- .element class="fragment" -->
* no direct access to Ceph storage network required <!-- .element class="fragment" -->
* connection to RadosGW can be secured (WAF) <!-- .element class="fragment" -->


<!-- .slide: data-state="normal" id="ceph-store-emails-3" data-timing="20s" data-menu-title="Ceph: Option librados" -->
## Where to store emails in Ceph?

<div>
    <img style="width: 35%; left: 55%; position: absolute" alt="librados"
         data-src="images/librados.svg" />
</div>

### Librados
* direct access to RADOS <!-- .element class="fragment" -->
* parallel I/O <!-- .element class="fragment" -->
* not optimized for email use case<!-- .element class="fragment" -->
* how to handle metadata/caches/indexes? <!-- .element class="fragment" -->
<br>
<br>

#### <b>Security</b> <!-- .element class="fragment" -->
* requires direct access to storage network <!-- .element class="fragment" -->
* only for dedicated platform <!-- .element class="fragment" -->

