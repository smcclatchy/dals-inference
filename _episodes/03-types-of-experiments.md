---
title: Types of experiments
teaching: 0
exercises: 0
questions:
- "What are the features of different kinds of experiments?"
- "What are experimental units?"
objectives:
- ""
- ""
keypoints:
- "."
- "."
source: Rmd
---


 
## Types of experiments
 
### Pilot
### Exploratory
 hypothesis generation 

### Confirmatory
 hypothesis testing
 
## Experimental units

## Technical versus Biological Replicates

Technical replicates are measurements taken on the same sample.  Biological replicates are measurements taken on different samples (one per sample).  Technical replicates do not convey biological variation in the data, as the difference between technical replicates in a sample measure “technical” variation, such as, instrument settings, technician skill, and environmental effects.  Biological replicates differ from technical in that differences seen between samples tends to be mostly biological.  If, for example, different technicians worked on measuring the biological samples, it is possible that a technician effect can be accounted for in the model via evaluating a technician batch effect. The key to understanding replicates is to identify the source of the variation that you are attempting to measure. Are you attempting to quantify the accuracy of the measuring tool or procedure from one measurement to the next? If so, then this is a technical replicate. Are you attempting to quantify the difference between one mouse and another? If so, this is a biological replicate.

As an example, if I were to weigh myself on a bathroom scale, record the measurement, then repeatedly weigh myself and record the measurement each time, the measurements might differ from one instance to the next. I could determine the variation of the bathroom scale by averaging all technical replicates and finding the difference of each measurement from this average. Manufacturing of measurement instruments like bathroom scales is never perfect, so there will be technical variation in measurements. In contrast, if I were to measure my own weight and a friend did the same, my weight and my friend's weight are independent of one another. This would be an example of a biological replicate. 

![](../fig/technical-replicates.png)

![](../fig/biological-replicates.png)


> ## Challenge 1
> You are attempting to get different red blood   cell counts from a mouse, and you have enough blood   to measure 3 times through the machine. How many   replicates would this be, and of what type?  
a. 3 biological replicates  
b. 3 technical replicates  
c. 1 biological replicate  
d. 1 technical replicate  
e. b and c
>
> > ## Solution to Challenge 1
> > e. One mouse means that n=1, thus 1 biological replicate. Three runs through the machine means 3 technical replicates. This would be a good way to measure variation in the instrument, but not to infer anything about mice. An n of 1 does not lead to generalizable findings. 
> {: .solution}
{: .challenge}

> ## Challenge 2
> If I want to know about mean blood glucose, should I   
a. measure 1 mouse 9 times
b. 3 mice 3 times each
c. 9 mice 1 time each

>
> > ## Solution to Challenge 2
> > c. 9 mice 1 time each so that you get a sense of the sample mean, the most precise estimate
> {: .solution}
{: .challenge}

