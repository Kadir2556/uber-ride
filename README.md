# Uber Ride Data Analysis using Data Cleaning and Exploratory Data Analysis (EDA)

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

# Load Dataset
df = pd.read_csv("uber.csv")

print("First 5 Records:")
print(df.head())

print("\nDataset Information:")
print(df.info())

# -----------------------------
# Data Cleaning
# -----------------------------

# Remove missing values
df.dropna(inplace=True)

# Remove duplicate rows
df.drop_duplicates(inplace=True)

# Convert pickup_datetime to datetime format
df['pickup_datetime'] = pd.to_datetime(df['pickup_datetime'])

# Remove invalid coordinates
df = df[
    (df['pickup_latitude'].between(-90, 90)) &
    (df['pickup_longitude'].between(-180, 180)) &
    (df['dropoff_latitude'].between(-90, 90)) &
    (df['dropoff_longitude'].between(-180, 180))
]

# Remove invalid fare amounts
df = df[df['fare_amount'] > 0]

print("\nCleaned Dataset Shape:", df.shape)

# -----------------------------
# Feature Engineering
# -----------------------------

df['year'] = df['pickup_datetime'].dt.year
df['month'] = df['pickup_datetime'].dt.month
df['day'] = df['pickup_datetime'].dt.day
df['hour'] = df['pickup_datetime'].dt.hour
df['weekday'] = df['pickup_datetime'].dt.day_name()

# -----------------------------
# Exploratory Data Analysis
# -----------------------------

print("\nStatistical Summary:")
print(df.describe())

print("\nAverage Fare:", round(df['fare_amount'].mean(), 2))
print("Maximum Fare:", df['fare_amount'].max())
print("Minimum Fare:", df['fare_amount'].min())

# Fare Distribution
plt.figure(figsize=(8, 5))
sns.histplot(df['fare_amount'], bins=50, kde=True)
plt.title("Fare Amount Distribution")
plt.xlabel("Fare Amount")
plt.ylabel("Frequency")
plt.show()

# Rides by Hour
plt.figure(figsize=(10, 5))
sns.countplot(x='hour', data=df)
plt.title("Number of Rides by Hour")
plt.xlabel("Hour")
plt.ylabel("Ride Count")
plt.show()

# Rides by Weekday
plt.figure(figsize=(10, 5))
sns.countplot(
    x='weekday',
    data=df,
    order=['Monday', 'Tuesday', 'Wednesday', 'Thursday',
           'Friday', 'Saturday', 'Sunday']
)
plt.title("Number of Rides by Weekday")
plt.xticks(rotation=45)
plt.show()

# Rides by Month
plt.figure(figsize=(10, 5))
sns.countplot(x='month', data=df)
plt.title("Number of Rides by Month")
plt.xlabel("Month")
plt.ylabel("Ride Count")
plt.show()

# Fare vs Passenger Count
plt.figure(figsize=(8, 5))
sns.boxplot(x='passenger_count', y='fare_amount', data=df)
plt.title("Fare Amount vs Passenger Count")
plt.show()

# Correlation Heatmap
numeric_cols = ['fare_amount', 'passenger_count', 'hour', 'day', 'month', 'year']

plt.figure(figsize=(8, 6))
sns.heatmap(df[numeric_cols].corr(), annot=True, cmap='coolwarm')
plt.title("Correlation Heatmap")
plt.show()

# -----------------------------
# Insights
# -----------------------------

print("\nTop 5 Busiest Hours:")
print(df['hour'].value_counts().head())

print("\nTop 5 Busiest Weekdays:")
print(df['weekday'].value_counts().head())

print("\nAverage Fare by Hour:")
print(df.groupby('hour')['fare_amount'].mean())

print("\nEDA Completed Successfully!")
