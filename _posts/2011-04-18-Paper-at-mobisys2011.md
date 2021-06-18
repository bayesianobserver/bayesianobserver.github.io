---
layout: post
title: "Paper at ACM Mobisys 2011"
date: 2011-04-18
mathjax: true
---



My paper titled 'ProxiMate: Proximity-based Secure Pairing using Ambient Wireless Signals' has been accepted at the 9th Annual International Conference on Mobile Systems, Applications and Services (ACM Mobisys) to be held at Washington D.C.. The paper is about how existing wireless signals, such as FM radio and TV signals, can be used by radios in close proximity to generate a shared secret, and then use that secret to communicate securely. By building a shared key in this manner, it is hoped that the problem of identity spoofing and eavesdropping on wireless links can be addressed. The principles at work in ProxiMate are: (i) Small-scale fading: the wireless channel between a distance RF source (such as an FM radio tower) and a receiver, behaves as a random process, thereby serving as a source of randomness, and (ii) receivers that are within half a wavelength of each other can observe highly correlated (but not identical) versions of these random processes, allowing wireless devices in proximity access to a shared source of common randomness that is not available to any sufficiently distant adversary. ProxiMate is a proof of concept system built on software-defined radio and evaluated using ambient FM and TV signals. It is intended to be information-theoretically secure -- meaning, the key generation phase does not need to assume a computationally bounded adversary -- as opposed to say, Diffie Hellman, which must assume a computationally bounded adversary in order to guarantee that the observations available to the adversary will not allow it to compute the key. On a side note, D.C. is one of the more boring cities to have a conference once you have done the museums circuit. Anyhow, looking forward to it!
