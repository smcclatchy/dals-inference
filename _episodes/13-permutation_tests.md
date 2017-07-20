---
title: Permutation tests
teaching: 0
exercises: 0
questions:
- "?"
- "?"
objectives:
- ""
- ""
keypoints:
- "."
- "."
source: Rmd
---








## Permutation Tests

Suppose we have a situation in which none of the standard mathematical statistical approximations apply. We have computed a summary statistic, such as the difference in mean, but do not have a useful approximation, such as that provided by the CLT. In practice, we do not have access to all values in the population so we can't perform a simulation as done above. Permutation tests can be useful in these scenarios. 

We are back to the scenario where we only have 10 measurements for each group.


~~~
dat=read.csv("femaleMiceWeights.csv")

library(dplyr)

control <- filter(dat,Diet=="chow") %>% select(Bodyweight) %>% unlist
treatment <- filter(dat,Diet=="hf") %>% select(Bodyweight) %>% unlist
obsdiff <- mean(treatment)-mean(control)
~~~
{: .r}

In previous sections, we showed parametric approaches that helped determine if the observed difference was significant. Permutation tests take advantage of the fact that if we randomly shuffle the cases and control labels, then the null is true. So we shuffle the cases and control labels and assume that the ensuing distribution approximates the null distribution. Here is how we generate a null distribution by shuffling the data 1,000 times:


~~~
N <- 12
avgdiff <- replicate(1000, {
    all <- sample(c(control,treatment))
    newcontrols <- all[1:N]
    newtreatments <- all[(N+1):(2*N)]
  return(mean(newtreatments) - mean(newcontrols))
})
hist(avgdiff)
abline(v=obsdiff, col="red", lwd=2)
~~~
{: .r}

<img src="../figure/13-permutation_tests-diff_hist-1.png" title="Histogram of difference between averages from permutations. Vertical line shows the observed difference." alt="Histogram of difference between averages from permutations. Vertical line shows the observed difference." style="display: block; margin: auto;" />

How many of the null means are bigger than the observed value? That
proportion would be the p-value for the null. We add a 1 to the
numerator and denominator to account for misestimation of the p-value
(for more details see
[Phipson and Smyth, Permutation P-values should never be zero](http://www.ncbi.nlm.nih.gov/pubmed/21044043)).


~~~
#the proportion of permutations with larger difference
(sum(abs(avgdiff) > abs(obsdiff)) + 1) / (length(avgdiff) + 1)
~~~
{: .r}



~~~
[1] 0.06293706
~~~
{: .output}

Now let's repeat this experiment for a smaller dataset. We create a smaller dataset by sampling:


~~~
N <- 5
control <- sample(control,N)
treatment <- sample(treatment,N)
obsdiff <- mean(treatment)- mean(control)
~~~
{: .r}
and repeat the exercise:



~~~
avgdiff <- replicate(1000, {
    all <- sample(c(control,treatment))
    newcontrols <- all[1:N]
    newtreatments <- all[(N+1):(2*N)]
  return(mean(newtreatments) - mean(newcontrols))
})
hist(avgdiff)
abline(v=obsdiff, col="red", lwd=2)
~~~
{: .r}

<img src="../figure/13-permutation_tests-diff_hist_N50-1.png" title="Histogram of difference between averages from permutations for smaller sample size. Vertical line shows the observed difference." alt="Histogram of difference between averages from permutations for smaller sample size. Vertical line shows the observed difference." style="display: block; margin: auto;" />

Now the observed difference is not significant using this approach. Keep in mind that there is no theoretical guarantee that the null distribution estimated from permutations approximates the actual null distribution. For example, if there is a real difference between the populations, some of the permutations will be unbalanced and will contain some samples that explain this difference. This implies that the null distribution created with permutations will have larger tails than the actual null distribution. This is why permutations result in conservative p-values. For this reason, when we have few samples, we can't do permutations. 

Note also that permutation tests still have assumptions: samples are
assumed to be independent and "exchangeable". If there is hidden
structure in your data, then permutation tests can result in estimated
null distributions that underestimate the size of tails because the
permutations may destroy the existing structure in the original data. 
 
