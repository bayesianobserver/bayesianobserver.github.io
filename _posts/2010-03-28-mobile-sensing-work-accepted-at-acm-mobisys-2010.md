---
layout: post
title: "Compressive sensing of vacant parking spaces with mobile sensors"
date: 2010-03-28
original_url: "https://thebayesianobserver.wordpress.com/2010/03/28/mobile-sensing-work-accepted-at-acm-mobisys-2010/"
categories: ["learning", "mobile", "mobile-systems", "sensing", "vehicular"]
---
My work on mobile sensing for automotive parking applications has just been accepted to ACM Mobisys 2010 and I will br presenting this work at Mobisys in San Francisco in June 2010. The paper is about the design, implementation and evaluation of a mobile sensing system called ParkNet, for the purpose of harvesting in as close to real time as possible, information about the availability street-parking spaces in urban areas. ParkNet was recently featured in the [MIT Technology review](http://www.technologyreview.com/communications/24497/page1/). It has just been covered by Rutgers Today, an organization within Rutgers University that produces news articles about promising research efforts within Rutgers. ParkNet proposes that sensors for sensing vacant street side parking spaces be made mobile (see this project trial that uses stationary sensors installed in the asphalt road, one sensor per spot, presumably at a huge cost) by exploiting vehicles that regularly comb city environment, such as taxicabs. ParkNet can be thought of as a compressive sensing system because it drastically reduces the number of sensors needed [with a corresponding dramatic decrease in overall cost], with a very small loss in spatio-temporal accuracy.

[![](/images/mobile-sensing-work-accepted-at-acm-mobisys-2010-img-1.png "ParkNet San Francisco Taxicab study - 1 cab over 1 month")](https://thebayesianobserver.wordpress.com/wp-content/uploads/2010/03/screen-shot-2011-10-22-at-3-38-40-pm.png)

Naturally, one of the things I needed to figure out was: how well can a fleet of N taxicabs cover a given geographical area, in terms of mean time between successive cabs visiting a given street? How does this number vary with N. The [San Francisco Taxicab](http://cabspotting.org/) [dataset](http://crawdad.cs.dartmouth.edu/meta.php?name=epfl/mobility) came in handy. The visualization on the right is made with good old Matlab©. It shows GPS coordinates of a single taxicab in the San Francisco area, measured about once per minute, over a period of 30 days. When I plotted this, I immediately realized that taxicabs would be great for ParkNet because most taxicabs tend to spend most of their time in the crowded downtown area of the city (dense, upper right corner in the plot), and this is where the parking problem is most serious.

Update: My ParkNet paper received the best paper award at ACM’s annual Mobile Systems and Applications Conference [ACM Mobisys]!

![]()
