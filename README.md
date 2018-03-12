# irish_EV_charger_status

Objective

I am working with a dataset of statuses at EV charging stations in Ireland and building a model to predict the status of a charger at a particular time.
_________________________________

Why I Chose this Topic

I am excited about the shift from vehicles with internal combustion engines to electric vehicles. With Tesla leading the way and making EVs "cool" and "futuristic", the world is beginning to take note of the significant benefits of using electric vehicles. It's about time we start taking care of this beloved planet.

My mother bought one of the first Nissan Leafs a few years ago and I have been excited about EVs ever since. Without an infrastucture for EVs, however, they would be fairly useless. Tesla has done an incredible job building charging stations all over the US and beyond, with a total of over 1,100 to date. I was ecstatic to come across James Burkill's dataset of charge point statuses in Ireland because there is not very much data available on EV usage or charging. I am creating a predictive model of charge point statuses because it would be a tangible tool for people to determine when they can charge their vehicle, freeing up time and energy better spent in other areas of life. Who knows, in a decade or two, there may be little to no gas stations and charge points galore!
_________________________________

Data

The data I am working with consists of 14 months of timestamped statuses of electric vehicle charge points in Ireland. The status of several charge points in Ireland were recorded at five-minute intervals for the duration of the 14 months (November 2016 through December 2017). Each line of the dataset includes the data and time, a charge point ID, the type of charge point, status, address, and latitude and longitude.

(*Note: the above description of the data was paraphrased from the original collector of the data, James Burkill --> http://www.mlopt.com/?p=6598)

All data is from http://www.mlopt.com/?p=6598, courtesy of James Burkill. Thank you James! I originally found his post of the data on Reddit forum r/datasets (https://www.reddit.com/r/datasets/).
_________________________________

Questions I Hope to Answer

1. When will the charger(s) be free? In other words, when is the best time to use the charger(s)?
2. Should you charge your car on the way or way home from work? In other words, are the chargers more likely to be free during the morning hours or afternoon hours?
3. What times should someone avoid going to a charge point? In other words, when is the highest demand for the charger(s)? 
_________________________________

My Model

I will be using logistic regression as a baseline predictor of the status of a charge point at a particular time, day, and place. From there, I will experiment with other classficiation models including decision trees and random forest. I will also attempt to use an unsupervised k-means model to group the various charge points into tiers of usage (from 'rarely used' to 'used very often').
_________________________________

Project Updates:

Update 2/11/18: I have spent some time cleaning the data and it is almost ready to be used to train the model. However, I encountered some difficulty in converting the data and time into a datetime type in pandas with python. I successfully concatenated all 14 months into a single dataframe which has an absurd 17,314,536 rows of data. As mentioned by James Burkill in the original description of the dataset, some of the charge points were moved during the 14-month period and so the charge point ID is not a reliable marker of a consistent location. I will use the latitude and longitude as markers of a charge point's location instead.

Update 2/19/18: I *think* the data is all cleaned and ready to be used to start training and testing the models I'm going to build. I am planning on using a linear regression algorithm and a k nearest neighbor algorithm but will experiment with others and see which is most successful towards my goal of predicting the availabilty of a particular charging point.

Update 2/20/18: I am working with time series data of 14 months of 5-minute intervals of many different electric vehicle charging stations. I find myself in a bit of a bind, or rather a challenge in which I could proceed in a few directions. And I’m not sure which is the best. One of the main features of my data that I’m concerned with is the Status column (which I’ve split into dummy variable but can  undo that as needed). The Status can either be OOC (out of contact), OOS (out of service), Occ (occupied), or Part (partly occupied). An omission of a timestamp means the status is essentially available. There are a lot of OOC and OOS markings and basically all of that data is unusable to me. And there are time periods of NaN readings as well. I took one approach which was to find the addresses with at least 80% data (100% being consistent 5-minute interval readings for 14 months). I was left with 12 of 561 addresses that passed the threshold. But within that new dataframe, a high percentage of entries are either out of contact OOC or out of service OOS. I’m struggling with how to choose which chunks of the data to work with and which parts to discard. I could go in two directions: 1. pick a couple of charge points (out of 561 total) to predict the status of, working with less data and less omissions, or 2. clean the data set more and work with as many charge points as possible, working with more data including more errors. I am going to proceed with option 1 for now, picking the datasets with the most data, and then explore option 2 if I have time.

Update 2/26/18: How have I explored the data and what insights have I gained as a result? 1. Working with a large dataset takes a lot of time, especially when I need to restart the kernel and re-do the output. 2. It can be challenging to work with data when an absence of an entry implies a certain value. In my cause, looking at the status of a charge point, the lack of an entry implied that the charge point was available. I had to reframe how i was thinking about the data, and some of my questions, like changing ‘when is the charge point available?’ to ‘when is the charge point not available?’ and figuring out when it is available based on that second question. 3. I used get_dummies, but it was useful to keep in place the original Status column so that i could utilize both types of categorization. 4. When beginning the logistic regression, I had to decide whether to count missing data as part of the 'Available' group or 'Not Available' group.

Update 3/1/18: The project is coming to a close (for now). I have used several models including linear regression, logistic regression, decision (classification) tree, random forest classification, and a bagged regression tree. I compared (when possible) the RMSE, sensitivity/TPR, precision/PPV, accuracy, and F1 scores to consider which models were most effective in answering my questions. My random forest and bagged tree models were the most successfully predictive and "best" models.
_________________________________

Conclusion

I will begin by answering the questions I began this project with:

*Note: the questions below are answered in regards to a single EV charge point located at Clifton House, 11A Fitzwilliam Street Lower, Dublin 2, County Dublin

1. When will the charger be free? In other words, when is the best time to use the charger?

The best time to use the charger is in the first eighth of the day, from around midnight to 3am. The other period in which the charge point is likely to be free is in the first two fifths of the day and not in the last five minutes of the hours, from 4-4:55am, 5-5:55am, 6-6:55am, 7-7:55am, and 8-8:55am.

2. Should you charge your car on the way or way home from work? In other words, is the charger more likely to be free during the morning hours or afternoon hours?

You should charge your car on the way to work (if you live in Ireland). The charger is more likely to be free, or available, in the morning, and more likely to be unavailable in the afternoon and evening.

3. What times should someone avoid going to a charge point? In other words, when is the highest demand for the charger?

Someone should avoid going to the charge point after work, or if it is not one of the "best" periods specified in the answer to the first question above. However, this is not absolute and the charge point may be available at any time.


Project Summary

My objective was to work with a dataset of statuses at EV charge points in Ireland and build a model to predict the status of a charger at a particular time. Though I was not able to fully complete that objective in the scope of this project, I made large steps toward that goal and was able to answer the questions above to predict the status of the charger based on certain characteristics or features.

This project was a fun opportunity to work with time series data. I improved my graphing skills and now feel very comfortable working with the datetime type and capabilities in pandas. I built models to classify a particular EV charge point as 0 for available or 1 for unavailable. As with many data science projects, the majority of my time was spent on pre-processing. The main challenge I faced in the pre-processing step was refining the large dataset I began with (17,314,536 rows of data after the concatenating 14 months) and choosing the best subset to answer my questions.

I had to make thoughtful decisions about which data to work with based on two subtleties of the data. The first subtlety was that the data of when a status was avaialable was implied by omitted timestamps. Basically, if there was an absence of a timestamp marking the status of a charge point at a particular 5-minute interval within the dataset, the charge point was available at that time. The second subtley that affected my decision was that some charge points were moved during the 14-month collection period, and when they were moved, that charge point ID was usually changed. This meant I could not use the charge point ID to have a contiguous stream of information about the status of a particular charge point. Location is a feature of the data that would be fascinating to further explore, but was not in the span of this project. 

When I was going through the data to refine it after cleaning it, I first went through and chose the charge points to work with based on which charge points had the most data. I soon realized that was not a good thing, as the sheer amount of data for a charge point reflected the cumulative number of intervals in which a charge point's status was Occ (fully occupied), Part (partly occupied), OOS (out of service), and OOC (out of contact). If a charge point was OOS or OOC for an extended period of time, its cumulative data count would be high. Instead, I found the charge points with the least summed OOC and OOS values. This gave me a list of 10 charge points (out of 561 total) that had the least bad data mixed in. From there I saw that 4 of those 10 addresses had very, very little data, which left me with six possible charge points to work with. By now I had decided it would be smart to pick a single charge point to work with to build models (ideally that model could be used with any other charge point in the dataset in the future). Of the six possible charge points, I plotted a stacked bar graph of status values for each and made a well-informed decision to work with the 'clifton' charge point because it had consistent usage across all 14 months and was one of the two most heavily-used charge points.

After I had chosen the charge point I labeled 'clifton' (as its address was 'Clifton House, 11A Fitzwilliam Street Lower, Dublin 2, County Dublin'), I had to add in the data of when the charge point status was available. I accomplished this by creating a new dataframe of 5-minute intervals for the duration of the 14 months for this single charge point, with the status marked as 'A' for available in all rows. The features were the same as the other dataset. With this newly created dataset in hand, I updated the value in each row's 'Status' column to reflect the status of the clifton charge point in the original dataset (Part, Occ, or OOC) if it was different.

Finally, I got to the models. First I used linear regression to create a makeshift baseline for classification of the status of clifton. From there I created a train/test split and made a logistic regression model, classification tree, bagged tree, and random forest. Initially, I used the 'Hour' feature to predict the class. This gave me some funky results with the classifiers and it became clear that my logistic regression model was predicting based on the null accuracy, as that was above 70%. After working with a decision tree, it was obvious that the 'Hour' feature was not very predictive of the Status. The decision tree told me that 'Minute', however, was.

Using some good ol' algebra and critical thinking skills, I created a new feature of the clifton data called 'Period' which reflected which 5-minute period of the day each timestamped Status belonged to, from 0 to 287 (there are 288 5-minute periods in a day). Period = 12*Minute/60 + 12*Hour was my handy equation, where Minute reflected a value between 0 and 60 and Hour represented a value between 0 and 24. I predicted that 'Period' would be the most predictive feature between 'Hour', 'Minute', and 'Period', but surprisingly, 'Minute' was the most predictive by far. So in the end, I used 'Minute' as the main predictive feature, but bagged tree and random forest were my best models, which considered all three of those features.

Looking at the performance metrics, I compared (when possible) the RMSE, sensitivity/TPR, precision/PPV, accuracy, and F1 scores of all five models I used. Random forest and bagged tree had the lowest RMSE and highest accuracies. Based on this and the fact that both of those models consider the feature importances of multiple features led me to the conclusion that the best models for this problem are random forest and bagged tree.

The value of using many models to explore a problem or project became clear to me, as I learned why certain models were not working as well from the results and information given by other models. For example, my decision tree, which had a low feature importance for 'Hour', showed me why my logistic regression model was not that successful at first--because 'Hour' was not a very predictive of 'Status'.  

_________________________________

Future Exploration

As I only worked with a single charge point out of 561 total, there is still a huge space for exploration within the original dataset. It would be interesting to look at patterns across the whole dataset as well, including how location affects 'Status' in various ways.

I have several questions and curiosities that were beyond the scope of this project:

1. Do the busiest times vary by location?
2. What areas tend to have more availability?
3. Is the value of each charger greater than the cost? in other words, is each charger being used enough to make it worthwhile?
4. Does the distribution of locations match the needs by location?
5. Is the use of the chargers increasing over time?
6. Which types of chargers are being used the most? Least?
7. What is the average time someone spends at a charge point?
8. Which features of a charge point are most important in predicting whether or not a charge point is available to use at a particular time and day?

Contact: If you have any questions or would like to discuss this project or any of my work further, please email me at datagrlxyz@gmail.com.
