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

____________________________________________
Index
The jupyter files with the combined pytrend and fec code as well as the graphs made can be found based on year and whether it is for the Senate or House :
2014 Senate Correlation.ipynb
2012 Senate Correlation.ipynb
2010 Senate Correlation.ipynb

2014 House Correlation.ipynb
2012 House Correlation.ipynb
2010 House Correlation.ipynb

The specific code for just pytrends can be found in the Pytrends folder for the House and Senate
The specific code for just the FEC data manipulations can be found in the FEC folder.
____________________________________________

For the pytrends code, we took the names of the candidates from the FEC dataset and formed kw_list which is required for the build_payload function to run and search the trends and return the results. We initially started by running the two names from each state for the Senate years through it's own pytrend code, (ie. running pytrends for AK and then AL and then appending the two numbers obtained for each person), but soon found it to be extremely tedious to do so and knew that this would be even more so for the House Code. Hence, we created a for loop that would run through the entire list of candidates in each of the states and create a list which we converted to a dataframe with a column for the index and the percentage of searches obtained.

A few problems we ran into whilst running the pytrends code include:
Some candidates' names were producing errors given that their name was not quite searchable due to an errant middle initial (we removed all middle initials after a point)
Some candidates share names with other far more famous people, for example. James Woods
Some candidates went by more common names/ nick names, for example. Hank Johnson for Henry R. Johnson
A number of times we would get 429 errors for running the code far too many times, we implemented a sleep to remedy this however, sometimes even that would not work.

Other general pytrends problems:
We were not able to obtain city trends data that were usable, as even after setting the 'geo' as US we would just get a list that would just signify the proportion in the state that the two candidates were from given that they were not really being searched much out of their state as expected, thus we stuck to just using the interest_over_time function with the pytrends.

We limited the candidates per state to the two top-most candidates based on who obtained approximately more than 17% of the vote. Some states had just one primary candidate based on this cut off, for example. Jeff Session in Alabama and so when using pytrends we input a dummy term 'All Others' 
_____________________________________________

Data Obtained
The two key pieces of data we obtained through the data manipulation were the Percentage Searched, which was the proportion of total search obtained by that candidate with respect to his/her opponent from the Pytrends data and the Percentage of vote obtained from the FEC dataset.
