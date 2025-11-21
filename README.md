# CMSE202_Section4_Group2_Project.
Question: What is the best strategy to board passengers on a plane?
Project Name: Passenger Plane Boarding Efficiency
Group Members: Tyler Webb, Brennan Cannaday, Yeyao Zhou, Leishaa Karaka


# Overview
Our project aims to find the quickest way to board passengers on a plane using various different strategies. The end goal is to analyze the time it takes in seconds for each simulation and compare different methods aka. reverse order, window-middle-aisle, and front to back, to find which one takes the least time to board/sit all passengers.


# Features
Our simulation is of a traditional domestic aircraft layout like a Boeing737 with one aisle down the middle and 3 seats on either side. 

Passengers – Each passenger has a PID (personal ID number), and a row (1–9) and seat label (A–F) assigned. These together determine the exact (row, seat) positions which the simulation will use to move people and determine if a seat is visually seated on or not.

Plane - We build the plane as a full (row x seat) (3-seat) grid with a central aisle, supporting forward movement and sideways movement into the seats plausibly.

Multiple boarding strategies – Supports Southwest open seating, WILMA (Window first, then Middle, Aisle final), Back-to-Front, Front-to-Back, and Jason Steffen’s optimized method.

Step by step visualization – `Plane.run()` shows a simple animated step by step run where we animate moving people down the aisle using the back of a procedure to move passengers.

Fast as hell mode of doing lots of runs at once – `run_no_plot()` lets us evaluate our boarding strategies very quickly without the animation at all hundreds or thousands of runs.

Performance comparison framework to evaluate the boarding strategy selected. `measure_strategy()` runs the simulation repeated times (100-1000) and uses the total boarding time, averaged for the period, for each strategy.

Consistent method of generating the plane passengers that run the sim. `make_passengers()` always produces this same set of flight passengers so that we’re guaranteed to be comparing apples to apples rather than technical changes. 

Modular, extensible design where we can add a new boarding strategy just by creating a new ordering alongside a reordered passenger, i.e. `WILMA()`.


# Running the Code
Currently to run the code copy down the format below with each individual passenger/ticket contained in a list.
```
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
```

To run a visual boarding simulation, first create a plane and generate a full passenger list using `make_passengers()`, then apply any boarding strategy function and load the resulting passenger order into the plane:
```
plane = Plane(num_rows=9)
passengers = make_passengers()

# Example strategy: Steffen method
ordered_passengers = steffen_boarding(passengers)

for p in ordered_passengers:
    plane.add_passenger(p)

plane.run()   # visual animation of the boarding process
```

# Add passengers to the plane
for p in passengers:
    boeing.add_passenger(p)

# Run the simulation
boeing.run()

# To quickly evaluate a strategy without visualization, use the high-speed mode:
```
measure_strategy(steffen_boarding, n=100) # can replace steffen_boarding by any other methods
```

# Contributions
Tyler Webb - Plane Class and methods, README.md description

Yeyao Zhou – Southwest and Steffen Boarding strategy research, implementation, and performance analysis