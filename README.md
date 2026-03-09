# Flight-Ticket-Price-Analysis-
This project analyzes flight ticket pricing trends using Python.  Key analysis includes: - Airline price comparison - Ticket price distribution - Duration vs price relationship - Seasonal travel trends  Tools used: Python, Pandas, NumPy, Matplotlib, Seaborn


# Flight Ticket Price Analysis

# Import libraries
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

# Load dataset
df = pd.read_csv("flight_data.csv")

# Display first 5 rows
print(df.head())

# Dataset information
print(df.info())

# Check missing values
print(df.isnull().sum())

# Data Cleaning
df.dropna(inplace=True)

# Convert date column to datetime
df['Date_of_Journey'] = pd.to_datetime(df['Date_of_Journey'])

# Extract journey day and month
df['Journey_Day'] = df['Date_of_Journey'].dt.day
df['Journey_Month'] = df['Date_of_Journey'].dt.month

# Price distribution
plt.figure(figsize=(8,5))
sns.histplot(df['Price'], bins=30)
plt.title("Flight Ticket Price Distribution")
plt.show()

# Average price by airline
avg_price_airline = df.groupby('Airline')['Price'].mean().sort_values()

plt.figure(figsize=(10,6))
avg_price_airline.plot(kind='bar')
plt.title("Average Ticket Price by Airline")
plt.ylabel("Price")
plt.show()

# Price vs Duration
plt.figure(figsize=(8,5))
sns.scatterplot(x='Duration', y='Price', data=df)
plt.title("Flight Duration vs Ticket Price")
plt.show()

# Top expensive airlines
top_airlines = df.groupby('Airline')['Price'].mean().sort_values(ascending=False)
print(top_airlines.head())

# Save cleaned dataset
df.to_csv("cleaned_flight_data.csv", index=False)

print("Analysis Completed")
