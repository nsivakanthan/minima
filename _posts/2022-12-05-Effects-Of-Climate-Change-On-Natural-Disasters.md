By: Nitharsan Sivakanthan, Prateek Kakkar, Ramgopal Reddy Putta

### Abstract: 

Climate change has created a series of adverse effects on our planet. Is it causing an effect on the frequency and severity of natural disasters across the globe? If so, can governments save human lives and money by reducing climate change causes?

Our carbon footprint harms the environment we live in as it is one of the main causes of human-induced climate change. As of October 11, 2022, there have been 15 weather/climate disaster events with losses exceeding $1 billion each to affect the United States (Billion-Dollar Weather and Climate Disasters, 2022). This study investigates the impact of CO2 emissions on the frequency and severity of natural disasters and questions whether it is possible for the US to save taxpayer dollars in mitigating the effects of these catastrophes. We find similar trends between global CO2 emissions, the count of natural disasters in the US, people affected by natural disasters in the US, and money spent on natural disaster relief by the US. Together, these trends indicate the possibility to improve US citizens’ lives and save the US government billions of dollars by working together with countries worldwide to reduce the CO2 emissions.

 
### Introduction: 

The COVID-19 pandemic has managed to draw researchers’ attention to the impacts of natural disasters. According to the report by the Center for Research on the Epidemiology of Disasters, in 2021, a total of 432 catastrophic events were recorded, which is considerably higher than the average of 357 annual catastrophic events for 2001-2020 and these accounted for 10,492 deaths, affected 101.8 million people and caused approximately 252.1 billion US$ of economic losses (CRED, 2022). Natural disasters result in a diverse series of consequences. The ever-increasing, Carbon dioxide emissions, a key greenhouse gas that drives global climate change, heat our planet, and ultimately leads to extreme weather events like droughts, heatwaves, cyclones, etc. One example of this is the devastating Australian bushfires in 2019 and 2020. The authorities confirmed the causes were arson and lightning, but climate change influenced its intensity significantly because 2019 was the driest and hottest year in Australian history (PAPER, 2020). Accordingly, mitigating the impact of natural disasters and controlling CO2 emissions have become a pressing issue in the international community. This study consists of visuals to show the trends of CO2 emissions and people affected by natural disasters across the globe. The costs incurred by the US government due to the natural disasters is another focus. 

 
### Methodology: 

#### Data Collection -  
We sourced multiple datasets from Kaggle and Our World in Data. These datasets complement each other well and provide enough information to explore the questions we sought out to answer. The first dataset from Kaggle contains the CO2 emissions in metric tons per capita of every country from 1960-2018. The second dataset from Kaggle contains information regarding every disaster occurring in the United States between 1980 and 2022 that cost the US more than 1 billion dollars. Additionally, this data set includes information on the deaths per disaster and classifies each disaster into a disaster type. The third dataset from Our World in Data provides information about natural disasters for every country in the world from 1900 to 2022. Our analysis uses the values of deaths, people affected, and people affected per million for each country from this dataset. ‘People affected’ is defined as people who require immediate assistance during a disaster. The fourth dataset is extracted from the Geodata package, which provides geographic polygons for all the world's countries. This data is used to visualize the world, to highlight countries contributing to CO2 emissions and the most affected countries.

 
#### Data cleaning and tools used- 
Once the data is loaded into the coding notebook, the data from various data files are converted into data frame formats and comprehensive data preparation is initiated. The column names were renamed to have consistent field names, removed all the null values for considered columns, filtered out the required data, converted required data frames from wide to long formats, changed the data types, and dropped unwanted columns. Aggregation operations are performed over required columns to calculate the mean and median values. Considering the huge size of the data files, we narrowed our focus to specifically required columns for the disaster data set. For the disaster data set, we only used the columns which provided information about the number of deaths and those affected by each disaster. 
After the data preparation is performed, a statistical visualization python library, ‘Altair’ is implemented to visualize the required plots. A series of world maps, bar plots, and line graphs are created to communicate the trends and data findings. We also used our knowledge of Tableau, a visual analytics platform, to create some of the visualizations which seem to be complicated using python libraries. The same data files were used as a source in this software to produce the charts in separate sheets and finally layered them together on a dashboard to extract as a static visual image. 
 
### Results: 

#### CO2 Emissions: The Global Trend - 
To investigate whether CO2 emissions impact the frequency or severity of natural disasters, we will first look at global trends in CO2 emissions. Fig 1 shows CO2 emissions in metric tons per capita in 2021 for the top 15 countries. It is important to note the US is among the top CO2 emitters. 

![Top 15 CO2 Emitters](https://raw.githubusercontent.com/nsivakanthan/co2emissions-and-disasters/main/Vis-project-images/img1.png 'Top 15 CO2 Emitters')

Fig 1: Top 15 Countries in CO2 Emissions in 2021 

To get a better sense of yearly CO2 emissions, we show CO2 emissions in metric tons per capita for a select few countries for each year from 1960 to 2020. Countries were chosen to show a range of CO2 emitters. In addition, we selected countries that are interesting to compare to the US such as China and India. Most importantly, we include a dotted line representing the global median emissions each year. This upward trending dotted line indicates that over time, CO2 emissions have been increasing worldwide. What we would like to do next is compare this trend to the occurrence of natural disasters in the US. 
 
![Yearly CO2 Emissions for Countries](https://raw.githubusercontent.com/nsivakanthan/co2emissions-and-disasters/main/Vis-project-images/img2.png 'Yearly CO2 Emissions for Countries') 

Fig 2: Yearly CO2 Emissions for Countries 
 
#### The Human Cost: Frequency and Severity of Natural Disasters - 
Fig 3 shows us an upward trend in the count of disasters over time in the US. It is important to note, Fig 3 shows us the counts of disasters from 1980 to 2022, while we can see from Fig 2 the upward trend in CO2 emissions starts decades before this. Regardless, both trends are consistent even when focused on matching time periods. From this, there seems to be a strong relationship between global CO2 emissions and the frequency of natural disasters in the US. The largest attributor to the count of natural disasters over time in the US are severe storms. We can compare the counts of natural disasters to the counts of other types of natural disasters as well. 
 
![Count of Disasters](https://raw.githubusercontent.com/nsivakanthan/co2emissions-and-disasters/main/Vis-project-images/fig3.png 'Count of Disasters')

Fig 3: Count of Disasters in the US per Year

[Link to Interactive Plot](https://nsivakanthan.github.io/co2emissions-and-disasters/Vis-project-images/fig3.html)

Before we look deeper at the severity of natural disasters in the US, we want to look at the global landscape. We chose to show the average of the past two decades to gather a more recent picture of global values. Fig 4 shows the total number of people affected per million in each country from 1998 to 2018.  It is observed that the USA is one of the most affected countries in the world, since the color of USA is towards the ‘red’ color shade of the color scheme.   
 
![Global Map for Affected per Million](https://raw.githubusercontent.com/nsivakanthan/co2emissions-and-disasters/main/Vis-project-images/fig4.png 'Global Map for Affected per Million') 

Fig 4: Global Map for Affected per Million

[Link to Interactive Plot](https://nsivakanthan.github.io/co2emissions-and-disasters/Vis-project-images/fig4.html)
 
Now, we will shift from looking at the frequency of natural disasters to their severity over time. Fig 5 shows the top 5 countries with the most people affected by natural disasters in the most recent two decades. While the number for countries like China and India are five to ten times more than the US, the people affected in the US is still among the top 5 in the world. 
 
![Top 5 Most Affected Countries](https://raw.githubusercontent.com/nsivakanthan/co2emissions-and-disasters/main/Vis-project-images/img5.png 'Top 5 Most Affected Countries') 

Fig 5: Top 5 Most Affected Countries 
 
Next, we will look at how the severity of natural disasters has changed over time. We compare global trends to the trends in the US. Fig 6 shows yearly totals of people affected by natural disasters globally and for the US. Both show us increasing trends in people affected over time.  
 
![Number of People Affected Globally and in the US](https://raw.githubusercontent.com/nsivakanthan/co2emissions-and-disasters/main/Vis-project-images/img6.png 'Number of People Affected Globally and in the US')

Fig 6: Number of People Affected Globally and in the US
 
Fig 7 shows yearly totals of deaths by natural disasters globally and for the US. There does not appear to be any trend, however there are periods of time where natural disasters are more deadly. This likely has to do with factors such as population density of locations of the natural disasters and the degree of severity of the natural disaster.   
 
![Number of Deaths Globally and in the US ](https://raw.githubusercontent.com/nsivakanthan/co2emissions-and-disasters/main/Vis-project-images/img7.png 'Number of Deaths Globally and in the US ')  

Fig 7: Number of Deaths Globally and in the US 
 
In Fig 8, we can compare which types of disasters affect the most people and cause the most deaths globally and in the US. In the US, storms are the major cause of people affected and death totals. This is corroborated by the trends we found in Fig 3 with the increasing counts of disasters in the US over time being attributed mostly due to the increasing counts in severe storms. 

![Percentage Deaths/Affected](https://raw.githubusercontent.com/nsivakanthan/co2emissions-and-disasters/main/Vis-project-images/fig8.png 'Percentage Deaths/Affected')

Fig 8: Percentage of Deaths/Affected by Disaster Type Globally and in the US

[Link to Interactive Plot](https://nsivakanthan.github.io/co2emissions-and-disasters/Vis-project-images/fig8.html)
 
Overall, we see the frequency and severity of natural disasters increasing over time in the US. We believe this trend is related to the upward trend of global CO2 emissions found before. Therefore, there is potential to save lives and improve outcomes for hundreds of thousands of people in the US and millions of people around the world if the world can reverse the trend of global CO2 emissions.  
 
#### The Monetary Cost: How much is the US spending? - 
Now, we switch our focus to how much the US is spending due to natural disasters and whether this has any relation to CO2 emissions. During this analysis, it is important to note we are only considering disasters that cost the US over a billion dollars, CPI adjusted. We had this limitation due to the data collected. However, this likely will not affect the outcomes of the analysis due to the magnitude of the costs of disasters. 
 
As we noted before a disparity between types of natural disasters in the US, we will first look at the trends of dollars spent per disaster type from 1980 to 2022. In fig 9, we can see the trends of the cost of each disaster type during this time period. Although severe storms account for the highest count of disasters in the US, the type of disaster that can be the costliest are tropical cyclones. Costs of disasters highly depend on the individual disasters and their degree of severity.  

![Trend lines for Cost (in millions of dollars) per disaster type](https://raw.githubusercontent.com/nsivakanthan/co2emissions-and-disasters/main/Vis-project-images/img9.png 'Trend lines for Cost (in millions of dollars) per disaster type')

Fig 9: Trend lines for Cost (in millions of dollars) per disaster type 
 
We would like to compare the trend lines of median global CO2 emissions and cost of disasters in the US. Fig 10 shows us that both are increasing trends. There are significant fluctuations in the cost of disasters depending on the year. This is due to the individual severities of disasters occurring during those years. Despite this, the overall trend of the cost of disasters in the US is increasing.  

![Yearly Global CO2 emissions and Yearly Cost of Disasters for the US](https://raw.githubusercontent.com/nsivakanthan/co2emissions-and-disasters/main/Vis-project-images/img10.png 'Yearly Global CO2 emissions and Yearly Cost of Disasters for the US') 

Fig 10: Yearly Global CO2 emissions and Yearly Cost of Disasters for the US 
 
Fig 11 explicitly shows the trend of cost of natural disasters in the US per unit of CO2 emissions globally. This trend line shows that over time the cost of CO2 emissions regarding damage from natural disasters has increased. We do have fluctuations in the cost per unit of CO2 emissions, but overall, the increasing trend is worrying. 

![Yearly Cost per CO2 emissions](https://raw.githubusercontent.com/nsivakanthan/co2emissions-and-disasters/main/Vis-project-images/img11.png 'Yearly Cost per CO2 emissions')

Fig 11: Yearly Cost per CO2 emissions for the US 
 
This analysis shows the potential to decrease the financial cost of natural disasters in the US by decreasing global CO2 emissions. As such, it is in the United States’ best interest to work together with countries across the planet to reduce CO2 emissions. 

 
### Conclusion:

Climate change has many effects on our planet. This research focuses on climate change’s effect on the human and monetary costs of natural disasters. Studies have shown that human-induced climate change is in large part due to CO2 emissions across the globe. Our analysis starts by showing the increasing global trend in CO2 emissions. An increasing trend can also be seen for the counts of natural disasters, the number of people affected by natural disasters, and the cost of natural disasters across the United States. As such, it is possible that climate change causes these increasing trends of human and financial costs to the US. If countries around the world worked together to decrease human-induced climate change, our analysis shows it is possible to save and improve people’s lives and save the US government billions of dollars.  
In the future, we will need more information to establish a causal relationship between climate change and these increasing trends. There are three areas to focus efforts on. Further analysis of how people are affected by disasters is necessary. More detail is needed on how US dollars have been used for disaster events over time. Finally, consideration is needed of how data collection might have changed over time due to improved technologies on detecting natural disasters, obtaining numbers of people affected from disasters, and dollar values of relief efforts.  

 
### Appendix:

#### Design of Visualizations - 
All the bar plots use the same color (‘e57a44’) to maintain consistency of color scheme throughout the visualizations. 

Fig 1: Top 15 Countries in CO2 Emissions in 2021 -  
A table heatmap is created in Tableau to visualize the CO2 emissions (Metric Tons per Capita) for the top 15 countries. A sequential multi-Hue orange-gold color scheme was used to emphasize the high CO2 emitting countries. The dark-to-light intensity of the color shows the amount of CO2 emitted by these countries in 2021. 
 
Fig 2: Yearly CO2 Emissions for Countries - 
This a line plot showing how CO2 emissions (metric tons per capita) change over time for a select few countries. In addition, a dotted line for the global median is added so that we can establish a global trend of CO2 emissions. The countries are selected to show a range of values above and below the global median. Since certain countries have very low and very high emissions per capita, we re-scale the y-axis so the trend lines for all countries are visible. The scale type 'square root (sqrt)' is used so that the distances in the pixel range will correspond to the square root of the distances in the data domain. To prevent overcrowding of the x-axis, we show ticks every five years. Colors are chosen to distinguish countries and shown in the legend. 

Fig 3: Count of Disasters in the US -  
This is a bar plot showing the counts of disasters each year from 1980 to 2022 in the US. Opacity is used to distinguish between counts of natural disasters and counts of severe storms, which is one of the types of disasters. Severe storms are shown because they are the major contributor of natural disasters in the US. This plot is used to show the increasing trend of the number of natural disasters in the US. 
 
Fig 4: Global Map for affected per million - 
A Choropleth map is plotted to communicate about the most affected countries due to Global CO2 emissions with respect to the number of people affected per million population using the color scheme 'yelloworangered'. The countries that are most affected are highlighted in red color and the intensity of the color of the countries decreases with a decrease in the value of number of people affected.  
 
Fig 5: Bar plot top 5 most affected countries - 
The top five countries with the greatest number of people affected are represented in Bar graph with the Y axis rescaled to ‘square root’ type. USA Stands among top 5 countries. 
 
Fig 6: Number of People Affected Globally and in the US - 
This is a bar plot that shows the number of people affected (in Millions) by catastrophes around the world and the USA per decade. The opacity was adjusted to make grid lines visible behind the filled bars. The Y-axis was scaled to show the count per million. 
 
Fig 7: Number of Deaths Globally and in the US - 
This is a bar plot that shows the number of people who lost their life in catastrophes around the world and the USA per decade. The opacity was adjusted to make grid lines visible behind the filled bars. The Y-axis shows the actual number of deaths in the world against the USA. 
 
Fig 8A and 8B: Percentage of People Affected/Deaths by Disaster Type Globally and in the US  
This is a bar plot that shows the percentage of total deaths/affected people around the world and the US for each disaster. The percentages are calculated independently for each pane (World and USA). This actual visualization comes with an interactive feature to select the impact on People (Deaths or Affected). The opacity is adjusted to show the grid lines behind the filled bars. 
 
Fig 9: Trend line for Cost (in millions of dollars) per disaster type  
This tabular visualization is built in tableau to show the trend in the amount of cost spent by the US government to mitigate the effects of these natural disasters. This table is selectively designed to show important information to the audience. The first column shows the disaster name, and the second and fourth columns show the minimum and maximum cost spent on each disaster in millions of dollars. The third column, a line chart, shows the trend cost from 1980 to 2018 with the y-axis scaled independently for each disaster. 
 
Fig 10: Yearly Global CO2 emissions and Yearly Cost of Disasters for the US - 
Two distinct line graphs are combined in a single dual Y-axis plot with respect to the ‘Years’. Both the graphs are distinguished by different colors. Each Y-axis label is highlighted with the same color as their respective line plots. Since the trend is being described, between 2008 and 2018, the X-axis is labeled with only 3 years to reduce the ink usage and clumsiness.  

Fig 11: Yearly Cost per CO2 emissions for the US - 
Yearly economic costs per CO2 emissions for the USA are calculated by dividing the cost of disaster for the USA by its CO2 emissions, per year. With this data, a scatterplot is plotted for ‘Yearly Cost per CO2 emissions for the US’ against the years and a regression line is plotted to observe the trend between 1980 and 2018 Here also, just three years are shown on Y axis, since only trend of the points is being observed and not focused on individual year. 
 
#### Data Sources-

https://www.kaggle.com/datasets/kkhandekar/co2-emissions-1960-2018 
https://www.kaggle.com/datasets/michaelbryantds/billiondollar-disasters 
https://ourworldindata.org/natural-disasters 
Country Polygons as GeoJSON - Dataset - DataHub - Frictionless Data 
https://ourworldindata.org/natural-disasters 

 
#### References-
 
NOAA National Centers for Environmental Information (NCEI) U.S. Billion-Dollar Weather and Climate Disasters (2022). https://www.ncei.noaa.gov/access/billions/, DOI: 10.25921/stkw-7w73 
 
Centre for research on the epidemiology of disasters: Centre for research on the epidemiology of disasters. Centre for Research on the Epidemiology of Disasters, Centre for Research on the Epidemiology of Disasters. Available at: https://www.cred.be/publications  
 
Paper, D.A. (2020) How climate change contributed to the Australian bushfires, Double A Paper Supplier. Available at: https://us.doubleapaper.com/home/climate-change-australian-bushfires/  

