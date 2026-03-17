---
layout: post
title: "Location Privacy"
date: 2008-05-05
original_url: "https://thebayesianobserver.wordpress.com/2008/05/05/location-privacy/"
categories: ["privacy"]
---
I attended some interesting talks at the [3rd Rutgers-Helsinki PhD Student Workshop on Spontaneous and Pervasive Networking](http://discolab.rutgers.edu/workshops/2008/index.html) (phew!) today. In particular, a talk by Marco Gruteser reviewing location privacy for various applications caught my eye. Location based services have been much talked about and are expected to take off (any moment now) in a big way. This introduces the problem of preserving user-privacy. Marco talked about an interesting class of problems that deal with preserving the privacy of location traces. The idea is as follows: Each mobile client periodically transmits its location to a central server, which then forwards this information on to a application service provider (ASP) that provides some location-based service to the user. (Think [DASH](http://www.dash.net/)!) However, the user wishes to conceal its identity to the ASP. Hence we would like to make it impossible (or very hard) to infer the user’s identity from observing location updates.

Marco’s group has proposed a centralized processing architecture for solving the problem, wherein the location updates from all users are first ‘anonymized’ by a central server (call it the ‘location broker’) by what can be termed verious signal processing techniques such as dropping a few samples, shifting the time stamps a bit, etc. Note that the degree of location privacy granted to a user is a coupled function of the information about other users that is revealed by the location broker to the ASP.

An interesting extension of the problem would be to engineer a system wherein the availability of a location broker cannot be guaranteed and users wish to solve the problem themselves, i.e. a distributed architecture for the problem of location privacy/ praivacy of location traces. Ostensibly, this would require some cooperation /message passing between the mobile clients because intuitively, the degree of anonymity enjoyed by a user is a function of the user density in its surroundings. Something to think about..

![](https://blogger.googleusercontent.com/tracker/8218408692418372840-3038960936329812716?l=thebayesianobserver.blogspot.com)
