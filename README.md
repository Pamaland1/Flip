# District Flip Forecasts in Congressional Elections

This is a classification problem that takes a look at political forecasting.
I have always taken for granted that a district party flip was a result of demographic or 
cultural changes (or gerrymandering) in a specific district, a phenomenon often referred 
to as spatial sorting. I used this project to assess that assumption.

## Objective

I wanted to predict a Congressional District Party Flip, as well as
determine greatest contributing factors to a Party Flip.

## Data Sources

I first looked at the complete history of the U.S. House Returns available from MIT:

* [MIT Election Lab: US House of Representatives Returns](https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/IG0UN2)

I augmented this data with place-based datasets available from the * [The Daily Kos](https://www.dailykos.com/stories/2018/2/21/1742660/-The-ultimate-Daily-Kos-Elections-guide-to-all-of-our-data-sets#16):

* [Congressional district geographic descriptions and largest places - 116th Congress](https://docs.google.com/spreadsheets/d/1ihOWzdGib_P-N3dXiwtP271stvSAcnZLL9JQJpHrGSk/edit#gid=0)
* [2016 bachelor's degrees or greater for ages 25+ & median household income by congressional district for the 115th Congress (2016 1-Year ACS)
](https://docs.google.com/spreadsheets/d/1BIJPzoJpKHXuQZjJSIpaHXN9ZIGM-YsP0jFzfuXTj7c/edit?ts=59e677bd#gid=1591888487)
* [2010-2017 Population Change by Race by CD](https://docs.google.com/spreadsheets/d/1z2mPUyhpkZrUt2jpfZ-N4QmvWnn7_n8B2p7lDHAKd7o/edit#gid=0)
* [House and Senate 5-Year American Community Survey Racial Demographics by Citizenship Status](https://docs.google.com/spreadsheets/d/14gFG9uQgJ-qTq3lkTNQ9YbhB9C8s3Gy78I1eqd7EpRM/edit#gid=1494447813) 
* [Educational attainment by race](https://docs.google.com/spreadsheets/d/1HfUqHKseC8QaVDhmlHMSUEVc-J9eeDzZeYAuHbCierc/edit#gid=0)
* [2016 bachelor's degrees or greater for ages 25+ & median household income by congressional district](https://docs.google.com/spreadsheets/d/1BIJPzoJpKHXuQZjJSIpaHXN9ZIGM-YsP0jFzfuXTj7c/edit?ts=59e677bd#gid=1591888487)

I also obtained District Hex Maps from Daily Kos for visualizations here:
* [Elections maps Explainer](https://docs.google.com/spreadsheets/d/1LrBXlqrtSZwyYOkpEEXFwQggvtR0bHHTxs9kq4kjOjw/edit#gid=1250379179)

After modelling on this data, I had a very low recall score, in the 30th percentile.  
I knew there was a lot more data I could add, but time was running out and I needed 
to make a call on what to add.
I decided to add more specific data regarding campaign financing from the FEC 
(after talking to my politically savvy brother about my poor scores...).  You can find the 
campaign finance files here:

* [2018 House of Representatives Campaign Finance](https://www.fec.gov/data/candidates/house/?election_year=2018&election_full=True)
* [2016 House of Representatives Campaign Finance](https://www.fec.gov/data/candidates/house/?election_year=2016&election_full=True)
* [2014 House of Representatives Campaign Finance](https://www.fec.gov/data/candidates/house/?election_year=2014&election_full=True)
* [2012 House of Representatives Campaign Finance](https://www.fec.gov/data/candidates/house/?election_year=2012&election_full=True)
* [2010 House of Representatives Campaign Finance](https://www.fec.gov/data/candidates/house/?election_year=2010&election_full=True)


## Methodology

As I was just learning classification, I tried a number of models, as well as grid searches 
on my top performing models.  Support Vector Machine was selected after testing Gaussian Naive 
Bayes, K-nearest Neighbors, CART models, and Logistic Regression.  I also ventured into a 
multi-class classification method to make the demographic information more impactful, knowing 
that those who flip republican are likely different in demographics than those who flip democrat.
However, that path did was not fruitful.

## Metrics

I was able to achieve a 76% Recall score.
Recall selected because this metric prioritizes catching as many cases of flipping as possible. 
Precision and F1 score were referenced as well to ensure the model was not indicating too many 
districts that would not actually flip. AUC was also referenced — however due to the class imbalance 
and relative predictability of flipping, there were not major differences between models in this regard.


## Insights

A Decision Tree Model was also implemented to obtain the ranking of the most influential features. 
The results reveal that campaign money drives flipping, and is not all that entwined with demographics 
or geography. The ranking is as follows:  

### Predictive Feature Ranking  

1. $$$ - Financials  

2. History of Flipping  

3. Median Income  

4. 2nd Largest City: percent of population  

5. State  

6. Percent of population in largest metro  

7. Demographic Hyper-parameter - engineered feature  
 

Looking closer into the financial features, their ranking reveals that both individual and 
party committee contributions make an impact.  


### Financial Feature Ranking  

1. Operating Expenditure  

2. Party Committee Contribution  

3. Individual Unitemized Contribution  

4. Total Disbursement  

5. Total Contribution  

## Conclusion
Money is the biggest contributor to determine if a district will flip or not.
Demographics and geography are influential though not as much as pundits will have us think.


You can see the complete project, as well as a tableau map visualization of the predicted vs the actual Party Flips of 2018:
* [District Flip Forecasts in Congressional Elections](https://medium.com/@anupamagarla/district-flip-forecasts-in-congressional-elections-47324c71e7ab?source=friends_link&sk=cc611a6a196f09b0fa1419dcd57bd32f)


## Author

* **Anupama Garla** - [Pamaland1](https://github.com/Pamaland1)

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments

* Thank you to [Daily Kos](https://www.dailykos.com/) for making your nicely cultivated Congressional data and maps available. 
* Thank you to [fivethirtyeight](https://projects.fivethirtyeight.com/2018-midterm-election-forecast/house/) for inspiring me.
* and to my husband, Jesung Park, for supporting me in new endeavors even though its tough
* and [METIS](https://www.thisismetis.com/live-online-data-science-bootcamp) teachers for also supporting, assisting, and teaching me mad data science skills.

