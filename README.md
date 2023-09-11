# **Fitness Smartwatch Exploratory Analysis**

This is the final project from the course I took from Coursera (Google Data Analytics Course). For this project, I was assigned to be a data analyst for a fitness smartwatch company, Bellabeat.

## Background

Bellabeat is a a tech company focusing on health products like smartwatch for women since 2013. Bellabeat has a huge potential to become a large player in the global smart device market. As a junior data analyst in this company, I am required to analyze Bellabeat’s fitness tracker app to find opportunities to grow. I am required to look into insights, trends and correlations on how the customers are using the app in order to improve Bellabeat’s marketing strategy.

## Steps

Here are the six steps we do prior our data analysis:

1. Ask

2. Prepare

3. Process

4. Analyze

5. Share

6. Act

## Ask

These are the questions we ask prior our analysis:

* What are some trends in the smart device usage?

* How could these trends applied to Bellabeat customers?

* How could these trends influence Bellabeat’s marketing strategy?

## Prepare

1. The data is available for public in Kaggle:Fitbit Fitness Tracker Data and includes 18 CSV files.

2. The respondents are survey takers from Amazon Mechanical Turk between 12 March - 12 May in year 2016.

3. There are around 30 respondents in this survey.

4. Data includes collecting physical activity recorded in minutes, heart rate, sleep monitoring, daily activity and steps.

### Is the Data ROCCC?

According to the theory we learned in Google Analytics Capstone Project, a good data source is ROCCC, which stands for: Reliable, Original, Comprehensive, Current, Cited. So, is the data obtained ROCCC? Here’s my analysis:

* Reliable: LOW, because it only has around 30 respondents

* Original: LOW,  because the data is provided by the third party (Amazon Mechanical Turk), not conducted by Bellabeat itself.

* Comprehensive: MEDIUM, because most parameters match most of Bellabeat product’s parameters.

* Current: LOW,  because the data is recorded 7 years ago. The customer’s habits may have changed since then.

* Cited: LOW, The data is gathered from the Third Party and we do not know how they gather the data.

### Data selection

For this analysis,  we are going to use three CSV files. You can find the three CSV files here.  The three files we are going to use are:

* dailyActivity_merged.csv

* weightLogInfo_merged.csv

* sleepDay_merged.csv

* hourlyCalories_merged.csv



### Tools
The tools we are using for this data analysis are:

* Microsoft Excel (Data cleaning and manipulation)

* MYSQL (Query and analysis)

* Tableau (Data visualization)

## Process

1. All three files have id. They have 10 integers and are supposed to indicate a unique customer id for one customer. To shorten the id, I use the RIGHT(=RIGHT(B2,4)) function to only take the last 4 integers to make the id more simple and concise.  I also renamed the field from id to customer_id. I applied them to all the three CSV files including id.

2. I use the comma function to round up all the number into two decimal places to make them less complicated to read. I applied them to all CSV files including numerical values.

3. All three CSV files used dash (-) to indicate null or missing values. I replaced dash (-) with zero (0) to indicate the null values. To replace them all, I use the filter options to all columns with null values. I unchecked everything but dash (-) and replace them with zero (0). Afterwards, I checked all the values to return all values including the new missing values (where dash has been replaced with zero). I applied this to all CSV files. 

4. For dailyActitivity_merged. csv, I make a new column called total_minutes and SUM all the values from Lightly Active Minutes, Moderately Active Minutes, Very Active Minutes and Sedentary Active Minutes). We use the sum function =SUM(K2,L2,M2,N2). 

5. For dailyActitivity_merged. csv,  I use the IF function to indicate whether each user is Active or Not Active. We use the data from Total Minutes for this indicator. If the Total Minutes is less than 1000, then that user is not Active. We use the =IF(E2<1000,"Not Active","Active") function. 

6. For dailyActivity_merged.csv, I use the date values from column B and convert it to days of the week(Monday, Tuesday, etc) by using  =TEXT(C2,”dddd”) function. 

7. For WeightLogInfo_merged, I add the column bmi_status to indicate customer's bmi whether they are normal weight or overweight. . If the BMI is smaller than 25, it means the customer has normal weight. If not, the customer is overweight. I use the =IF(F2<25, "Normal Weight","Overweight") function. 

8. For SleepDay_merged, I converted the numerical values for minutes_asleep and minutes_total into hours_asleep and hours_total. I divided the minutes to 60(1 hour= 60 minutes) to convert them into hour values. I also get rid of Total_Sleep_Record and convert the date to 'short date' to get rid of the time. 

## Analyze

After cleaning the data, I import it to SQL for analysis. You can view my SQL queries [here]((https://github.com/carolinenata/bellabeatproject/blob/main/BellabeatSQL.sql).  

Here are some notable analysis we found:

* There are 32 customers in daily_act file and hourly_steps, 8 customers in weight_log file, and 24 customers in sleep_day.

* Tuesday is the most popular day among users while Sunday being the least.

* Customers' total distance are majorly lightly active distance. We can assume that they do not walk too far when using their smartwatch

* Customers' total minutes are majorly sedentary minutes. We can assume that the majority of the customers are not very active.

* The data is taken from April 12 - May 12. Customers are way much more active in April.

* Compared to the rest of the users, customers number 81 uses the smartwatch 61 times! Compared to the rest of the customers where majority uses the smartwatch around 30 times, we need to question the validity of customer 81. We assume he is an insider or a Bellabeat superfan that fills in the survey plenty of times.

* From the weight_log files, 5 customers are overweight 3 are normal weight.

* Overweight customers tend to have lower distance than normal weight customers. However, overweight customers have more total minutes than normal weight customers.

*Overweight customer sleep more than normal weight customers. \

I also perform statistical calculations(mean, min, max, standard deviation) to identify more trends. To display the results more conscisely, I use the Form Editor in MySQL. 

<img width="462" alt="Screen Shot 2023-09-11 at 1 00 00 PM" src="https://github.com/carolinenata/portfolio/assets/138493962/ce2a2a4a-0dd2-435a-a2d0-40e975614902">


From the calculations, we can conclude that:

The Average Total Minutes of the users are 1218 minutes. According to Centers of Disease Control and Prevention (CDC), adults need 150 minutes of of moderate-intense physical activity per week. Since the survey is taken in a 3 month period, the ideal minutes would be  1800 minutes (Considering each month has 4 weeks, therefore we are looking into 12 weeks in total. [12x150 minutes = 1800 minutes]. We can conclude that  Bellabeat users do not meet this healthy criteria. 

The Average Total Steps of the users are 7,630 steps. According to Medical News Today, they recommend adults to walk 10,000 steps per day. Even though the Average Total Steps of the users do not meet this criteria, the Max Total Steps for the users is 36,000. We can assume that some users are attempting a healthy lifestyle and starting with sedentary physical activity such as walking. 

The Standard Deviations for Total Minutes, Total Steps and Total Distance are considered to be very high.  The higher the standard deviation, the less exact the experiment. In order for us to have a lower standard deviation that will be closer to the mean, we need more samples from a more targeted customer segment. 

## Share

In this step, we create visualizations to display our findings. We are using Tableau. 

**Most Popular day for Users**

<img width="730" alt="Screen Shot 2023-09-11 at 12 59 33 PM" src="https://github.com/carolinenata/portfolio/assets/138493962/955604ae-9fda-40d1-9ac5-230781124784">

From this chart, we can conclude that Tuesday is the most active day for the users because they have the highest total minutes and total distance while Sunday is the least active day.

**Sleeping Hours Overweight vs Normal Weight** 

<img width="656" alt="Screen Shot 2023-09-11 at 12 59 36 PM" src="https://github.com/carolinenata/portfolio/assets/138493962/6f5bd5c2-ce03-4945-a269-048375cdaa16">

From this chart, we can conclude that overweight people tend to sleep more than those with healthy weight. Although, the difference is not that far.

**Total Minutes Overweight vs Underweight**

<img width="506" alt="Screen Shot 2023-09-11 at 12 59 40 PM" src="https://github.com/carolinenata/portfolio/assets/138493962/65a9c225-249f-4fed-bdf7-e56a96809652">

Although overweight people slept more, they are also more active than healthy weight people. we can conclude that the overweight people have a strong desire to exercise and trying to improve their lifestyl

**Calories burned per hour Overweight vs Normal Weight**

<img width="730" alt="Screen Shot 2023-09-11 at 12 59 43 PM" src="https://github.com/carolinenata/portfolio/assets/138493962/2a0d3c9c-7fda-4dfa-b70f-589bc13874e0">

From this line chart, we can conclude that overweight people attempt to burn more calories than normal weight people. These two groups also peak at 18:00, which is after work hours. We can conclude that these two groups start being more active after works (Example, going to the gym after work).

**Sleeping Hour April Vs May**

<img width="709" alt="Screen Shot 2023-09-11 at 12 59 46 PM" src="https://github.com/carolinenata/portfolio/assets/138493962/8eaa5ad1-5f11-441e-ba59-9f16b1962eae">

Bellabeat users slept more on April than May. We can assume they got more busy during that time period or they stop tracking their sleep properly using the smartwatch because they got bored.

**Bellabeat User Activity**

<img width="734" alt="Screen Shot 2023-09-11 at 12 59 51 PM" src="https://github.com/carolinenata/portfolio/assets/138493962/34124810-2d79-4fda-b0c6-8ab782c12490">

Here are the users of Bellabeat. Surprisingly, user 81 is the most active out of the bunch. In fact, so active that his number is an outlier. We can assume either he is a big fan of Bellabeat or an insider bias because aside from the smartwatch activities, the survey does not include any inquiries about their demographic background (age, occupation, job, income level etc).

View my Tableau Dashboard here in [Tableau Public](https://public.tableau.com/app/profile/caroline.natasia/viz/BellabeatProject_16929769516010/Dashboard1)


## Act

What are the trends identified?
Sedentary minutes has the highest compared to lightly active minutes, very active minutes and fairly active minutes. We can assume that the customers of Fitbit are not active users and do not exercise often.

Customers are most active in the weekdays (Tuesday, Wednesday, Thursday) and less active on the weekends.

Overweight people might sleep more, but they also spent more minutes and burn more calories per hour than Healthy Weight people. We learn that there is an attempt of trying to lose weight and leading a healthy lifestyle compared to Healthy Weight people.

Users with customer ID 81 is the most active Fitbit user. Compared to the rest of the respondents, he uses the app 81 times while the rest are around 31 times. There might be insider bias because the background of these respondents is not transparent. There is no survey questions indicating their demography and background.

People tend to sleep less in April than May. According to News in Health getting enough sleep is crucial for leading a healthy lifestyle. We can use this opportunity to encourage Bellabeat users to sleep earlier and add it to our marketing strategy.

How could these trends influence Bellabeat's Marketing Strategy?

Bellabeat can use social media to increase healthy life awareness (Instagram, Tiktok, etc). They can also encourage existing Bellabeat users to follow them on socials so they can participate in limited time events run by Bellabeat like:Updating the socials more on weekdays (preferrably after work) to invite users to exercise through Shorts and Reel

Since most exisiting Bellabeat users spend the most sedentary minutes, Bellabeat can implement a relaxing workout activity for a community gathering. They can make a walking marathon event (because walking is a sedentary activity) and encourage Bellabeat users to upload their experience in socials.

Implement a gamification feature into Bellabeat Smartwatch's app to encourage users to be active. It can remind users daily to workout. For example, if a user reached a certain number of active minutes per day, they will get points. These points can then be exchanged to get discount on Bellabeat's existing products and other benefits. Also, if the user shares their achievements on socials, they will get more points too! They can also apply this gamification method to encourage users to sleep earlier too.

How can we improve this analysis in the future?

Instead of taking data from a third party, Bellabeat should try find data using a primary source like spreading their own survey to a group of targeted respondents.

In the survey, try adding 'background questions' like age, income, job, and lifestyle questions to have a clear idea on the customer segment in the market.

We need more respondents in the survey to have a more less skewed data that have lower standard deviation.

