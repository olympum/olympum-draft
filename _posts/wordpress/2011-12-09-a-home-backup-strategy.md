---
layout: post
title: A Home Backup Strategy
date: 2011-12-09 06:07:53.000000000 +00:00
categories:
- Future
tags: []
status: publish
type: post
published: true
meta:
  tmac_last_id: '531409133556076544'
  _jetpack_related_posts_cache: a:1:{s:32:"8f6677c9d6b0f903e98ad32ec61f8deb";a:2:{s:7:"expires";i:1415514431;s:7:"payload";a:3:{i:0;a:1:{s:2:"id";i:225;}i:1;a:1:{s:2:"id";i:251;}i:2;a:1:{s:2:"id";i:21;}}}}
  _wpcom_is_markdown: '1'
  _edit_last: '1'
author:
  login: admin
  email: brunofr@olympum.com
  display_name: Bruno Fernandez-Ruiz
  first_name: Bruno
  last_name: Fernandez-Ruiz
---
For years I've been continuously fighting with backups. I have not been particularly good or consistent at it. We've been okay with Time Machine and Carbon Copy Cloner, but the recent addition of a digital SLR to our gadget collection has meant running out of space on our shared home drive.

Historically I'd been using a WD My Book 2x1 TB RAID1 array connected to an
Apple Airport Extreme and shared via AirDisk (afp). We had Time Machine backup
all the computers in the house in the AirDisk. We'd also store our photos and
videos, etc. in the AirDisk. Aside running out of space, we had no good
offsite strategy. Given that our digital picture collection is continuously
becoming more and more valuable as a family history artifact, I though it was
time to address this properly, rather than just adding more space.

I started by classifying the risk associated with each data type:

* **Personal files**: document scans, photos, videos, etc. This is the
  critical part of the equation. In case of fire or theft we'd have no
  replacement and the loss would be HUGE.
* **Shared Media**: movies, music, etc. These are regrettable if lost,
  but can be restore. I know how to find them back, even though it
  might be painful or costly.
* **Backups**: the time machine backups from our home computers. Since
  we have the laptops plus the backup, I was not too worried about
  losing this.

Since no all data is born equal, the required reliability levels vary. For
personal files, I want to be covered against hardware failures. For the other
kinds, I don't mind that much.

Additionally, for videos, I want to have the ability to connect the storage
unit directly to my computer while editing (my experience editing over the
network has not been great).

Finally, I really wanted an offsite backup for our personal data.

Given these constrains, I struggled to find a good (cost-effective)
combination, and since I think I've found something that works well for me, I
thought I'd share with others just in case this helps:


* Airport Extreme Station 802.11n 2nd Generation (100/1000) (any 1
  Gbps switch would do).
* Buffalo LinkStation Pro Duo 2x3 TB (NAS), connected to AES via 1
  Gbps ethernet. Setup as RAID1 and exposing two afp shares (Personal,
  Media) and a Time Machine 'Backup' share that each computer uses to
  create a separate sparsebundle.
* 2x WD My Book 2x1 TB on RAID0, mounted 'usbdisk', connected via USB
  to LinkStation and used to backup incrementally every night from the
  NAS internal disks. Every week I rotate the USB WD drive units
  between office and home.
* If I want to edit video, I unmount the USB drive and connect via
  Firewire to my computer for doing video edits. When I mount it back,
  I manually copy the edits back to the NAS internal drives. This is
  the only manual step in the process.
* The media files are exposed through the embedded server in the
  LinkStation via UPnP and iTunes Server. This allows me to use Boxee
  on any computer (and a patched Apple TV 2nd gen) to watch our
  videos. We also share iTunes music this way without having to share
  libraries.

I ended up putting all the data under RAID1, but I think the cost is low since
we mostly only read from the array (except the backups). With this setup:

* We have Time Machine for all computers in the house, happening over
  the network and transparently.
* We can access all data both via afp mounts as well as directly via
  USB/FW for intensive reads / edits.
* We have an offsite copy.

Overall, I am happy with the setup. I was initially worried about using a
home-grade NAS, but even though the LS is slow for writes, it's actually fast
for reads, so I am happy.
