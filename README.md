import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from datetime import date
import os
FILE = "screen_time.csv"
if not os.path.exists(FILE):
    df = pd.DataFrame(columns=["Date", "Hours"])
    df.to_csv(FILE, index=False)
def add_screen_time():
    hours = float(input("Enter screen time in hours: "))
    today = date.today()
    df = pd.read_csv(FILE)
    new_data = pd.DataFrame([[today, hours]], columns=["Date", "Hours"])
    df = pd.concat([df, new_data], ignore_index=True)
    df.to_csv(FILE, index=False)
    print("Screen time recorded!")
def analyze_screen_time():
    df = pd.read_csv(FILE)
    total = np.sum(df["Hours"])
    average = np.mean(df["Hours"])
    maximum = np.max(df["Hours"])
    print(f"Total Screen Time: {total} hours")
    print(f"Average per Day: {average:.2f} hours")
    print(f"Maximum in a Day: {maximum} hours")
def visualize_screen_time():
    df = pd.read_csv(FILE)
    plt.figure()
    plt.plot(df["Date"], df["Hours"], marker='o')
    plt.title("Daily Screen Time Usage")
    plt.xlabel("Date")
    plt.ylabel("Hours")
    plt.xticks(rotation=45)
    plt.tight_layout()
    plt.show()
while True:
    print("\n1. Add Screen Time")
    print("2. Analyze Screen Time")
    print("3. Visualize Screen Time")
    print("4. Exit")
    choice = input("Enter choice: ")
    if choice == "1":
        add_screen_time()
    elif choice == "2":
        analyze_screen_time()
    elif choice == "3":
        visualize_screen_time()
    elif choice == "4":
        print("Goodbye! Reduce screen time 😊")
        break
    else:
        print("Invalid choice")
