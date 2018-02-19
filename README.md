# irish_EV_charger_status

Objective

I am working with a dataset of statuses at EV charging stations in Ireland and building a model to predict the status of a charger at a particular time.

_________________________________

Data

The data I am working with consists of 14 months of timestamped statuses of electric vehicle charge points in Ireland. The status of several charge points in Ireland were recorded at five-minute intervals for the duration of the 14 months (November 2016 through December 2017). Each line of the dataset includes the data and time, a charge point ID, the type of charge point, status, address, and latitude and longitude.

(*Note: the above description of the data was paraphrased from the original collector of the data, James Burkill --> http://www.mlopt.com/?p=6598)

All data is from http://www.mlopt.com/?p=6598, courtesy of James Burkill. Thank you James! I originally found his post of the data on Reddit forum r/datasets (https://www.reddit.com/r/datasets/).

Update 2/11/18: I have spent some time cleaning the data and it is almost ready to be used to train the model. However, I encountered some difficulty in converting the data and time into a datetime type in pandas with python. I successfully concatenated all 14 months into a single dataframe which has an absurd 17,314,536 rows of data. As mentioned by James Burkill in the original description of the dataset, some of the charge points were moved during the 14-month period and so the charge point ID is not a reliable marker of a consistent location. I will use the latitude and longitude as markers of a charge point's location instead.

Update 2/19/18: I *think* the data is all cleaned and ready to be used to start training and testing the models I'm going to build. I am planning on using a linear regression algorithm and a k nearest neighbor algorithm but will experiment with others and see which is most successful towards my goal of predicting the availabilty of a particular charging point.
_________________________________

Why I Chose this Topic

I am excited about the shift from vehicles with internal combustion engines to electric vehicles. With Tesla leading the way and making EVs "cool" and "futuristic", the world is beginning to take note of the significant benefits of using electric vehicles. It's about time we start taking care of this beloved planet.

My mother bought one of the first Nissan Leafs a few years ago and I have been excited about EVs ever since. Without an infrastucture for EVs, however, they would be fairly useless. Tesla has done an incredible job building charging stations all over the US and beyond, with a total of over 1,100 to date. I was ecstatic to come across James Burkill's dataset of charge point statuses in Ireland because there is not very much data available on EV usage or charging. I am creating a predictive model of charge point statuses because it would be a tangible tool for people to determine when they can charge their vehicle, freeing up time and energy better spent in other areas of life. Who knows, in a decade or two, there may be little to no gas stations and charge points galore!
_________________________________

Questions I Hope to Answer

1. Using a predictive model that I create, when will the chargers be free? In other words, when is the best time to use the chargers?
2. Should you charge your car on the way or way home from work? In other words, are the chargers more likely to be free during the morning hours or afternoon hours?
3. What times should someone avoid going to a charge point? In other words, when is the highest demand for the chargers? Does this vary by location?
4. What areas tend to have more availability?
5. Is the value of each charger greater than the cost? in other words, is each charger being used enough to make it worthwhile?
6. Does the distribution of locations match the needs by location?
7. Is the use of the chargers increasing over time?
8. Which types of chargers are being used the most? Least?
9. What is the average time someone spends at a charge point?
10. Which features of a charge point are most important in predicting whether or not a charge point is available to use at a particular time and day?
_________________________________

My Model

I will be using a linear regression model to predict the status of a charge point at a particular time, day, and place. I will also use an unsupervised k-means model to group the various charge points into tiers of usage (from 'rarely used' to 'used very often').
_________________________________

Questions I will be answering soon:

How have I explored the data and what insights have I gained as a result?
Will I be able to answer my questions with this data, or will I need to gather more data (or adjust my questions)?
