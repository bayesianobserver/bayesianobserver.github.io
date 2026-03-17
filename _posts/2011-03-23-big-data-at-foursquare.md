---
layout: post
title: "Big data at Foursquare"
date: 2011-03-23
original_url: "https://thebayesianobserver.wordpress.com/2011/03/23/big-data-at-foursquare/"
categories: ["data", "math"]
---
Attended a meeting of the NY ML meetup. The speakers presented on the BIG DATA work happening at foursquare. I noticed that the speakers as well as the audience is heavily tilted towards programming rather than statistics/ml. Most questions were about hadoop, hive and mongo db. Hardly any questions about the statistical aspects. This could be because the audience understood the math behind recommendation systems quite well. One exception was the ‘cold start’ problem.

One thing that surprised me was that Foursquare doesn’t use matrix factorization but simpler nearest neighbor methods! I asked. Bell, koren and volinsky showed in the Netflix prize that latent models based on matrix factorization are better than NN.

Also felt that some of the questions were interesting ideas. For example, how they can collect implicit feedback by noticing what a user does after being offered recommendations. I thought this was a really neat idea for tuning the recommendations for a user — someone in the audience asked if they were doing it, and they replied they aren’t but they are thinking about it.
