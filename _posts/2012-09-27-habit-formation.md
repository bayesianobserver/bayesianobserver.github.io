---
layout: post
title: "Habit Formation"
date: 2012-09-27
original_url: "https://thebayesianobserver.wordpress.com/2012/09/27/habit-formation/"
categories: ["machine-learning"]
---
An urn contain balls of two colors, white and black. A ball is drawn at random, and then put back in the urn along with a new ball of the same color. This process is repeated  many times. What is the ratio of white balls to black balls in the urn after ![n](/images/habit-formation-img-1.php) tries? What is the ratio as ![n \rightarrow \infty](/images/habit-formation-img-2.php)? The answer depends upon the initial number of white and black balls of course.

This is the Polya Urn problem, and I find it to be an interesting way to think about the process of habit building. Imagine that the two types of balls represent two opposing choices that we can make about a certain aspect or activity in our lives, e.g. waking up early or not waking up early, doing regular exercise or not, smoking a cigarette after dinner, or not, completing homework on time every evening vs. playing video games during that time, etc.

```

# Polya urn simulation in Python
import random, pylab as plt

nruns = niter = 200
whitenum = blacknum = 1
for i in range(0,nruns):
  frac = []
  nwhite = whitenum
  nblack = blacknum
  for j in range(0,niter):
    if random.random() < nwhite/float(nwhite+nblack):
       nwhite = nwhite + 1
    else:
       nblack = nblack + 1
    frac.append(nwhite/float(nwhite+nblack))
  plt.plot(frac)
```

Let us say that picking a white ball corresponds to the desirable activity in these examples, and picking a black ball corresponds to the undesirable one. The fraction of white balls in the urn at any given time represents our proclivity to pick the desirable activity at that time.

This model has some interesting properties. First, if the number of balls of each type to begin with are equal, then the fraction of white balls at any step, and in particular at ![n \rightarrow \infty](/images/habit-formation-img-2.php) is a random variable that behaves as follows:

[![](/images/habit-formation-img-4.png "polya1")](https://thebayesianobserver.wordpress.com/wp-content/uploads/2012/09/polya1.png)Above: Fraction of whites, starting with 1 black and 1 white ball

[![](/images/habit-formation-img-5.png "beta-unif")](https://thebayesianobserver.wordpress.com/wp-content/uploads/2012/09/beta-unif.png)

Above: Histogram of the fraction of white balls after 20k iterations

Note that extreme outcomes are possible as ![n \rightarrow \infty](/images/habit-formation-img-2.php) if appropriate choices are enforced early on. Also the final value is attained after only a few iterations. Early iterations provide the opportunity for large swings in the final outcome, but there are hardly any swings after crossing about 50 iterations. Similarly, the that longer a habit has had to cement itself, that harder it is to change it.

But the model above converges to an almost uniform distribution on the fraction of white balls after a large number of tries. Perhaps starting with 1 white and 1 black isn’t quite right, because we are do not necessarily begin life with equal tendencies for picking each side of a binary choice. If we set the number of white balls to be greater than the number of black balls at the start, then the distribution of the fraction of white balls after many tries is, as expected, skewed in favor of white balls. Again, the fraction of white balls usually settles down to a fairly stable value that is typically  determined largely by the actions in the first few iterations.

[![](/images/habit-formation-img-7.png "polya5")](https://thebayesianobserver.wordpress.com/wp-content/uploads/2012/09/polya5.png)

Above: Fraction of whites, starting with 1 black and 15 white balls

[![](/images/habit-formation-img-8.png "beta1-5")](https://thebayesianobserver.wordpress.com/wp-content/uploads/2012/09/beta1-5.png)

Distribution of fraction of whites after 20k iterations starting with 5 whites, 1 black

If the initial number of balls is allowed to be fractional, then the limit distribution has most of its mass near 0 and 1. The plot below shows 500 iterations starting with 0.2 white and 0.2 black balls. Perhaps this better models habit formation in some people.

[![](/images/habit-formation-img-9.png "polyapoint5")](https://thebayesianobserver.wordpress.com/wp-content/uploads/2012/09/polyapoint5.png)

Fraction of white balls, starting with 0.2 whites and 0.2 blacks.

[![](/images/habit-formation-img-10.png "beta0.2")](https://thebayesianobserver.wordpress.com/wp-content/uploads/2012/09/beta0-2.png)

Distribution of fraction of whites, after 20k iterations, starting with 0.2 whites & blacks.

Habit building is not the only thing this model can describe. There are a number of phenomena in which reinforcement plays a role:

1. Popularity of a brand: Among competing brands of similar quality, one that is slightly more popular may get picked more by customers, making it even more popular (“So many people choose this brand, so it must be good”). I’m sure marketing majors know this well.
2. Rich get richer: It is easier to make $X when you have $100, compared to if you have only $10 to begin with.
3. Short term market fluctuation in the price of a security on the stock exchange can sometimes have this property. A large number of buy orders will signal to the market a positive outlook on the security, resulting in even more buy orders. Ditto for sell orders. Until the market stabilizes. Similar to (1) above.
4. Markets with network effects have a rather obvious reinforcement property: for e.g., the greater the number of users that facebook has, the greater the number of new users it is likely to attract, compared to, say, a competing network like Google+, because the marginal utility for a new user is greater when she join the larger network.
5. [Tragedy of the commons](http://www.cs.wright.edu/~swang/cs409/Hardin.pdf "1968 Essay, by Garett Hardin") [PDF]: Defined by Wikipedia as: ‘The depletion of a shared resource by individuals, acting independently and rationally according to each one’s self-interest, despite their understanding that depleting the common resource is contrary to their long-term best interests’. Example: A grassy hill is shared by several farmer to graze their cows. If one farmer overgrazes, others have an incentive to quickly overgraze too, and eventually the utility of the hill is destroyed for all farmers.
6. Hiring in a new company/group: If the organization has a good number of great/well-known people, it is easier to attract other good employees. Similar to (1).
7. Thinking: Sometimes people make a choice about thinking about something in a certain way (e.g. so-and-so is a mean person), and this colors their interpretation of future observations, in effect reinforcing their prior notion.

**Notes:**

1. In the form above, the urn model displays positive feedback. How can we change the urn model to display negative instead of positive feedback? Simple: put in an extra black ball if a white ball is picked and vice versa. This forces the fraction of white and black balls to remain close to 1/2.

2. Learning by rewards: There has been work in the psychology community that studies reinforcement learning in humans and animals, that is, given a set of choices and associated rewards, how does an animal learn which choice to pick? The *Law of Effect* is the hypothesis that the probability of picking a choice is proportional to the total reward accumulated from picking that choice in the past. Given a reward scheme, this translates to an Urn model with the colors representing rewards from the various possible actions. For a nice survey of reinforcement models, see: Robin Permantle, A survey of random processes with reinforcement, Probability Surveys, Vol. 4 (2007) .

3. The model above is the simplest urn model. There are several variations of this model, that have proved useful in modeling and learning tasks, other than reinforcement. E.g. using more than 2 colors, or using multiple urns, or allowing for the introduction of new colors. There are a number of interesting distributions for which these Pola Urn variations act as generating processes (Dirichlet-multinomial, Dirichlet Process, Chinese Restaurant Process), but that’s another post.
