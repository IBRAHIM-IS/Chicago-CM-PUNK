# Chicago-CM-PUNK
Use Python to analyze a Chicago dataset for time-based patterns like busy days or monthly trends. Convert dates, check for weekends, and visualize trends using pandas and matplotlib to gain insights quickly.
## For the following analysis I have downloaded the data from https://data.insideairbnb.com/united-states/il/chicago/2024-09-17/data/calendar.csv.gz

```diff
import pandas as pd
calendar=pd.read_csv("calendar.csv")
```
```diff
calendar.available.value_counts()
```
```diff
#t = true or available
#f = false or unavailable
```

```diff
availability_percentage = calendar['available'].value_counts(normalize=True) * 100
availability_percentage
```
```diff
busiest_dates = calendar[calendar['available'] == 'f']['date'].value_counts()
print("Busiest Dates:")
print(busiest_dates.head())
```

```diff
import matplotlib.pyplot as plt
availability_percentage.plot(kind='bar', color=['green', 'red'])
plt.title('Availability Percentages')
plt.ylabel('Percentage')
plt.xlabel('Available (t/f)')
plt.show()
```
![image](https://github.com/user-attachments/assets/c0d2a0aa-cf7e-455a-b435-f09423271b3f)

```diff
busiest_dates.head(10).plot(kind='bar', color='orange')
plt.title('Top 10 Busiest Dates')
plt.ylabel('Number of Listings Unavailable')
plt.xlabel('Date')
plt.show()
```
![image](https://github.com/user-attachments/assets/357beeeb-7f55-44ac-bcfe-acf2aa59af97)
```diff
import pandas as pd
listings = pd.read_csv('listings.csv')
```
```diff
listings.columns
```
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
![image](https://github.com/user-attachments/assets/6c887b78-0d02-4175-b009-9f8eec0b8064)
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
![image](https://github.com/user-attachments/assets/34a29c68-c232-4442-9549-75edfefb21ee)
```diff
import matplotlib.pyplot as plt
import seaborn as sns
plt.figure(figsize=(10, 6))
sns.scatterplot(data=listings, x='longitude', y='latitude', hue='price', palette='viridis', size='price', sizes=(10, 200))
plt.title('Geographical Distribution of Listings (Price Colored)')
plt.xlabel('Longitude')
plt.ylabel('Latitude')
plt.show()
```
![image](https://github.com/user-attachments/assets/1f16796f-55a4-4cd9-8abb-2a05b9cfefbd)

```diff
import folium
from folium.plugins import HeatMap
import pandas as pd


hawaii_data = listings[['latitude', 'longitude', 'price']]  # Example, you may add more columns

# Create a base map centered around Hawaii
m = folium.Map(location=[41.86990671281802, -87.62612350327707], zoom_start=10)

# Prepare the data for the heatmap
heat_data = [[row['latitude'], row['longitude']] for index, row in hawaii_data.iterrows()]

# Add the heatmap to the map
HeatMap(heat_data).add_to(m)

# Save the map as an HTML file to view in a browser

# If you're using Jupyter Notebook, you can display the map directly in the notebook:
m
```
```diff
# Plotting the pie chart
plt.figure(figsize=(6, 6))
plt.pie(calendar['available'], labels=calendar['available'], autopct='%1.1f%%', startangle=90, colors=['lightcoral', 'lightskyblue', 'lightgreen'])
plt.title('Availability Distribution')
plt.axis('equal')  # Equal aspect ratio ensures that pie is drawn as a circle.
plt.show()
```
```diff
plt.figure(figsize=(6, 4))
plt.plot(calendar['date'], calendar['available'], marker='o', color='skyblue')
plt.title('Availability Over Time')
plt.xlabel('Date')
plt.ylabel('Availability')
plt.xticks(rotation=45)
plt.grid()
plt.tight_layout()
plt.show()
```
