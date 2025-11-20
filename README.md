# CMSE202_Section4_Group2_Project.
Question: What is the best strategy to board passengers on a plane?
Project Name: Passenger Plane Boarding Efficiency
Group Members: Tyler Webb, Brennan Cannaday, Yeyao Zhou, Leishaa Karaka

# Overview
Our project aims to find the quickest way to board passengers on a plane using various different strategies. The end goal is to analyze the time it takes in seconds for each simulation and compare different methods aka. reverse order, window-middle-aisle, and front to back, to find which one takes the least time to board/sit all passengers.

# Features
Our simulation consists of a traditional domestic aircraft layout like a Boeing737 with one aisle down the middle and 3 seats on either side. 

Passengers - Our passengers are assigned a given arbitrary number as a PID (Personal ID #) as well as a row (#) and seat ('A', 'B', etc.) with their exact seat in a given row being a dictionary key that has a corresponding number value for plotting purposes.

Plane  - The plane consists of a number of different functions assigned under the general Plane class. The plane class takes in the number of rows you want aka. how long the plane is and returns a "board" which is the plotted grid of seats.



# Running the Code
Currently to run the code copy down the format below with each individual passenger/ticket contained in a list.
boeing = Plane(num_rows=9)

passengers = [
    Passenger(1, 3, "A"),
    Passenger(2, 4, "E"),
    Passenger(3, 2, "C"),
    Passenger(4, 5, "B"),
    Passenger(5, 6, "F"),
    Passenger(6, 8, "D"),
    Passenger(7, 6, "E")
]

# Add passengers to the plane
for p in passengers:
    boeing.add_passenger(p)

# Run the simulation
boeing.run()



# Contributions
Tyler Webb - Plane Class and methods, README.md description