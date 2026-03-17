---
layout: post
title: "In the eye of the Beholder"
date: 2012-11-20
original_url: "https://thebayesianobserver.wordpress.com/2012/11/20/in-the-eye-of-the-beholder/"
categories: ["creativity", "data", "information-theory", "math", "sensing", "signal-processing"]
tags: ["art", "beauty", "hacking"]
---
Why is the picture on the right more appealing than the one on the left?

[![](/images/in-the-eye-of-the-beholder-img-1.png "Screen shot 2012-11-19 at 8.07.11 PM")](https://thebayesianobserver.wordpress.com/wp-content/uploads/2012/11/screen-shot-2012-11-19-at-8-07-11-pm.png)

What is it that we find more interesting about the picture on the right, compared to the one on the left? The picture on the left contains more information. So we are certainly not looking for more information. One might say we don’t know how to interpret the image on the left into anything familiar, but it is television static. A more precise answer is given by [Jurgen Schmidhuber](http://www.idsia.ch/~juergen/), who [argues convincingly](http://videolectures.net/ecmlpkdd2010_schmidhuber_ftf/) that:

> Artists (and observers of art) get rewarded for making (and observing) novel patterns: data that is neither arbitrary (like incompressible random white noise) nor regular in an already known way, but regular in way that is new with respect to the observer’s current knowledge, yet learnable (that is, after learning fewer bits are needed to encode the data).

This explains the pictures on top. The picture on the left is not compressible because it is a matrix of uniformly random 0/1 pixels. The Monet on the right evokes familiar feelings, and yet adds something new. I think what Schmidhuber is saying is that the amount of compressibility should neither be too little, nor too much. If  something is not very compressible, then it is too unfamiliar. If something is too compressible, then it is basically boring. In other words, the pleasure derived first increases and then decreases with the compressibility, not unlike this [binary entropy curve](http://upload.wikimedia.org/wikipedia/commons/thumb/2/22/Binary_entropy_plot.svg/200px-Binary_entropy_plot.svg.png).

Let us ask the same question again for the following pair of images (you *have* to pick one over the other):

[![](/images/in-the-eye-of-the-beholder-img-2.png "Screen shot 2012-11-21 at 8.29.29 AM")](https://thebayesianobserver.wordpress.com/wp-content/uploads/2012/11/screen-shot-2012-11-21-at-8-29-29-am.png)

My guess is that most people will find the image on the right more appealing (it is for me at least). Please drop me a comment with a reason if you differ. When I look at the image on the right, it feels a little more familiar, there are some experiences in my mind that I can relate to the image – for example looking straight up at the sky through a canopy of trees (white = sky, black=tree leaves), or a splatter of semisolid food in the kitchen.

In order for an object to be appealing, the beholder must have some side information, or familiarity with the object beforehand. I learnt this lesson the hard way. About 2 years ago, I gave a talk at a premier research institution in the New York area. Even though I had received complements when I’d given this talk at other venues, to my surprise, this time, audience almost slept through my talk. I learnt later that I had made the following mistake: in the abstract I’d sent to the talk’s organizer, I had failed to signal that my work would likely appeal to an audience of information theorists and signal processing researchers. My audience had ended up being a bunch of systems researchers. The reason they dozed through my talk was that they had just a bit less than the required background to connect the dots I was showing them.

It is the same with cultural side information or context — the familiar portion of the object allows the observer to latch on. The extra portion is the fun. Without the familiar, there is nothing to latch on to. The following phrases suddenly take on a precise quantifiable meaning:

- “Beauty lies in the eyes of the beholder”: the beholder carries a codebook that allows her to compress the object she is observing. Each beholder has a different codebook, and this explains ‘subjective taste’.
- “Ahead of its time”: Something is ahead of its time if it is very good but does not have enough of a familiar portion to it, to be appreciated by the majority of observers.

I can think of lots of examples of art forms that deliberately incorporate partial familiarity into them — e.g. music remixes, Bollywood story lines. Even classical music first establishes a base pattern and then builds on top of it. In [this TED talk](http://www.ted.com/talks/kirby_ferguson_embrace_the_remix.html), [Kirby Ferguson](http://www.kirbyferguson.com/) argues that all successful creative activity is a type of remix, meaning that it builds upon something familiar.

Takeaways:

1. When writing a paper or giving a talk, always make sure the audience has something familiar to latch on to first. Otherwise, even a breakthrough result will appear uninteresting
2. Ditto for telling a story or a joke, DJing music at a party, or building a consumer facing startup. Need something familiar to latch on to.
3. In some situations it may be possible to gauge the codebook of the audience (e.g. having a dinner party conversation with a person you just met), to make sure you seem neither too familiar, nor too obscure.
