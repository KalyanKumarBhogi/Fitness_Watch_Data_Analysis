**Fitness Watch Data Analysis involves analyzing the data collected by fitness wearables or smartwatches to gain insights into users’ health and activity patterns. These devices track metrics like steps taken, energy burned, walking speed, and more.** <p>


# Fitness Watch Data Analysis: Process We Can Follow <p>
**Fitness Watch Data Analysis is a crucial tool for businesses in the health and wellness domain. By analyzing user data from fitness wearables, companies can understand user behavior, offer personalized solutions, and contribute to improving users’ overall health and well-being.** <p>

**Below is the process we can follow while working on the problem of Fitness Watch Data Analysis:** <p>

1. **Collect data from fitness watches, ensuring it’s accurate and reliable.** <p>
2. **Perform EDA to gain initial insights into the data.** <p>
3. **Create new features from the raw data that might provide more meaningful insights.** <p>
4. **Create visual representations of the data to communicate insights effectively.** <p>
5. **Segment user’s activity based on time intervals or the level of fitness metrics and analyze their performance.** <p>


**So, the process starts with collecting data from a fitness watch. Every fitness watch works with an app on your smartphone. You can collect data from that app on your smartphone. For example, in my case, I collected my fitness watch’s data from Apple’s Health app.** <p>

# Fitness Watch Data Analysis using Python <p>
**Now let’s get started with the task of Fitness Watch Data Analysis by importing the necessary Python libraries and the dataset:** <p>

import pandas as pd <p>
import plotly.io as pio <p>
import plotly.graph_objects as go <p>
pio.templates.default = "plotly_white" <p>
import plotly.express as px <p>

data = pd.read_csv("Apple-Fitness-Data.csv") <p>
**head of the dataset** <p>
data.head() <p>

![image](https://github.com/KalyanKumarBhogi/Fitness_Watch_Data_Analysis/assets/144279085/34516568-06f2-493b-b6a6-e33dc016d47a)

**Tail of the dataset** <p>
data.tail() <p>
![image](https://github.com/KalyanKumarBhogi/Fitness_Watch_Data_Analysis/assets/144279085/e5e2b783-97fb-4a95-bf08-897cac7d35a9)

**descriptive statistics of dataset** <p>
data.describe() <p>
![image](https://github.com/KalyanKumarBhogi/Fitness_Watch_Data_Analysis/assets/144279085/86a017c5-3b9c-4659-9621-fc8d6f4c6736)

data.info() <p>

![image](https://github.com/KalyanKumarBhogi/Fitness_Watch_Data_Analysis/assets/144279085/8f9a51cc-3843-44dd-92eb-c8b42267efd7)

**Let’s have a look if this data contains any null values or not:** <p>

data.isnull().sum() <p>

![image](https://github.com/KalyanKumarBhogi/Fitness_Watch_Data_Analysis/assets/144279085/f29977d9-2562-469c-a842-73c5d83435fa)

**So, the data doesn’t have any null values. Let’s move further by analyzing my step count over time:** <p>

fig1 = px.line(data, x="Time", <p>
               y="Step Count", <p>
               title="Step Count Over Time") <p>
fig1.show() <p>

![image](https://github.com/KalyanKumarBhogi/Fitness_Watch_Data_Analysis/assets/144279085/948845c6-324a-4ce0-9111-9921219131a4)

**Now, let’s have a look at the distance covered over time:** <p>

fig2 = px.line(data, x="Time", <p>
               y="Distance", <p>
               title="Distance Covered Over Time") <p>
fig2.show() <p>

![image](https://github.com/KalyanKumarBhogi/Fitness_Watch_Data_Analysis/assets/144279085/0607304a-b206-4d86-84bc-83bd0bb26e10)

**Now, let’s have a look at my energy burned over time:** <p>

fig3 = px.line(data, x="Time", <p>
               y="Energy Burned", <p>
               title="Energy Burned Over Time") <p>
fig3.show() <p>


![image](https://github.com/KalyanKumarBhogi/Fitness_Watch_Data_Analysis/assets/144279085/a4054726-0433-4d5d-a02e-3e0f2bcc73b0)

**Now, let’s have a look at my walking speed over time:**

fig4 = px.line(data, x="Time", <p>
               y="Walking Speed", <p>
               title="Walking Speed Over Time") <p>
fig4.show() <p>
 
![image](https://github.com/KalyanKumarBhogi/Fitness_Watch_Data_Analysis/assets/144279085/05f429b9-e6f0-4441-b478-4e7a7cb6f2de)

**Now, let’s calculate and look at the average step counts per day:** <p>

average_step_count_per_day = data.groupby("Date")["Step Count"].mean().reset_index() <p>

fig5 = px.bar(average_step_count_per_day, x="Date", <p>
              y="Step Count", <p>
              title="Average Step Count per Day") <p>
fig5.update_xaxes(type='category') <p>
fig5.show() <p>

![image](https://github.com/KalyanKumarBhogi/Fitness_Watch_Data_Analysis/assets/144279085/0391bddb-da53-46ad-a75b-624178833fdb)

**Now, let’s have a look at my walking efficiency over time:** <p>
data["Walking Efficiency"] = data["Distance"] / data["Step Count"] <p>

fig6 = px.line(data, x="Time", <p>
               y="Walking Efficiency", <p>
               title="Walking Efficiency Over Time") <p>
fig6.show() <p>

![image](https://github.com/KalyanKumarBhogi/Fitness_Watch_Data_Analysis/assets/144279085/5bdbf12b-c69d-4128-bc52-99a26095091d)

**Now, let’s have a look at the step count and walking speed variations by time intervals:** <p>

time_intervals = pd.cut(pd.to_datetime(data["Time"]).dt.hour, <p>
                        bins=[0, 12, 18, 24], <p>
                        labels=["Morning", "Afternoon", "Evening"],  <p>
                        right=False) <p>

data["Time Interval"] = time_intervals <p>

fig7 = px.scatter(data, x="Step Count", <p>
                  y="Walking Speed", <p>
                  color="Time Interval", <p>
                  title="Step Count and Walking Speed Variations by Time Interval", <p>
                  trendline='ols') <p>
fig7.show()   <p>

![image](https://github.com/KalyanKumarBhogi/Fitness_Watch_Data_Analysis/assets/144279085/f192f679-fad5-4e62-b134-207be0a8d661)

# Conclusion <p>
**Fitness Watch Data Analysis provides valuable insights into user health and activity patterns. The analysis involved collecting and exploring data from a fitness watch dataset, encompassing metrics such as step count, distance covered, energy burned, and walking speed. Visualizations were created to depict these metrics over time, offering a comprehensive overview of daily activities. Additionally, average step counts per day and walking efficiency were calculated and visualized, providing a deeper understanding of overall performance. The analysis also segmented data into time intervals, revealing variations in step count and walking speed throughout the day. These insights can be instrumental for businesses in the health and wellness domain to tailor personalized solutions and enhance users' overall well-being.**










