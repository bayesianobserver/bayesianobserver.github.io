---
layout: post
title: "Habit Formation, Part 2"
date: 2012-10-08
original_url: "https://thebayesianobserver.wordpress.com/2012/10/08/habit-formation-part-2/"
categories: ["economics", "learning", "machine-learning", "math"]
tags: ["habits", "human-behavior"]
---
This post builds upon an [earlier post on modeling habit formation](https://thebayesianobserver.wordpress.com/2012/09/27/habit-formation/). To follow this post, please read [this](https://thebayesianobserver.wordpress.com/2012/09/27/habit-formation/) post first. Go on, I’ll wait.

The urn model in that post is not really a complete description of habit formation because the limit distribution of the system (i.e., fraction of white balls after a very large number of draws) is completely determined by the initial configuration of the urn (i.e., number of white and black balls). In reality, habits are formed from repeated actions, and our actions are based on not just our inclinations but also the conscious choices that we make, which can sometimes be against our inclinations. Free will is missing from this model. There is no way to break a bad habit if one start out with one.

Therefore, let us alter the basic urn model slightly to capture choice: At each step, before picking a ball, we explicitly declare which color we are interested in for that pick: a white ball ( = follow the desirable habit) or a black ball ( = follow the undesirable habit). Suppose we choose to aim for a white ball. A ball is then sampled from the urn at random, and if a white ball does indeed come up, then:

1. A payoff of $W is received (We wanted white and we got white, so we are happy to the extent of $W).
2. The white ball is placed back into the urn, along with an extra white ball (Reinforcement).

But if we decide to pick white and a black ball comes up, then there is no payoff, and the black ball is placed back in the urn without any extra ball. However, if we chose black, a black ball is guaranteed to show up, we get a payoff of #B, where # is a different currency from $, and the black ball is placed back along with an extra black. The extra black ball makes picking a white ball harder when a white is desired.

Consider the implications of this model:

1. Suppose there are very few white balls compared to black. A white ball would rarely show up. With the decision to pick a white, most of the time there will be no payoff and no reinforcement. But with the decision to pick a black ball, there is guaranteed payoff of #B units, but at the cost of picking a white later on harder.
2. As the bad habit is reinforced, the chance of reverting to the good habit never dies away completely, but diminishes as the number of black balls grows in comparison to the whites. (‘It’s never too late, but it does get harder’).
3. The purpose of the different currencies is to model the fact that the pleasure obtained from following a bad habit is qualitatively different from the one obtained from following a good one. Since most habits are based on short-term pleasure at the expense of long term benefit (e.g. cigarette smoking, binge eating /drinking, putting off exercise),  currency # may correspond to lots of short term kicks, while $ may correspond to long term well being.

**Short-term thrills**

I believe human behavior is fundamentally driven by a desire to be happy. However, different individuals can have very different ideas about what will make them happy. Since most bad habits result from a focus on short term happiness, at the expense of long term happiness, we would do well to make the following tweak: # and $ can be added to give a total payoff, but each unit of # currency is worth only ![\epsilon < 1](/images/habit-formation-part-2-img-1.php) unit, 1 iteration after it was earned. The other currency, $, however, does not decay with time. The question is what behavior emerges when the objective is simply maximization of total payoff? It is intuitive that the answer will depend upon whether the game has a finite horizon or an infinite horizon. Since players have finite lifetimes, it is appropriate to use a finite time horizon, but since a person does not know when he/she will die, the horizon must be a life expectancy with some uncertainty (variance). In other words, nobody knows when they will die, but everybody knows they will die. The only time it makes logical sense to pick a black ball is if the player believes his remaining lifetime is so small that the expected cumulative gain from deciding to pick whites is smaller than the expected cumulative gain (including the decay effect) from picking blacks. Of course this depends upon how he spent his past — i.e. whether or not he built up a high fraction of whites.

**Breaking a bad habit**

Suppose a person starts out with a predominant inclination towards an undesirable habit and wishes to switch to the good habit. It is clear that if she always chooses the white ball, then she will eventually succeed in creating a larger number of white balls and a good $ balance. But she will have to go many tries and no payoff before that happens. In practice, this requires determination, and she may be tempted to pick the black ball because it is so easily available.

Suppose ![D \in [0,1]](/images/habit-formation-part-2-img-2.php) is the fraction of times that (s)he will decide to aim for a white ball, i.e. the player’s determination. It is intuitive that a larger value  ![D](/images/habit-formation-part-2-img-3.php) would help her switch to the good habit in fewer iterations. It would be interesting to see if there is a threshold value of ![D](/images/habit-formation-part-2-img-3.php) below which the bad habit is never broken. In particular, I expect there to be a threshold value ![D(w,N-w)](/images/habit-formation-part-2-img-5.php), below which the bad hait is never broken, w.p. 1, where ![w](/images/habit-formation-part-2-img-6.php) is the number of whites in the urn and ![N-w](/images/habit-formation-part-2-img-7.php) is the number of blacks.

**Game over when wealth < 1 unit**

Now let us further suppose, that in the course of playing the game, a player can never have less than 1 currency units. In other words, the game stops if the total currency units with a player reaches zero. All other rules are the same: 1 unit earned from a white ball, 1 unit from a black ball but units earned from black balls decay to ![\epsilon](/images/habit-formation-part-2-img-8.php) of their value every time slot. Deciding to pick a black guarantees a black, and an extra black goes in. Deciding to pick a white, provides a white with a probability proportional to the fraction of whites in the urn, and an extra white goes in. With the new rule stipulating ‘game over’ when the player’s wealth falls below 1, the player is incentivized to pick a black if she ever approaches 1 unit of wealth. This is meant to model the inclination of individuals with low self worth and happiness levels to engage in activity that would yield short term happiness (alcohol, drugs, binge eating, etc. ) at the expense of long term prospects.
