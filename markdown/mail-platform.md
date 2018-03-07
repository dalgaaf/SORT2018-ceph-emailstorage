<!-- .slide: data-state="section-break" id="section-break-3" data-timing="10s" -->
# How to store
# 6.7b emails in Ceph


<!-- .slide: data-state="normal" id="telekommail" data-timing="20s" data-menu-title="TelekomMail" -->
## TelekomMail platform

* DT's mail platform for customers <!-- .element class="fragment" data-fragment-index="1"-->
* dovecot <!-- .element class="fragment" data-fragment-index="2"-->
* Network-Attached Storage (NAS) <!-- .element class="fragment" data-fragment-index="3"-->
* NFS (sharded) <!-- .element class="fragment" data-fragment-index="4"-->
* ~39 million accounts <!-- .element class="fragment" data-fragment-index="5"-->
* ~1.3 petabyte net storage <!-- .element class="fragment" data-fragment-index="6"-->
  * ~6.7 billion emails <!-- .element class="fragment" data-fragment-index="7"-->
  * ~1.2 billion index/cache/metadata files <!-- .element class="fragment" data-fragment-index="8"-->
  * ~42% usable raw space <!-- .element class="fragment" data-fragment-index="9"-->

Note: emails are stored compressed


<!-- .slide: data-state="normal" id="mailplatform-nfs" data-timing="20s" data-menu-title="NFS Operations" -->
## NFS Operations

<center><img src="images/nfs-ops_libreoffice_noframe.png" style="width:90%"></center>


<!-- .slide: data-state="normal" id="mailplatform-nfs" data-timing="20s" data-menu-title="NFS Traffic" -->
## NFS Traffic

<center><img data-src="images/nfs-traffic_libreoffice_noframe.png" style="width:90%"></center>


<!-- .slide: data-state="normal" id="mailplatform-nfs-stats" data-timing="20s" data-menu-title="NFS relevant IOs" -->
## NFS relevant IOs

<center><img data-src="images/nfs-ops_relevant_libreoffice_noframe.png" style="width:90%"></center>


<!-- .slide: data-state="normal" id="mailplatform-mails-dist" data-timing="20s" data-menu-title="Email distribution" -->
## Email Distribution
<center><img src="images/email-size-distribution_libreoffice_new.png" style="width:90%"></center>

Note: avg 42 KiB, max 600 MiB


<!-- .slide: data-state="normal" id="store-emails" data-timing="20s" data-menu-title="How stored?" -->
## How are emails stored?

### Emails are written once, read many (WORM) <!-- .element class="fragment" data-fragment-index="0"-->

### mailbox, maildir <!-- .element class="fragment" data-fragment-index="1"-->

### Usage depends on: <!-- .element class="fragment" data-fragment-index="2"-->
  * protocol (IMAP vs POP3) <!-- .element class="fragment" data-fragment-index="2"-->
  * user frontend (mailer vs webmailer) <!-- .element class="fragment" data-fragment-index="2"-->

### usually separated metadata, caches and indexes <!-- .element class="fragment" data-fragment-index="3"-->
  * lost of metadata/indexes is critical <!-- .element class="fragment" data-fragment-index="3"-->

### without attachments easy to compress <!-- .element class="fragment" data-fragment-index="4"-->


<!-- .slide: data-state="normal" id="project-motivation" data-timing="20s" data-menu-title="Project Motivation" -->
## Motivation

* faster and automatic self healing <!-- .element class="fragment" data-fragment-index="1"-->
* less IO overhead <!-- .element class="fragment" data-fragment-index="2"-->
* prevent vendor lock-in <!-- .element class="fragment" data-fragment-index="3"-->
* commodity hardware <!-- .element class="fragment" data-fragment-index="4"-->
* open source where feasible <!-- .element class="fragment" data-fragment-index="5"-->
* reduce Total Cost of Ownership <!-- .element class="fragment" data-fragment-index="6"-->
