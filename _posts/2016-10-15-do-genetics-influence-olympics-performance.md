---
layout: post
title: "Do genetics influence olympic performance?"
date: 2016-10-15
mathjax: true
---

During the recent 2016 summer olympics in Brazil, I found myself grumbling along with some friends about the historically poor performance of India at the Olympics. During the discussion, it was suggested that one of the reasons for India's poor performance at the Olympics might be that Indians are genetically disadvantaged at competitive sport. This was an intriguing hypothesis, but one that was difficult to settle.

A few weeks later, I came across a Priceonomics article about the average heights of people in each country over time. This seemed to provide an opening to test the genetics hypothesis. The Pricenomics article suggested that the mean height of a country was reflective of access to nutrition enjoyed by a country's population during developmental years (and hence reflective of income & resource equality) and contained information that is orthogonal to a country's GDP. I hypothesized that the medal count of a country might have a relationship with it's mean height even after controlling for the country's GDP (it was highly plausible that there is a link between GDP and medal count). If it were so, then it would mean that performance at the Olympics was linked to the portion of the variance in mean height that cannot be explained by GDP, and which must be a consequence of either (1) differences in inequality and/or (2) genetic predisposition. If we could eliminate the dependence of height on inequality, that would ostensibly leave only genetic predisposition. 

This suggested therefore, that if a regression is performed with olympic medal count as the response, and with two predictors: (1) GDP and (2) a version of mean height per country from which economic effects had been residualized, ostensibly leaving behind only genetic factors, then the debate could be settled. If this residualized height variable were to be found statistically significant after controlling for GDP, it would suggest that genetic factors are statistically significant in determining Olympic performance. If we this residualized height were found to not be predictive of medals however, we would only have shown that genetics does not influence Olympic performance via height -- it might still influence performance independently of height. 


Fortunately, I was able to find an Olympic medal count dataset courtesy of The Guardian, a clean dataset on mean height by country broken down by gender and year linked from this study linked from the Priceonomics article, and datasets on GDP and GINI coefficient from the World bank. What follows is an exploration of the relationships between these variables after performing the necessary joins, en route to the hypothesis test crafted above.  The final joined dataset contained data for 156 countries with the following variables: GDP, GDP per capita, GINI coefficient, mean_height for men and women, and counts of medals ever won, by year for each country by medal type (Bronze, Silver, Gold). We take the average of the mean height of men and women to be a single mean height for the country. Further, we compute a single medals score = 3 * # of Golds + 2 * # of Silvers + # of bronzes as a representative scalar of a country's performance at the Olympics. Here is the file with all the data for 156 coutries. We begin with descriptive statistics of the variables in the joined dataset, followed by the simplest univariate relationships.


In each of the regression studies below, we pay special attention to a few countries of interest: USA, China, India and the Netherlands using the colors blue, red, green and cyan respectively. The Netherlands is in the list because it is the country with the largest mean height, while USA and China are in the list because of their Olympic performance and interesting economic variables. 


Univariate regression studies
Medal count and height: The total medal count of a country is indeed related to its mean height. USA appears as a large outlier, suggesting that it's olympic medal count is not driven by its mean height but something else.


Medal count and GDP: shows a strong relationship, much stronger than the relationship between height and medals. This is not too surprising given that richer countries can afford to spend more resources in training their athletes, and that a higher per capita GDP is likely to encourage greater participation in sport. We also tested the GDP per capita against medals and the log10 versions for both GDP and GDP per capita, but found the raw GDP below to have the higher r-quared with medals. USA is no longer an outlier in this regression fit, suggesting that its olympic performance might be driven less by its mean height and more by its GDP. It is worth acknowledging that we cannot make claims about causality from these results. USA is a country of immigrants and it attracts talent in many fields, including sports. This also probably plays a role in its outsized Olympic medal count, even though this is probably related to its high GDP too.


Medal count and GINI coefficient: The hypothesis here is that countries with more equitable distribution of wealth should have a higher medal count because they make resources & nutrition more broadly to their population. We do see a weakly negative relationship but it falls just short of statistical significance of |tstat| > 2.


Height and GDP: Not surprisingly, there is a positive relationship between height and GDP.


However, the relationship is much stronger if we consider GDP per capita instead of raw GDP


The scatterplot above is strongly suggestive that there is a log-like relationship between height and GDP per capita and indeed we see this after transforming GDP per capita to the log domain. The plot below is worth dwelling over. It shows a strikingly good fit between mean height and log 10 of per capita GDP, with an r-squared of 52%! Netherlands does better in mean height and India does worse, than the linear fit from log10 per capita GDP would suggest. 


Height and GINI coefficient: Interestingly, there is a fairly strong negative relationship between height and GINI coefficient, which supports the hypothesis that an equitable distribution leads to a greater mean height. 


Multiple linear regressions
Height vs. log10 of GDP_pcap and GINI: We discovered above that height has a strong positive relationship with log10 of per capita GDP which represents the amount of resources available per unit of population without taking into account the distribution of resources within a country. It is therefore worth examining the effect of adding on GINI as a predictor, which is meant to capture just this, and which we have seen to have a negative relationship with height. We find that adding GINI does indeed improve the r-squared and GINI is found to be a statistically significant predictor. This is evidence that between countries with the same per capita GDP, greater equality leads to a larger mean height. 


Medals vs GDP and height: Does height improve the predictability of medals beyond what is already captured by GDP? We find that this is indeed the case. That is, height contains information relevant to the determining the performance at olympics that is not already captured by a country's GDP. 


Medals vs GDP and GINI: As per our hypothesis, countries with the same GDP should earn more medals if they have a more equitable distribution of wealth because of better access to resources and nutrition. We do find this to be the case. Adding GINI as a predictor to the regression between medals and GDP improves the r-squared and shows GINI to be statistically significant in the presence of GDP.  


Do genetic factors influence Olympic medal counts?
Finally, we arrive at the question we sought to answer: do genetic factors influence olympic medal count? And is genetic disadvantage the primary excuse for India's poor performance at the Olympics? We take a shot at studying this by first removing the effects of GDP per capita (mean resources per person) and GINI coefficient (inequality) from the mean height of a country. This is done by simply regressing mean height against those two predictors and retaining the residual and intercept. 

Mean height=β1∗(log10(GDP per capita))+β2∗(GINI)+residual
The residualized height can be scaled and shifted such that it has the same mean and variance as the original mean height variable. Then the residualized heigh can be thought of as what the mean heights of countries would have been if there were no economic factors at play, only genetic factors (and other factors we may not have thought of). Plotting the residualized height against the original mean height shows that USA, China and Netherlands have a lower residualized height than their mean heights, while India has a higher residualized height than its mean height. In other words, removing economic factors influencing height causes the height of India to increase and the heights of China, USA and Netherlands to decrease. 


Having removed the linear projection onto these two economic variables, we take the residual to be determined largely by genetic factors. This is then used as a predictor against medal count. 


The residualized height shows no statistically significant predictive power against medal count in a univariate regression, where we have not controlled for the effect of GDP on medals. Therefore the univariate relationship between mean height and medals that we saw above disappears if we remove the economic factors that influence height, which says that height influences medals directly only because of the economic factors that influence height. Now, let us control for the effect of GDP on medals and examine the effect of residualized height on medals after GDP has been controlled for. 


Thus, we find that among countries with similar GDP, residualized height does appear to be a statistically significant predictor of medals, indicating that genetics have an impact on Olympic performance if we control for the effect of GDP on medals. 

