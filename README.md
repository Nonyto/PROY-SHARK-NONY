# PROYECT: SHARKS 

Data cleaning and statistics



The goal of this project is to use data wrangling, cleaning, and manipulation with Pandas. For this project, I have to use a messy data set about Shark Attack. The final report will consist of a clean CSV data file and some graphs to understand de data.


## Requeriments

♦ Cleaning columns only if there are more than 80% of Nulls in them.

♦ Minimun number of rows: 6000

♦ Trying to use: duplicates eliminating, regular data type, null eliminating or replacing...


## A quick sum-up

Data cleaning was developed with: duplicates and null values eliminating; null values searching and replacing; atypical and/or wrong reported values replacing and establishing new variables from data in dataframe. Dataframe started initially with 25723 rows and 24 colums and finished with 6302 rows and 23 columns, although the worked columns were finally 12 of them. Parameters that have been studied:

😢 Fatality of sharks: attack type, species, fatal/months relation, fatal/sex

✈ Countries: attaks in countries, sex/age/country relation

👩🏻‍🤝‍🧑🏻 Sex/gendre: affected people sex, fatal/sex, sex/age


## Data cleaning

Dataframe dimensions are initially 25723 rows x 24 columns.

### 1) Duplicates eliminating ❌

I eliminated 19411 rows with no content in them, just empty rows that they do not give any kind of information.

Dataframe dimensions are now 6312 rows x 24 columns.


### 2) Null values eliminating ❌❌

I searched nulls by column as first step and I found that two columns had almost 99% null values so I decided to eliminate both of the (not information at all). The rest of the columns in the dataframe had less than a 80% of null values so I let them intact.

In case of rows, I found ten rows with more than 90% of null values so I decided to drop them out.

Dataframe dimensions are now 6302 rows x 22 columns.


### 3) Null values searching and replacing 🧨


First of all, I changed the column names for better-working. Then I replace NaN values by 'unknown' and 'not declared' in categoric columns. For numeric columns as date, year or age, this step has been studied before taking actions.

Year column contained float values (i.e. 1925.0) so I changed them for integer values (just data type). When I did it, I figured out some years was inconsistent (i.e. 500, 77 or 0). Thinking of consistency, I prefered to establish those values as 'unknown' instead of zeros. 

Age column contained integer and string values (i.e. '13 or 14' or 7 & 30) so I used RegEx to find out the values I was interested of. I took the first number with one or two numbers in it and in every row, avoiding to duplicate rows. I could do this with the function with RegEx and a for loop based on the length of the date, appending the number if the length was 1, and appending a NaN value if length 0 (empty value) or other length not equal to 1. 

To replace the NaN value I studied the age distribution with a boxplot and distribution plot to decide if I should use the mean, mode or median value for age.


IMG BOXPLOT

In the boxplot graphic, I figured out about outliers greater than aprox. 60 years old and a huge group of values between 18-35 (more or less). This fact suggested me that using the mean of age values was not a good idea.

IMG DISPLOT

In the distribution plot graphic, I observed that distribution was left-skewed so median (24 yo) or mode (17 yo) were good options to use for but the quantity of NaN values was nearby 50%. I rejected the idea and replaced NaN values by 'not declared'. The new column about age was included in the Dataframe.


Dataframe dimensions are now 6302 rows x 23 columns.


### 4) Atypical and/or wrong reported values replacing 🥴❓


Some columns contained values wrong reported (typo mistakes, probably). For example, in 'sex' column where only M and F must appear, values as 'N' OR 'lli' appeared. They were replaced by 'not declared' if the date was unintuitive and as 'M' or 'F' if the value was intuitive ('M ' is a 'M' or 'N' is probably a 'M'). This happened in 'fatal' column with values as Y (yes) and N (N).


### 5) Establishing new variables 🆕

I saw a potential new variable from the dataframe: month. From the 'data' column, where a date (YYYY-MM-DD) was given, I decided to take the month and year value. For year value, it alredy exists in dataframe but I considered 'data' column more consistent than the 'year' column.

I proceeded the same as age treatment, with a RegEx function to extract a 4-number value based on the length of the data for the year and a 3-letter word with an '-' before. Then, I just replaced '-AAA' month for the complete month name and take the year from a consistent date.


I would like to work more the 'species' and 'injuries' columns but it was such a mess and I had enough time to deep into. Maybe a recleaning of these variables and 'attack type' would be a better work for me in future.

Finally, I worked with a dataframe with 6302 rows and 12 columns (attack type, country, area, activity, sex, injury, fatal, time, species, age, year and month). 


## Data treatment 📈📊


First of all, I decided to study the values with few variables, such as sex (M/F), attack type (9 values), fatal (Y/N) and months (January to December). I calculated frequencies, obtaining:

♠ 81% attacked people were men and a 10% were women. A 9% attacked people were not-declared-sex.
♣ A 73% attacks were unprovoked while a 9% was provoked. Other ratings were a 4% for sea disaster or 5% for boating.
♦ A 22% attacks were letal for affected people while a 68% were no-letal attacks. A 10% attacks were with unknown ending.
♥ July (10%), August (9%) and September (8%) were the months with more sharks attacks, according to summer time. November (6%), May (6%) and February (6) were the months with less sharks attacks.

Working on countries, the most attacked ones were USA (35%), Australia (21%), South Africa (9%) and Papua New Guinea (2%). Because of low consistency of the country column, it is hard to assure the rightness of the values.

Searching the shark species from the attacks register and comparing with '10 more dangerous sharks' list, I found:

◘ Registered white sharks:  436
◘ Registered tiger sharks:  48
◘ Registered bull sharks:  51
◘ Registered blacktip sharks:  30
◘ Registered Mako sharks:  44
◘ Registered blue sharks:  29
◘ Registered copper sharks:  3
◘ Registered sand sharks:  13
◘ Registered hammer sharks:  0


Focusing on fatal injuries from shark attacks and sex, I studied multivariables where I relationed 'fatal/sex' columns, 'sex/age' columns, 'sex/age/country' columns and 'fatal/month' columns.

○ From 81% of attacked men, a 18% of them were letal while a 55% were a no-letal attack. For women, from a 10% of attacks only a 2% were letal and a 7% were non-letal. The rest were from sex-not-declared person.

○ From 81% of attacked men, a bit less of a half were for 14 to 29 yo men. Those men were mainly from USA and Australia.

○ A fatal-month tendency was not found because of the main value was only 2% from letal in July, predominating non-letal attacks with higher valures of letal-month relation.



## Links & Resources 💻

https://www.kaggle.com/teajay/global-shark-attacks
https://numpy.org/doc/1.18/
https://pandas.pydata.org/
https://docs.python.org/3/library/functions.html
https://plotly.com/python/
https://matplotlib.org/
https://seaborn.pydata.org/
https://pandas.pydata.org/docs/
https://towardsdatascience.com/beware-of-storytelling-with-data-1710fea554b0?gi=537e0c10d89e
