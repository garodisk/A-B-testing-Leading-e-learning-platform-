# A-B-testing-Leading-e-learning-platform-
**Analyzing the different metrics and using the data from a A/B test to analyze whether a new feature should be implemented for a leading -Learning platform. It involves analyzing metrics at various levels of the funnel, checking for the invariants and evaluation metrics, doing a sanity check and then checking for statistical significance using analytical and sign test methods**

# **1. Introduction**

This Project contains a detailed report about an experiment conducted by a **leading e-learning platform** to analyze whether to include a new feature on their course overview page.

The experiment that I am talking about is **A/B testing** where some users are allotted to a control group while some are put in an experiment group and a variety of metrics and statistics designed before an experiment is analyzed to gauge whether the feature should be implemented as per the needs of the company.

**More specifically**, an experimental step would be added after the “Start Free Trial” button on the course page. Based on this experiment, after clicking on the “Start Free Trial” button, a message would be shown asking users the weekly time that they want to invest on the course. If the input hours is below 5 hours per week, “a message would appear indicating that the course usually require a greater time commitment for successful completion, and suggesting that the student might like to access the course materials for free.”

The **goal of the experiment** is reducing the number of students who would quit the course during the starting 14days period, while leaving the number of studnets who pass this 14days period intact. I would like to call the first group of students, “frustrated”, and the second group, “resolute” students.

**Contents:**

**1) Introduction**

**2) Metric Choice**

**3) Measure of variability**

**4) Sizing**

**5) Sanity Check**

**6) Effect Size Tests**


The hypothesis was that this might set clearer expectations for students upfront, thus reducing the number of frustrated students who left the free trial because they didn’t have enough time—without significantly reducing the number of students to continue past the free trial and eventually complete the course. If this hypothesis held true, the company could **improve the overall student experience** and improve coaches’ capacity to support students who are likely to complete the course.

The **unit of diversion is a cookie**, although if the student enrolls in the free trial, they are tracked by user-id from that point forward. The same user-id cannot enroll in the free trial twice. For users that do not enroll, their user-id is not tracked in the experiment, even if they were signed in when they visited the course overview page.


# **2. Metric Choice**


We need two groups of metrics. One group for measuring the effect of change that is imposed, and one group for sanity check, i.e. validation of the test.

The former is called the **Evaluation metric** and the later is called the invariant metric. Evaluation metric are those metrics which we want to use to analyze the change that is it must be sensitive to the changes that we are looking to incorporate.

**Invariant metric** are in general expected to be robust and not change and therefore we expect invariant metric to be same in the experiment and the control group.

***Detailed Analysis of each metric***

**1) Number of Cookies**: That is, number of unique cookies to view the course overview page. (dmin=3000) - Definitely this metric is not affected by the experiment, so this cannot be an evaluation metric. However, it can be an “invariant metric”, since the number of cookies should be more or less the identical in both experiment and control groups.

**2) Number of user-ids**: That is, number of users who enroll in the free trial. (dmin=50) - This can be an evaluation metric, since we expect the number of students who enroll remains the same.

**3) Number of clicks**: That is, number of unique cookies to click the “Start free trial” button (which happens before the free trial screener is trigger). (dmin=240) - This metric cannot be an evaluation measure since at this point of the process, the change is not affected the users yet. It can be an invariant metric.

**4) Click-through-probability**: That is, number of unique cookies to click the “Start free trial” button divided by number of unique cookies to view the course overview page. (dmin=0.01) - It can be an invariant metric.

**5) Gross conversion**: That is, number of user-ids to complete checkout and enroll in the free trial divided by number of unique cookies to click the “Start free trial” button. (dmin= 0.01) - It can be an evaluation metric. The value should be reduced in the experiment group since the number of enrollments is expected to decrease.

**6) Retention**: That is, number of user-ids to remain enrolled past the 14-day boundary (and thus make at least one payment) divided by number of user-ids to complete checkout. (dmin=0.01) - This can be an evaluation metric. Since we expect that the number of enrollment reduces, and the number of payments remains more or less the same, this metric is expected to be more in the experiment group comparing to the control group.

**7) Net conversion**: That is, number of user-ids to remain enrolled past the 14-day boundary (and thus make at least one payment) divided by the number of unique cookies to click the “Start free trial” button. (dmin= 0.0075) - This can be an evaluation metric. The number of clicks is unaffected by the change, the number of payments is expected to remain more or less the same, so the change of this metric is expected to be insignificant.
In order to choose the evaluation metric, we should remember what we wanted to evaluate. First, the number of “frustrated” stduents, and second, the number of “resolute” students.

The number of **user-ids** would be lower in the experiment group, but what does it measure? The possible reduction can be related to both “frustrated” and “resolute” groups. So this metric is not distinctive. The **Gross Conversion** can measure the “frustrated” students. Both the unit of diversion, and the unit of analysis are different in this metric. The **Net Conversion** can measure the “resolute” students. This is a must have metric. The **Retention** can measure the “frustrated” students, hand-in-hand with the net conversion.

So the last three can be chosen as evaluation metircs, and I choose all three now, but the required number of observation may change this set.

# **3. Measure of variability**

The next step will be to calculate the variability of the different metrics. It is the “standard deviation of the sampling distribution” or standard error(SE), rather than the simple standard deviation. The standard error of the current metrics depends on the sample size, and can be computed either **analytically** or **empirically**. Computing it analytically means using an assumption that it follows a statistical distribution (like normal) and using the central limit theorem to calculate it. In general in a real world scenario, it is always useful to calculate it both analytically and empirically ( **using A/A tests**) as empirical calculations are better estimates since they don't have any assumptions though it requires more resources when it comes to time and money. Here, I will use just analytical calculations for our purpose.


I would rather go empirically but it is insisted to use analytical method.

Since the daily unique cookies of the overview page is 5000, we need to figure out sample size for each metric. The sample size is equal to the denominator quantity, assuming 5000 unique cookies for the overview page.

# **4. Sizing**


This is the more interesting part of the report. In any experiment design, determination of the sample size is a fundamental step. Based on the distribution of the metric, the sample size is a function of some parameters such as alpha, i.e. significance level, beta, false negative probability or type II error, baseline conversion, practical significance and so.

We will use this sample-size calculator (http://www.evanmiller.org/ab-testing/sample-size.html), to calculate the sample size.




There are two points to note here. First, I did not adjust significant level based on the fact that we have multiple metrics. Bonferroni is one approach to such adjustment, and there are more approaches to do so. I did not adjust, because these metrics are closely related to each other, and Bonferroni would be too conservative, cause inflamation of the sample sizes. Even now these sample sizes are very high, as we will see, when we consider the unique cookie number of overview page visitors. It is possible to reduce the alpha in order to reduce the false positive probability of the whole test anyway.


**Summary:**

**Metric 1**  Gross Conversion

Baseline Conversion: 20.625%

Minimum Detectable Effect: 1%

alpha: 5%

beta: 20%

1 - beta: 80%

sample size = 25,835 enrollments/group

Number of groups = 2 (experiment and control)

total sample size = 51,670 enrollments

clicks/pageview: 3200/40000 = .08 clicks/pageview

pageviews = 645,875

**Metric 2** Retention

Baseline Conversion: 53%

Minimum Detectable Effect: 1%

alpha: 5%

beta: 20%

1 - beta: 80%

sample size = 39,155 enrollments/group

Number of groups = 2 (experiment and control)

total sample size = 78,230 enrollments

enrollments/pageview: 660/40000 = .0165 enrollments/pageview

pageviews = 78,230/.0165 = 4,741,212

**Metric 3** Net Conversion

Baseline Conversion: 10.9313%

Minimum Detectable Effect: .75%

alpha: 5%

beta: 20%

1 - beta: 80%

sample size = 27,413 enrollments/group

Number of groups = 2 (experiment and control)

total sample size = 54,826

clicks/pageview: 3200/40000 = .08 clicks/pageview

pageviews = 685,325


In all the 3 cases, the **pageviews** required is huge.

# **5. Sanity Check**

Next, we will do the sanity check for all the metrics

The first step in validation of the experiment is assessment of invariant metrics. There are some metrics that are expected to have more or less identical values in the both experiment and control groups.

From the metrics that we have, I have chosen the number of cookies, number of clicks, and click-through probability as invariant metrics. Now using this data, I check whether the values of these metrics are significantly different in the experiment and control groups.

For the counts metrics, we assumed that 50% of the experiment traffic goes to the experiment group and 50% goes to the control group. If we call these two groups success and failure, then the model can be a Bernoulli distribution. So I would check whether the current counts of these two groups can come from a population with 0.5 change of success or failure. And I do it using bootstrapping to estimate and build confidence interval.

Null Hypothesis: Status quo. Any difference between the metric value of the two groups is due to chance. Alternate Hypothesis: The difference between the metric value of the two groups is meaningful, and significant. It cannot be due to random change.

It is said in the course that we should calculate the fraction of the control group on the total. It can be the difference of the numbers of the two groups, or relative size of each group to another one. There are different ways anyway.


# **6. Effect Size tests**

After all the sanity checks were passed, and the experiment data is validated to some extent, we can go forward and analyze the **evaluation metrics**.

What we want to do is **assessing whether the differences between evaluation metric values of the control and experiment groups are significant or not**. Previously, we had chosen gross conversion and net conversion as the two evaluation metrics.

**1) We expect the gross conversion to be lower in the experiment group since the number of enrollments should be lowered**

**2) We expect not to see any significant difference between the values of net conversion rate of the experiment and control groups.**

The **confidence interval does not contain 0** that means the difference in the gross conversion is **statistically different** and **similar** to what we were expecting.

The **confidence interval contain 0** that means the difference in the net conversion is **not statistically different** and **similar** to what we were expecting. We expected the net conversion rate to be almost similar.


Out of 23 days, on 19 days, control has more Gross Conversion rate than the experiment group which is **consistent** with our previous results.

Also, for net  conversion rate case, control group has higher value for 13 days and for the other 10 daays, the experiment group has a higher value which makes sense since there shouldn't be any expected difference.

**Therefore, as per the resullts, the online elearning platform should launch the new feature.**



