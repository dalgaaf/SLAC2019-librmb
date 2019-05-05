<!-- .slide: data-state="section-break" id="section-break-3" data-timing="10s" -->
# Ceph


<!-- .slide: data-state="normal" id="ceph-overview" data-timing="20s" data-menu-title="Ceph Components" -->
<center><img src="images/ceph-stack.svg" style="width:80%"></center>

NOTE: well known picture, short info on components


<!-- .slide: data-state="normal" id="ceph-store-emails-2" data-timing="20s" data-menu-title="Ceph: Option CephFS" -->
## Where to store in Ceph?

<div>
    <img style="width: 35%; left: 55%; position: absolute" alt="CephFS"
         data-src="images/cephfs.svg" />
</div>

### CephFS

* same issues as NFS <!-- .element class="fragment" -->
* mail storage on POSIX layer adds complexity <!-- .element class="fragment" -->
* no option for emails <!-- .element class="fragment" -->
* usable for metadata/caches/indexes <!-- .element class="fragment" -->
<br>
<br>

#### <b>Security</b> <!-- .element class="fragment" -->
* requires direct access to storage network <!-- .element class="fragment" -->
* only for dedicated platform <!-- .element class="fragment" -->


<!-- .slide: data-state="normal" id="ceph-store-emails-3" data-timing="20s" data-menu-title="Ceph: Option RBD" -->
## Where to store in Ceph?

<div>
    <img style="width: 35%; left: 55%; position: absolute" alt="RBD"
         data-src="images/rbd.svg" />
</div>

### RBD

* needs sharding and large RBDs <!-- .element class="fragment" -->
* needs account migration and RBD/fs extend scenarios <!-- .element class="fragment" -->
* still includes POSIX layer like NFS <!-- .element class="fragment" -->
* no sharing between clients <!-- .element class="fragment" -->
* impracticable <!-- .element class="fragment" -->
<br>
<br>

#### <b>Security</b> <!-- .element class="fragment" -->
* no direct access to storage network required <!-- .element class="fragment" -->
* secure through hypervisor abstraction (libvirt) <!-- .element class="fragment" -->


<!-- .slide: data-state="normal" id="ceph-store-emails-4" data-timing="20s" data-menu-title="Ceph: Option RadosGW" -->
## Where to store in Ceph?

<div>
    <img style="width: 35%; left: 55%; position: absolute" alt="RGW"
         data-src="images/rgw.svg" />
</div>

### RadosGW
* can store emails as objects <!-- .element class="fragment" -->
* extra network hops <!-- .element class="fragment" -->
* potential bottleneck <!-- .element class="fragment" -->
* very likely not fast enough <!-- .element class="fragment" -->
<br>
<br>

#### <b>Security</b> <!-- .element class="fragment" -->
* no direct access to Ceph storage network required <!-- .element class="fragment" -->
* connection to RadosGW can be secured (WAF) <!-- .element class="fragment" -->


<!-- .slide: data-state="normal" id="ceph-store-emails-5" data-timing="20s" data-menu-title="Ceph: Option librados" -->
## Where to store in Ceph?

<div>
    <img style="width: 35%; left: 55%; position: absolute" alt="librados"
         data-src="images/librados.svg" />
</div>

### Librados
* direct access to RADOS <!-- .element class="fragment" -->
* parallel I/O <!-- .element class="fragment" -->
* not optimized for emails <!-- .element class="fragment" -->
* how to handle metadata/caches/indexes? <!-- .element class="fragment" -->
<br>
<br>

#### <b>Security</b> <!-- .element class="fragment" -->
* requires direct access to storage network <!-- .element class="fragment" -->
* only for dedicated platform <!-- .element class="fragment" -->
