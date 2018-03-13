<!-- .slide: data-state="cover" id="cover-page" data-timing="20" -->
<img src="images/Ceph_Logo_Stacked_RGB_120411_fa.png" style="width:20%; left: 85%; top:-2%; position: absolute">
SORT 2018 - Cologne
<br>
<br>
<br>
## Ceph Luminous/Mimic
and 
<br>
## How to store 6.7 billion emails
<br>
Danny Al-Gaaf <br>
Deutsche Telekom Technik GmbH - FMED
<br>
<img src="images/T_Logo_3c_p_DE.png" style="width:10%; left: -1.5%; position: absolute">


<!-- .slide: data-state="normal" id="ceph-overview" data-timing="20s" data-menu-title="Ceph Components" -->
<center><img src="images/ceph-stack.svg" style="width:90%"></center>

NOTE: well known picture, short info on components


<!-- .slide: data-state="normal" id="ceph-daemons" data-timing="20s" data-menu-title="Ceph Daemons" -->
<center><img src="images/cephfs_legend.svg" style="width:65%"></center>


<!-- .slide: data-state="normal" id="ceph-openstack-block" data-timing="20s" data-menu-title="OpenStack Block" -->
<center><img src="images/OS-Storage-April2017SurveyReport.svg" style="width:85%"></center>

Note: OpenStack User Survey April 2017, November: RBD 67%, LVM 21%, Huawei 16%, NetApp 13%, NFS 10%, EMC 7%, Rest less than 4%


<!-- .slide: data-state="section-break" id="ceph-release-timeline-1" data-menu-title="Ceph Release Timeline" data-background-image="images/ceph-release-timeline.png" data-background-size="cover" data-timing="10s" -->


<!-- .slide: data-state="normal" id="ceph-release-timeline-2" data-timing="20s" data-menu-title="New Release Cycle" -->
## New Release Cycle

### Till Luminous <!-- .element class="fragment" data-fragment-index="1"-->
* 6 month release cycle <!-- .element class="fragment" data-fragment-index="1"-->
* every second release were LTS <!-- .element class="fragment" data-fragment-index="1"-->
* too slow LTS cycle <!-- .element class="fragment" data-fragment-index="1"-->
* non-LTS used in production sometimes <!-- .element class="fragment" data-fragment-index="1"-->

### With Mimic <!-- .element class="fragment" data-fragment-index="2"-->
* 9 month release cycle, all releases are stable <!-- .element class="fragment" data-fragment-index="2"-->
* Bugfix backport for two subsequent releases <!-- .element class="fragment" data-fragment-index="2"-->
* Upgrade support for N-2 <!-- .element class="fragment" data-fragment-index="2"-->

### Vendors select releases for LTS in their products <!-- .element class="fragment" data-fragment-index="3"-->
