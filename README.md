# Final Project - Julia and Adriana

Proposal Question

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

Datasets Used

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
#Trending Into Office
 
s;dkf;sldkfjlskdf;laskjdf;lksdlfj

##Question
asdkjf;laskdjf;lksadjf;lksj

##Index

The combined pytrend and FEC data as well as the graphs and statistical analysis can be found here:
- 2014 Senate Correlation.ipynb
- 2012 Senate Correlation.ipynb
- 2010 Senate Correlation.ipynb
- 2014 House Correlation.ipynb
- 2012 House Correlation.ipynb
- 2010 House Correlation.ipynb

The pytrends code for both the House and Senate can be found in the Pytrends folder, and the code for the FEC data manipulation can be found in the FEC folder. 
____________________________________________
##**Pytrends Code** 
For the pytrends code, we took the names of the candidates from the FEC dataset and formed a kw_list for each state which is required for the build_payload function to run and search the trends and return the results. We initially started by running two names from each state through their own pytrend code, (ie. running pytrends for AK and then AL and then appending the two numbers obtained for each person), but soon found it to be extremely tedious to do so and knew that this would be even worse for the House Code. Hence, we created a for loop that would run through the entire list of candidates in each of the states and create a list which we converted to a dataframe with a column for the index and the percentage of searches obtained. We began using this method after 2014 and 2012 Senate had already been completed, which is why these two have code that looks substantially different. 

A few problems we ran into while running the pytrends code include:
- Inputting the names into the list in the appropriate format as an array with the brackets and the quotes was also quite a task initially when we attempted to do it manually. We then just assigned a string with the names and used the replace function to add the brackets and quotes.
- Some candidates' names were producing errors given that their name was not quite searchable due to an errant middle initial (we removed all middle initials after a point).
- Some candidates share names with other far more famous people, for example: James Woods, Tom Smith, etc. 
- Some candidates went by more common names/ nick names, for example: Hank Johnson for Henry R. Johnson, Buddy Carter for E. L. Carter, etc. 
- A number of times we would get 429 errors for running the code far too many times, we implemented a sleep to remedy this but sometimes even that would not work.

##FEC Code
For the FEC datasets, we filtered out all but the top two candidates for each race to avoid exhausting pytrends searches and our own energy. Initially this meant using a cutoff of around 17% for each Senate race but once we began using the for-loops we had to stop using cutoffs since there were some races that only had one candidate and we needed to add in some placeholder who got 0% of the vote. 
This meant that every candidate who we didn't want included in our analysis had to be deleted from the dataset. 

Another complication arose when certain states such as New York and Massachusetts had multiple parties who endorsed the same candidate and the percentage of the vote earned by that candidate was split among these parties. For example, Chuck Schumer earned 45% of the vote as a Democrat, 6% as a Green, etc. All these percentages then had to be added up in order for our analysis to be accurate.   


_____________________________________________

Data Obtained
The two key pieces of data we obtained through the data manipulation were the Percentage Searched, which was the proportion of total search obtained by that candidate with respect to his/her opponent from the Pytrends data and the Percentage of vote obtained from the FEC dataset.





Other general pytrends problems:
We were not able to obtain city trends data that were usable, as even after setting the 'geo' as US we would just get a list that would just signify the proportion in the state that the two candidates were from given that they were not really being searched much out of their state as expected, thus we stuck to just using the interest_over_time function with the pytrends.
