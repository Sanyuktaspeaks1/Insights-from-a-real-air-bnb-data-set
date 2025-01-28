# Insights-from-a-real-air-bnb-data-set
# :white_check_mark: Select the data of your fav city from
[https://insideairbnb.com/get-the-data/](https://insideairbnb.com/get-the-data/)
I have done all the calculations based on data from Hawaii
![image](https://github.com/user-attachments/assets/b188dbfe-e13b-4ed3-961f-0f3d872debb4)
After landing on the website you can click on calendar.csv.gz and it will be downloaded!

If you are using Google Collab then .gz will give you no issues
```diff
import pandas as pd
calendar = pd.read_csv('calendar.csv')
```

# :white_check_mark: Questions that you might want to address about the given data
Let`s dive into exciting insights!
# 1 Want to know the number of available and unavailable rooms
```diff
calendar.available.value_counts()
```
![image](https://github.com/user-attachments/assets/869fa62b-b464-4e3e-bf51-fe811c59e127)

# 2 Purpose: Calculates the percentage of available (t) and unavailable (f) dates.
* Explanation:
* value_counts(normalize=True) gives proportions.
* Multiplying by 100 converts the proportions into percentages
```diff
availability_percentage = calendar['available'].value_counts(normalize=True) * 100
availability_percentage
```
# 3 Let`s Count the busiest day! :triangular_flag_on_post:
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
```diff
busiest_dates.head(10).plot(kind='bar', color='orange')
plt.title('Top 10 Busiest Dates')
plt.ylabel('Number of Listings Unavailable')
plt.xlabel('Date')
plt.show()
```
![image](https://github.com/user-attachments/assets/470d83c9-ef82-4989-99cf-32e16a7693ba)


## :page_facing_up: Download listings dataset of Hawaii from https://data.insideairbnb.com/united-states/hi/hawaii/2024-09-13/data/listings.csv.gz 
```diff
import pandas as pd
listings = pd.read_csv('/content/listings (1).csv')
```
![image](https://github.com/user-attachments/assets/5cfe421f-6daf-46e8-b776-9af088335542)
```diff
listings.columns
```
![image](https://github.com/user-attachments/assets/74ce7541-e3e0-473b-af3c-469f21838675)


## :white_check_mark: Room type and price is given seperately
Let`s Combine and visualize them
```diff
import matplotlib.pyplot as plt
price_by_room = listings.groupby('room_type')['price'].mean()
print(price_by_room)

# Plot price by room type
price_by_room.plot(kind='bar', color='cyan')
plt.title('Average Price by Room Type')
plt.ylabel('Average Price')
plt.xlabel('Room Type')

plt.show()
```

![image](https://github.com/user-attachments/assets/17a50918-aff3-4dec-b0c2-e847d0b23355)


## :white_check_mark:  Which are the top 10 neighborhoods with the most listings?
```diff
neighborhood_counts = listings['neighbourhood'].value_counts().head(10)
print("Top 10 Neighborhoods by Listings:")
print(neighborhood_counts)

# Plot neighborhoods with most listings
neighborhood_counts.plot(kind='bar', color='lightcoral')
plt.title('Top 10 Neighborhoods by Listings')
plt.ylabel('Number of Listings')
plt.xlabel('Neighborhood')
plt.xticks(rotation=90)
plt.show()
```
![image](https://github.com/user-attachments/assets/77ace96c-8d3c-40e7-87a1-8609d84ef95c)

## :white_check_mark: Geographical Distribution of Listings (Price Colored)
```diff
import matplotlib.pyplot as plt
import seaborn as sns
```
```diff
plt.figure(figsize=(10, 6))
sns.scatterplot(data=listings, x='longitude', y='latitude', hue='price', palette='viridis', size='price', sizes=(10, 200))
plt.title('Geographical Distribution of Listings (Price Colored)')
plt.xlabel('Longitude')
plt.ylabel('Latitude')
plt.show()
```
![image](https://github.com/user-attachments/assets/8d686df0-7669-42a3-a2c6-f97ff437f41a)

## Let us see the listings on a real map
- Hotter Areas (Red/Yellow):
High Density: The areas that appear in red or yellow (the "hot" colors) indicate higher density or concentration of listings. This means there are more listings in these areas.
Popular Locations: These regions might be more popular or in high demand. It could be near tourist attractions, popular neighborhoods, or central areas in Hawaii where people tend to stay more often.
Colder Areas (Green/Blue):

- Low Density: Areas with blue or green (the "cold" colors) indicate a lower concentration of listings. These regions have fewer listings available.
Less Popular Locations: These areas might be less popular or further from key attractions. If you're looking at pricing or other factors, lower density could imply less competition in these regions, which might indicate more affordable areas or less tourist traffic.
Density Patterns:

- Clustered Areas: If you notice clusters of heatmap intensity, they represent hotspots. These might correspond to high-traffic areas like resorts, beaches, or urban centers.
Spread-Out Listings: If the heatmap shows a more uniform distribution, it could suggest that listings are more evenly spread across the region, which may reflect a more balanced demand for rentals across different areas of Hawaii.
```diff
import folium
from folium.plugins import HeatMap
import pandas as pd


hawaii_data = listings[['latitude', 'longitude', 'price']]  # Example, you may add more columns

# Create a base map centered around Hawaii
m = folium.Map(location=[20.7967, -156.3319], zoom_start=10)

# Prepare the data for the heatmap
heat_data = [[row['latitude'], row['longitude']] for index, row in hawaii_data.iterrows()]

# Add the heatmap to the map
HeatMap(heat_data).add_to(m)

# Save the map as an HTML file to view in a browser
m.save('hawaii_heatmap.html')

# If you're using Jupyter Notebook, you can display the map directly in the notebook:
m
```
![image](https://github.com/user-attachments/assets/54ff150b-aab4-4376-8ec5-6c8d2f13f99c)

![image](https://github.com/user-attachments/assets/1f60f2c1-32f7-4815-bed9-d0b4d4b7438f)


## :rotating_light: How do I find location for my city?
- Type your city name on google maps
- Click on What`s here
![image](https://github.com/user-attachments/assets/d3a64a51-52e1-438c-8999-d85a45220814)
- You will find latitude and longitude at the bottom of screen
![image](https://github.com/user-attachments/assets/bfc3f0a0-22ba-45d3-aa3a-de4e5bae8813)



