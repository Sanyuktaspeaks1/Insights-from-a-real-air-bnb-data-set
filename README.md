# Insights-from-a-real-air-bnb-data-set
# Select the data of your fav city from
[https://insideairbnb.com/get-the-data/](https://insideairbnb.com/get-the-data/)
I have done all the calculations based on data from Hawaii
![image](https://github.com/user-attachments/assets/b188dbfe-e13b-4ed3-961f-0f3d872debb4)
After landing on the website you can click on calendar.csv.gz and it will be downloaded!

If you are using Google Collab then .gz will give you no issues
```diff
import pandas as pd
calendar = pd.read_csv('calendar.csv.gz')
```

# Questions that you might want to address about the given data
Let`s dive into exciting insights!
# 1 Want to know the number of available and unavailable rooms
```diff
calendar.available.value_counts()
```
![image](https://github.com/user-attachments/assets/869fa62b-b464-4e3e-bf51-fe811c59e127)

# 2 Purpose: Calculates the percentage of available (t) and unavailable (f) dates.
Explanation:
value_counts(normalize=True) gives proportions.
Multiplying by 100 converts the proportions into percentages
```diff
availability_percentage = calendar['available'].value_counts(normalize=True) * 100
availability_percentage
```
# 3 Let`s Count the busiest day! 
Hint: We will be counting the most unavailable days (given by f)
```diff
busiest_dates = calendar[calendar['available'] == 'f']['date'].value_counts()
print("Busiest Dates:")
print(busiest_dates.head())
```
# 4 Plot a bar graph to show availability percentage
```diff
import matplotlib.pyplot as plt
availability_percentage.plot(kind='bar', color=['green', 'red'])
plt.title('Availability Percentages')
plt.ylabel('Percentage')
plt.xlabel('Available (t/f)')
plt.show()
```
![image](https://github.com/user-attachments/assets/fe65b8d9-d871-46c1-80f5-1ba58d2c7ef1)

# 5 Plot the busiest day
busiest_dates.head(10).plot(kind='bar', color='orange')
plt.title('Top 10 Busiest Dates')
plt.ylabel('Number of Listings Unavailable')
plt.xlabel('Date')
plt.show()
![image](https://github.com/user-attachments/assets/470d83c9-ef82-4989-99cf-32e16a7693ba)






