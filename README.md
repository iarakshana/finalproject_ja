# Trending Into Office 

# Proposal

**Question**

We want to explore the relationship between a candidate’s online presence (here represented
by Google Trend data) and the actual percentage of the vote received by each candidate.
Initially we were hoping to use social media data from either Facebook or Reddit but it was a bit
difficult to obtain a coherent usable data set from either so we settled on using the Google
trends data. We are focusing our analysis on Congressional races since the data from
presidential races could potentially be misleading (Trump had a massive online presence but
received less than half of the popular vote). We would like to analyze multiple election cycles to
see if an increased online presence over time has led to an increase in the vote for any given
candidate. While this data may be misleading for incumbents since they have a massive political
advantage regardless of online presence, this analysis could prove informative when it comes to
candidates running multiple times in the same district who have to consider how much
increasing their online presence will realistically increase their odds of being elected.

**Datasets Used**

Google Trends - Google Trends shows how often a particular search-term is entered relative to
the total search-volume across various variables, including region, time and related queries. We
hope to input specific key terms/topics that relate to each candidate in order to find who was
searched more, i.e. more popular by region, in this case ‘by metro’. For example, we would input
the terms Franken, Al Franken, Minnesota Senators, or use the Topic feature that automatically
includes all related queries to the topic “Senator Al Franken” and obtain the trends csv that
includes the data with the variables of time and search frequency as an index of 100. Given the
multiple data files that would be needed, we hope to use the python feature of pytrends that will
help automate the download of data when we list the required key terms, regions and time
period. Using code written by GitHub members, we can directly input key terms and immediately
get a Pandas dataframe with the relative frequency of words over time and over a certain
region. We then hope to compare the frequency of a given candidate with the percentage of the
vote obtained from the FEC datasets.
https://trends.google.com/trends/
https://github.com/GeneralMills/pytrends

Congressional Results - The Federal Election Commission (FEC) has published election
results from every federal election up to 2014 which detail the percentage of the vote received
by each candidate in any given congressional race. We would have to use a different dataset for
each election cycle but the datasets themselves are a bit more manageable.
https://transition.fec.gov/pubrec/electionresults.shtml
__________________________________________
# Project 

## Question
We wanted to test whether or not being searched on Google more than your opponent would translate into a higher percentage of the vote in the next election. We did this by analyzing Google trend data for each candidate in the period from January 1st to Election Day of the year they ran for office. We then calculated the relative amount of internet searches for each candidate compared to their opponent. This trend data was a proxy for the relative amount of online interest in any given candidate in the months leading up to the election. We then compared this with the relative percent of the vote received by each candidate to determine whether or not there was a correlation between the amount of online interest and the percent of the vote received. 

## Index

The combined pytrend and FEC data as well as the graphs and statistical analysis can be found here:
- 2014 Senate Correlation.ipynb
- 2012 Senate Correlation.ipynb
- 2010 Senate Correlation.ipynb
- 2014 House Correlation.ipynb
- 2012 House Correlation.ipynb
- 2010 House Correlation.ipynb

The pytrends code for both the House and Senate can be found in the Pytrends folder, and the code for the FEC data manipulation can be found in the FEC folder. 
____________________________________________
## Pytrends 
The pytrends code gave us the frequency of searches for any given pair of candidates we input in our list on an index of 100, i.e. how much the particular candidate is searched relative to the total search-volume of both candidates over the period of time requested.
In order to obtain the variables we required, we created a for loop to sum these search frequencies and find a proportion of searches in comparison to the opponent candidate in the set, and thus obtained a dataframe with the index of the candidate in one column and the percentage searched in the other column.

For the pytrends code, we took the names of the candidates from the FEC dataset and formed a kw_list for each state which is required for the build_payload function to run and search the trends and return the results. We initially started by running two names from each state through their own pytrend code, (ie. running pytrends for AK and then AL and then appending the two numbers obtained for each person), but soon found it to be extremely tedious to do so and knew that this would be even worse for the House Code. Hence, we created a for loop that would run through the entire list of candidates in each of the states and create a list which we converted to a dataframe with a column for the index and the percentage of searches obtained. We began using this method after 2014 and 2012 Senate had already been completed, which is why these two have code that looks substantially different. 

A few problems we ran into while running the pytrends code include:
- Inputting the names into the list in the appropriate format as an array with the brackets and the quotes was also quite a task initially when we attempted to do it manually. We then just assigned a string with the names and used the replace function to add the brackets and quotes.
- Some candidates' names were producing errors given that their name was not quite searchable due to an errant middle initial (we removed all middle initials after a point).
- Some candidates share names with other far more famous people, for example: James Woods, Tom Smith, etc. 
- Some candidates went by more common names/ nick names, for example: Hank Johnson for Henry R. Johnson, Buddy Carter for E. L. Carter, etc. 

## FEC Code
The FEC dataset was a relatively nice way to get the percent of the vote received by any given candidate. The data was provided in the form of an excel spreadsheet which was easier to use than some of the other voter data we encountered. Unfortunately, we couldn't find data for 2016 on the FEC website so we limited our analysis to the previous three elections. 

For the FEC datasets, we filtered out all but the top two candidates for each race to avoid exhausting pytrends searches and our own energy. Initially this meant using a cutoff of around 17% for each Senate race but once we began using the for-loops we had to stop using cutoffs since there were some races that only had one candidate and we needed to add in some placeholder who got 0% of the vote. 
This meant that every candidate who we didn't want included in our analysis had to be deleted from the dataset. 

Another complication arose when certain states such as New York and Massachusetts had multiple parties who endorsed the same candidate and the percentage of the vote earned by that candidate was split among these parties. For example, Chuck Schumer earned 45% of the vote as a Democrat, 6% as a Green, etc. All these percentages then had to be added up in order for our analysis to be accurate.   
_____________________________________
## General Problems 

As seen in the proposal, we were hoping to analyze the interest over region for each candidate. We were not able to obtain state/city trends data that were usable, since even after setting the 'geo' as US we would just get a list that would signify the proportion of searches that the two candidates were getting in each state. Given that they were not really being searched much outside of their home state(as expected), we stuck to just using the interest_over_time function with the pytrends. This meant that we were technically gathering data from the entire United States but overall the searched were highly concentrated in each candidate's home state so the analysis should still hold. 

Another complication was that a number of times we would get 429 errors for accessing the trends data far too much. We implemented a sleep to remedy this but sometimes even that would not work. Thus, it was quite hard to consolidate the House data sets for the three years owing to the sheer volume of names that we needed for each one.

_____________________________________
## Analysis 

### Senate


All analysis for Senate races can be found in the Correlation notebooks for each respective year. The primary functions used were pytrends, pandas, seaborn, and statsmodels. 

**Comparison By Year**

We started our analysis with the 2014 Senate election. We wanted to see if the correlation between trend percentage and percent of the vote was strongest in the later election or in the earlier elections. We started out by making a multiple bar plot to observe whether or not there was some similarity between the percent of the vote and the percent searched. After verifying that there was in most cases, we plotted the overall correlation between the two variables. We then performed an OLS regression and observed the residuals. All graphs can be found in the Jupyter notebooks for each year. 

After doing this analysis for each year, we found a substantial difference between the strength of the correlation in any given year. We found that in 2014 and 2012, there was a weak but substantially positive correlation between the percent of searches and the percent of the vote received by each candidate. In 2010, however, there was a very weak and less positive correlation observed (Sad!). The p values for all three years were statistically significant, which implies that although the correlation in 2010 was not as strong, there was still some correlation. We hypothesize that this relatively weak correlation is due to the fact that in 2010 there were quite a few candidates who lost yet had a much higher search percentage, either due to them sharing a name with a popular figure or due to them being incumbents. In the 2010 Senate elections the Republicans picked up a few seats by defeating incumbents; even though the incumbents lost the election they were still searched much more than their opponents.  

After plotting the residuals we noticed that they were not at all clustered around 0; there were several candidates with really low residuals and some candidates who had really high residuals. The candidates who shared names with very popular figures likely contributed to the low residuals and candidates whose opponent did not have a topic likeliy contributed to the very high residuals. 

In every year, there were a few cases where the losing candidate shared a name with a popular figure and thus skewed the pytrends data significantly (as mentioned in the pytrends code section). This meant that we got several losing candidates with abnormally high search percentages which undoubtedly contributed to some of the outliers in our data. There were also cases where the losing candidate was popular in their own right as a business owner or philanthropist. These also contributed to the outliers and made our analysis less robust. 

<p align="center">
2010 Senate Correlation
</p>

<p align="center">
  <img width="400" height="300" src="https://github.com/iarakshana/finalproject_ja/blob/master/2010simg.png">
</p>

<p align="center">
2012 Senate Correlation
</p>

<p align="center">
  <img width="400" height="300" src="https://github.com/iarakshana/finalproject_ja/blob/master/2012simg.png">
</p>

<p align="center">
2014 Senate Correlation
</p>

<p align="center">
  <img width="400" height="300" src="https://github.com/iarakshana/finalproject_ja/blob/master/2014simg.png">
</p>


### House 
We started by performing the same analysis on the 2014 House race. Since there were so many more races and so many more chances for candidates not to show up in Google Trends, it was not surprising when our graph wasn't quite as clean. For the 2014 House race there was actually a negative and incredibly weak correlation between percent searched and the percent of the vote received by each candidate. For 2012 there was a slightly positive yet still very weak correlation between the two variables. One possible explanation for the 2014 correlation being slightly negative would be that 2014 was the year when Republicans gained several seats in the House, defeating a decent amount of incumbents. Of course, a more likely reason for such a strange correlation would be that pytrends did not recognize a larger number of names from House races since the losers of these races are more likely to be unknown to the world wide web. 


As there was no strong correlation, we didn't plot the residuals for all years but based on the 2014 plot it is safe to say that we can't conclude much about the relationship between percent searched and percent of the vote earned. There were several candidates who were not searched at all (likely because their name did not warrant a pytrends topic) and many others that were undersearched relative to the percentage of the vote they actually received. It makes sense that this sort of analysis would work better in the Senate than in the House; Senate candidates must appeal to the entire state and thus must rely much more heavily on people searching for them while many House races solely rely on the opposing party not fielding a threatening candidate. 

<p align="center">
2010 House Correlation
</p>

<p align="center">
  <img width="400" height="300" src="https://github.com/iarakshana/finalproject_ja/blob/master/2010himg.png">
</p>

<p align="center">
2012 House Correlation
</p>

<p align="center">
  <img width="400" height="300" src="https://github.com/iarakshana/finalproject_ja/blob/master/2012himg.png">
</p>

<p align="center">
2014 House Correlation
</p>

<p align="center">
  <img width="400" height="300" src="https://github.com/iarakshana/finalproject_ja/blob/master/2014himg.png">
</p>



<p align="center">
  <img width="400" height="300" src="https://github.com/iarakshana/finalproject_ja/blob/master/2014_repeats.png">
</p>



<p align="center">
  <img width="400" height="300" src="https://github.com/iarakshana/finalproject_ja/blob/master/2012_repeats.png">
</p>

____________________________________________________________

## Conclusions
Overall, we can conclude that despite not being extensive, there is some correlation between our two variables in question, however, it is not as positive as we had expected or hoped. This might be either due to the outliers skewing the analysis or the changes in the search terms and frequency over the years analyzed. As a candidate running for office, it is worthwhile to consider how often you are being searched online as candidates who are searched more often generally outperform their opponents. However, this may not be the most effective way of guaranteeing an increased percent of the vote on Election Day. 

__________________________________________________
## Moving Forward 

Moving forward it would be worthwhile to analyze a potential third variable that affects both internet searches and vote received: money. Candidates with more money in general both receive more of the vote and likely are able to get their name out more easily which would result in a higher amount of searches. If this relation is significant, then the correlation between internet searches and vote receieved would only get stronger as the years go on and the amount of money poured into our electoral system increases. Another potential area of analysis would be seeing how incumbents perform against their opponents and/or seeing how male and female candidates differ when it comes to internet searches and percent of the vote received. Performing the same analysis on more years would also prove informative as perhaps the correlation between internet search and percent of vote received is even weaker in 2008 when Citizens United had not yet been passed. 
