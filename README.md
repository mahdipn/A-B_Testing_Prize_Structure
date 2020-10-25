# Analyzing the Effect of Different Prize Structure on the Participation Rate: A Hypothesis Testing Approach

## Introduction
In a business setting, increasing the response rate of the target population is an essential task. Companies try various methods to encourage the participation of their employees in different fun activities to boost the sense of “unity.” In this study, I explored, using <b>hypothesis testing</b>, the effect of using two different prize structures on the response rate of the participants. The total amount of the prize for both scenarios was the same; however, they have different structures. In other words, for one scenario, called “Before”, the number of winners was two, while for the other one, called “After” the number of winners was six. The number of participants for both Before and After scenarios is comparable, 147 vs. 136, respectively. Throughout this analysis, I tried my best to keep the educational purpose of this Notebook, so there might be many concepts that you already know! With this background in mind, let’s start our analysis.

## Exploratory Data Analysis (EDA)
We are dealing with two small datasets, so the EDA is rather quite simple. I think a simple numerical analysis that shows the average response rate for both scenarios should suffice. Here it is:

 Prize Structure | Participation Rate
 --------------- | ------------------
Structure #1     | 23.1%
Structure #2     | 24.3%

OK, what we see is interesting! It seems that the change in prize structure has little to no effect on the participation rate. Well, intuitively we can say that it has no significant effect and we may not need any fancy analysis. However, in a business setting, you need to prove things with sound analysis. So, let’s keep moving…it helps us practice and have some fun with math and statistics!

## Hypothesis Testing
In hypothesis testing, we need to define a null hypothesis, which is always denoted by “no.” Like, there is no difference between the participation rates from the Before to the After scenario. This is how we define our hypothesis in this study:
- Null hypothesis: There is no difference between the participation rates using different prize structures
- Alternative hypothesis: There is a difference between the participation rates with the employment of different prize structures

### Sample Size and Bootstrap
In hypothesis testing (and A/B testing), the sample size is determined through a rigorous process that takes into account various factors including statistical power and confidence level. However, in this study, we were limited in terms of the number of participants and sample size. So, what is the solution? Remember, we need to think probabilistically! The solution is "resampling." We employed the bootstrap technique, as a popular resampling technique, in this study. In plain language, what this technique does is that it creates many replicates with the same size as your sample datasets by choosing randomly from the sample datasets. So, to implement the bootstrap technique, we need the replication size. We use a large number, like 10,000 in this study, to offset the effect of noise when choosing a small replicate size. For each of the replicates, we calculate the participation rate and store it in an array. At the end of this process, we will be left with two 10,000-member arrays, for the Before and After scenarios. We can create histograms of these replicates to get a better sense of their distribution, as seen below:

<img alt="Participation Rates Distribution" src = "images/normal_dist.png" width = 1500>

### Visual Evaluation of the Hypothesis
The graphs we developed above are cool-looking graphs, and of course, show normal distributions of the participation rates. So, how do we use these graphs? How do we conclude that there is a difference between participation rates from the Before to the After scenario from these graphs? How do we support these graphs numerically? 

To answer these questions, we need to bring up the concept of the 95% confidence interval (CI). In statistics, the 95% confidence interval simply means that there is a 95% probability that the identified interval includes the true mean. OK, good to know! How do we use these for our analysis? We need to bring up another relevant concept. In statistics, if we observe an overlap between the confidence intervals of two metrics (here, participation rate), then the difference between the two study groups is not statistically significant. 

Having these in mind, there are two methods we can use that both employ the abovementioned concepts. We will explore both methods in detail below.

For the first methods, we need to bring the two graphs into one x-y coordinate, show their 95% Cis With these in mind, let’s polish the graphs a little bit and rearrange the figures. We now want to put the two figures on top of each other on the same coordinate and then show their 95% intervals. If their 95% CI overlap, then we know the result. Here is the first method shown graphically:

<img alt="First Visualization Method" src = "images/visual_1.png" width = 750>

OK, they overlap! So no statistically significant difference! 

The next method is an alternate version of the first method. In this method, we will subtract the Before mean replicates from the After mean replicates, then we draw the histogram (normal distribution) and its 95% CI. If the CI includes zero (which means the difference of participation rates between Before and After scenarios is zero) then there is no statistically significant difference between the means. Let’s explore it:

<img alt="Second Visualization Method" src = "images/visual_2.png" width = 750>

The conclusion is the same, as the 95% CI includes zero. We have also shown the mean difference, which is very close to zero!

### Numerical Evaluation of the Hypothesis
We can also prove our conclusions numerically using the p-value. We can calculate the p-value as the number of the data points in the mean difference array taking values at least as large as zero to the total number of observations. In hypothesis testing, if the p-value is greater than 0.90 (you might use a different number, like 0.95, or even 0.99 depending on the problem you want to solve) it means that we cannot reject the null hypothesis and, hence, there is no difference in the participation rates between two scenarios. The calculated p-value is 0.59, and you know the conclusion! 

## Conclusions
In this study, we analyzed the effect of two different prize structures on the participation rate in an activity. The nature of the problem governs the use of hypothesis testing. Given the sample size limitation, we used the bootstrap method, a resampling technique, to increase the sample size. We employed two different visual methods as well as p-value calculation to determine the difference between the participation rates given the type of prize structure. All analyses identified no statistically significant difference between the participation rates, hence the change in prize structure does not affect the participation rate. 
