---
layout: post
title: "Commercial localization in shopping malls using GNURadio"
date: 2008-05-28
original_url: "https://thebayesianobserver.wordpress.com/2008/05/28/commercial-localization-in-shopping-malls-using-gnuradio/"
categories: ["privacy", "security"]
---
I came across a company named Path Intelligence that is selling equipment to track consumer’s locations passively using their cellphone signals inside shopping centers, malls, etc. ostensibly for the purpose of tracking consumer behavior. Apparently, their ‘equipment’ is centered around the GNUradio platform and uses triangulation based schemes for localization. What is interesting to me is that:

(1) They manage to use signals from cellphone even when the phone is not in a voice call (There must be some beacons!?)  
(2) They manage to simultaneously localize multiple phones.  
(3) The company website claims accuracy of 1-2 meters

It appears that early adopters of their solution are in the UK. A large mall can be covered by 20 of their ‘boxes’.

The Privacy issue:  
“The Information Commissioner’s Office (ICO) expressed cautious approval of the technology, which does not identify the owner of the phone but rather the handset’s IMEI code – a unique number given to every device so that the network can recognise it.”

So they don’t just track the pure signal but they also demodulate the IMEI code – a reverse lookup may reveal IMEI -> Phone number -> identity but would probably require the cooperation of the carrier. Unlike MAC addresses in 802.11 networks, the IMEI cannot be changed as easily. From a privacy perspective, it appears that the IMEI is therefore a really bad thing (it is unencrypted) as it could potentially allow one to be spied upon (location traces, etc etc.) There are various other privacy issues especially when such a technology is put into effect without having shoppers sign disclosure forms. The [page on slashdot](http://yro.slashdot.org/article.pl?sid=08/05/18/1838222&from=rss) has many interesting user comments.  
Some links are [here](http://technology.timesonline.co.uk/tol/news/tech_and_web/article3945496.ece), [here](http://www.pathintelligence.com/website-aboutus.htm) and [here.](http://photos1.blogger.com/photoInclude/blogger/6124/1637/1600/path_intelligence.jpg)

[Here](http://p10.hostingprod.com/@spyblog.org.uk/blog/2008/05/path-intelligence-footpathtm-a-few-more-details.html) is an email from Toby Oliver, the owner and CEO of Path Intelligence explaining the technology in an effort to allay concerns.

Here is a particularly insightful comment from Slashdot that brings out the ‘value’ of location information rather than worrying about privacy:

> *“My shop usage data have great financial value (otherwise the shops wouldn’t pay to install surveillance systems) and the shop’s surveillance is involuntary – I am not given a choice whether to allow them track me or not, except if I avoid transmitting wireless signals while near their shop. As the data collection is not voluntary and my shop usage data have financial value, I demand payment from shops using this system. I want a share of my shop usage data’s financial value.”*

I think this makes a good case for researching PHY-layer based location privacy. Having simple omni transmitters is equivalent to relinquishing one’s privacy as well as volunteering usage data for free.

![](https://blogger.googleusercontent.com/tracker/8218408692418372840-7546904893812666729?l=thebayesianobserver.blogspot.com)
