---
layout: post
title: 'NatWest Online Banking: Card Reader'
date: 2007-08-07 13:07:27.000000000 +01:00
categories:
- Security
tags: []
status: publish
type: post
published: true
meta:
  tmac_last_id: '531409246500704256'
  _jetpack_related_posts_cache: a:1:{s:32:"8f6677c9d6b0f903e98ad32ec61f8deb";a:2:{s:7:"expires";i:1415356686;s:7:"payload";a:3:{i:0;a:1:{s:2:"id";i:49;}i:1;a:1:{s:2:"id";i:273;}i:2;a:1:{s:2:"id";i:279;}}}}
author:
  login: admin
  email: brunofr@olympum.com
  display_name: Bruno Fernandez-Ruiz
  first_name: Bruno
  last_name: Fernandez-Ruiz
---

On Friday I received and "Online Banking Card Reader" from NatWest, my bank here in the UK. Let me tell you, it is one of a curious kind.

<p>NatWest issued me a new debit card a few weeks back now, although it was actually not due. The chip in the new card looked slightly different from the one on the last one, but it is still an EPROM with 255 bytes of storage. I have not read its contents yet ... I am sure I am bound by some dubious legal agreement not to do it anyway.</p>
<p>The device is roughly the size of a smallish pocket calculator. It is a Xiring device, patented by French company Xiring. The device has a PIN-and-chip reader where you slide your debit card into, and it then prompts you for input. The device has three modes of operation:</p>
<p>* Identity, enter a secret (your PIN) and receive back a secure code.<br />
* Respond, enter a secret and a (reference) number and receive back a secure code.<br />
* Sign, enter a secret, a (reference) number and an amount, and receive back a secure code.</p>
<p>It seems like a useful device, more secure than the current password solution RBS/NatWest has. The only way to do online banking in the future with NatWest will be through this device.</p>
<p>I am not sure about it though. The device is nothing but a fancy electronic challenge/response card, but highly inconvenient to the consumer. The device relies on batteries and it's very bulky compared to a card you can slot into your wallet.</p>
<p>My bet is that we will see massive pushback.</p>
