# A/B testing  

## Definition  
A/B testing is a statistical technique for comparing two versions of something, version A vs version B.  

## How it works  
1. Design your experiment to randomly assign version A to about half of your subjects and version B to the other half.  
2. Pick a level of statistical significance, a.k.a. alpha, for your A/B test experiment, and derive the minimum sample size needed.  
3. Conduct your experiment or collect your data until you have two comparable samples for each version, each of at least the minimum sample size.   
4. Choose a meaningful estimator for your use case and the assumed distribution shape of the underlying distribution.  
   >**Example:** Your estimator may be the mean dollar value of a user's shopping cart, with an approximately normal distribution as the assumed underlying distribution of shopping cart dollar values.  
   >**Example:** Your estimator may be the click-through rate, and the assumed underlying distribution is binomial.  
5. Identify the appropriate two-sample hypothesis test, given your chosen estimator and the assumed distribution.  
   >**Example:** For the first example above, you could use Welch's t-test.  
   >**Example:** For the second example above, you could use Fisher's exact test or Barnard's test.  
6. Run your selected two-sample hypothesis test.  
7. Draw conclusions by comparing the p-value of your test to the level of significance you chose earlier.  

## Assumptions  
- One specific change in a single independent variable accurately represents the difference between versions A and B. There are no confounding variables that could contribute to the differences found in the response variable for the two versions.  
- The estimator you selected reasonably accurately reflects the goal of your experiment.  
- The underlying assumed distribution shape reasonably accurately reflects the true distribution of your estimator.  
- As in all statistical hypothesis testing, you understand and accept that there is a chance that the conclusion indicated by your A/B test is wrong. That chance is equal to the level of statistical significance you've picked. If you set alpha to 5%, that means if you rerun this test 100 times, you should expect that in about 5 of those times, this test will point you to the wrong conclusion.  

## Limitations  
- An A/B test measures one specific difference between only two versions.  
  - To test multiple specific differences across multiple versions, you can use multivariate testing. Multivariate testing works like conducting multiple A/B tests at once.  
- It can be difficult to assess whether the difference in versions is truly and accurately represented by the specific change in the independent variable we are using in our A/B test. This is always a judgment call that is subject to human errors and biases.  
  >**Example:** Suppose we have always had a green button on our webpage, and now we want to try out a blue button to see if more users click it. We design an A/B test where the color of our button is the independent variable we use to represent the difference between the green-button version A of the webpage and the blue-button version B. We conduct our A/B test thinking it will tell us whether users are more likely to engage with one color versus the other. Say, our A/B test results indicate that switching to a blue button is better, and so we go ahead and spend money and time switching to blue buttons on our entire website. Did we make a good decision? Not necessarily.  
  >In creating our A and B versions, we may have unintentionally introduced a confounding variable. In this example, the green button was always there and expected by the users, while the blue button introduced not only a color change but also an element of novelty. The users might have clicked on the blue button more simply because it is new and different and not because they prefer the color. Over time this novelty may wear off, and the users will return to the previous click-through rate, the same as it was with the green button. Furthermore, they might actually slightly dislike the color change, but the novelty of it won over during the experiment. If that's the case, switching our entire website to blue buttons made it less appealing to our users.  
- Deciding what should be A/B tested (and when) is always a judgment call subject to human errors and biases.  
  - A/B testing tests specific changes one at a time, which can be costly and time-consuming. Hence when we have an unmanageably large number of variables we could test, we have to pick and choose which variables we want to test.  
- A/B testing of individual parts of a whole does not guarantee improvement of the whole.  
  - For example, A/B testing is often used to test a small part of a webpage's design. The underlying assumption here is that the whole design is the sum of its parts. This is often not the case. A holistic approach to design matters: blindly following A/B testing for website design improvements can result in a website that is an incohesive mess and an overwhelming user experience.  
- A/B testing is not subjectivity-free or bias-free, or intuition-free, for that matter.  
  - A/B testing is a very popular technique, often branded as evidence-based, scientific, and other big fancy words that make it sound as reliable as hard science. This exaltation of A/B testing is often followed by some sort of shaming of using intuition or guesswork. The thing is, conducting A/B testing involves a lot of intuition and educated guesswork, from deciding what, how and when to test to picking the right estimator and guessing the underlying distribution. Ideally, you want to leverage expert intuition and educated guesses as part of your A/B testing to get the most reliable results.  

## Code examples  
- [A/B testing landing page designs](https://github.com/33eyes/data-science-notes/blob/main/examples/AB_test_landing_page_conversion_rate.ipynb)  
  - conversion rate as response variable  
  - binomial disrtibution
  - Fisher's exact test, two-sample z-test for proportions  

## Why it's important  
- Under the name "A/B testing", this methodology is a popular technique in marketing, web design, app design and similar domains. It is typically used with the goal of optimizing product improvements for user engagement.  
- In a broader sense, "A/B testing" is just another name for a simple randomized controlled experiment with a single treatment group. Randomized controlled experiments are a basic technique in statistics, applied broadly across a wide range of research and evidence-based domains, including healthcare, pharma, agriculture and many more.  

## History  
"A/B testing" is a shorthand name for a specific type of randomized controlled experiment that came into use sometime in the 20th century. Note that it is just the name "A/B testing" and a more formalized version of a randomly controlled experiment that came into use at that time. The principles of a randomized controlled experiment and less formal applications go back hundreds of years. The modern version of A/B testing in marketing started sometime in the 1990s in domains like direct marketing/advertising, predating the web. In 2000, Google first used the technique for web design optimization.

- **1990s:** Modern version of A/B testing comes into use. [(source)](https://hbr.org/2017/06/a-refresher-on-ab-testing)  
- **Feb 27, 2000:** Google engineers ran their first A/B test to find the optimal number of search results to display per page. [(source)](https://www.wired.com/2012/04/ff-abtesting/)  

## Alternatives  
For A/B testing within marketing and digital product optimization domains, qualitative analysis techniques can be used as an alternative to A/B testing.  
Some examples:  
- User interviews  
- User feedback  
- User behavior tracking  
- Session recordings  

For the broader notion of a randomized controlled experiment, the alternative techniques would depend on the exact problem to be solved.  

## Related concepts  
- [Randomized controlled trial](https://github.com/33eyes/data-science-notes/blob/main/notes/randomized_controlled_trial.md)  
- Experimentation  
- Segmentation  
- Multinomial/multivariate testing  

## Further reading  
- [A Refresher on A/B Testing](https://hbr.org/2017/06/a-refresher-on-ab-testing) (Harvard Business Review, 2017)  
- [The A/B Test: Inside the Technology That's Changing the Rules of Business](https://www.wired.com/2012/04/ff-abtesting/) (Wired, 2012)  
- [The Complete Guide to A/B Testing: Expert Tips From Google, HubSpot, and More](https://www.shopify.com/blog/the-complete-guide-to-ab-testing) (Shopify Blog, 2022)  
- [A/B testing](https://en.wikipedia.org/wiki/A/B_testing) (Wikipedia article)  
- [E. Hariton, J. J. Locascio, "Randomised controlled trials—the gold standard for effectiveness research", BJOG (2018).](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC6235704/) (Accessed through NIH National Library of Medicine).  

