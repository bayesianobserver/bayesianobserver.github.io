---
layout: post
title: "Mobicom paper accepted!"
date: 2008-07-29
original_url: "https://thebayesianobserver.wordpress.com/2008/07/29/mobicom-paper-accepted/"
categories: ["uncategorized"]
---
My [Mobicom](http://www.sigmobile.org/mobicom/2008/) paper has officially been accepted – now that the several rounds of changes and formatting issues have been fixed (I was both surprised and amazed as the painstaking detail with which ACM perused the paper; IEEE standards fall pale in comparison).

The paper is titled ‘Radio-telepathy: Extracting Secret Bits from an Unauthenticated Wireless Channel’. In this paper, I teamed up with some folks over at InterDigital to build a system that can use the received signal from 802.11 cards to ‘extract’ bits at the two ends of a wireless channel, in such a way that a third user cannot infer any useful information about the bits that were extracted. The idea is to enable generation of identical bit sequences at the two ends, which can then be used as cryptographic keys for encrypting future communications. What is more, these keys can be refreshed at regular intervals using channel information that the 802.11 system can extract from regular received packets.

The system we proposed provides an analog of quantum cryptography for ‘everyday wireless channels’. While QC relies on the quantum physics behind photons, our proposed system relies on two simple, somewhat surprising but verifiable properties of the wireless medium: (1) The channel decorrelates in space very quickly – over distances of the oder of a wavelength (a few cm for 802.11) and (2) The wireless channel is, toa good extent, reciprocal. This means that although it is continuously changing in time, at a fixed instant of time and at a  fixed frequency, the channel behaves in exactly the same way, irrespective of whether Alice transmits and Bob receives, or vice-versa. In practice, it is hard to have both users transmit and receive simultaneously, so there is a small time-delay between transmissions in the two directions. However, if this delay is small, then the channel only has a chance to change by a small amount and is still heavily correlated.

The most notable point about our algorithm is that it provides *information theoretic secrecy.* This means that the secrecy of the keys extracted is *unconditional –* it does not depend upon the assumption of a computationally bounded adversary or the computational hardness of a mathematical problem.

I’m looking forward to attending the conference in September. There are a number of o[ther very interesting papers](http://www.sigmobile.org/mobicom/2008/program.html) in wireless and otherwise.

![](https://blogger.googleusercontent.com/tracker/8218408692418372840-3513118536786775515?l=thebayesianobserver.blogspot.com)
