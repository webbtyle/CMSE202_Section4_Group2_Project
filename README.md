# CMSE202_Section4_Group2_Project.
## Question: What is the best strategy to board passengers on a plane?
### Project Name: Passenger Plane Boarding Efficiency
### Group Members: Tyler Webb, Brennan Cannaday, Yeyao Zhou, Leishaa Karaka


---
# Overview
This project studied airplane boarding efficiency by simulating each of the strategies for how passengers board, and recording how long.completing boarding by each strategy took. A discrete‐step simulation was used to model walking, blocking of aisles, aisle congestion,and delay due to overhead luggage. Used & compared many methodologies - Front-to-Back, Back-to-Front, WILMA, Southwest Open Seating, and the Jason Steffen Method. Multiple runs done to arrive upon which boarding sequence seemed optimal, and which takes least amount of total boarding time.

---
# Aircraft & Simulation Features
### **Aircraft Layout**
- There are **20 rows** of seating.
- Each row has a **3–aisle–3 layout** (A B C | aisle | D E F)
- Rows 1–5 represent First/Business Class seating.
- Rows 6–20 are Economy Class.
- Each passenger or aisle takes up a “space” in the simulation grid

### **Passenger model**
Each passenger has:
- **PID** (personal ID number)
- **Assigned row (1–20)**
- **Seat (A–F)**
- **Carry-on luggage status** (subjectively randomly assigned )
- **Overhead luggage delay** (randomized instead to have an additional delay of 9–12 seconds) when chosen, you are in control of the plane now make bumpy noises
- **Movement rules:** can move *forward*, *left*, or *right*, but **never backwards**

### **Plane simulation**
- `make_passengers()` produces the entire list ready to go - for this aircraft,
20 x 6 (seats) = 120 total
- `step()` moves people through the aisle, addressing blocked and congestion issues.
- `run()` handles running the entire process animating the entire thing (slow, visual).
- `run_no_plot()` takes you through only the logic i.e. no animation (actually a lot faster). We assume 1 simulation timestep = 1.5 second real time of boarding time!

---
# Boarding Strategies Implemented
### **Front-to-Back (Start from Row 1 to Row 20; from Window, then Middle, finally Aisle)**
Seats passengers from the front rows first; within a row, window seats load before middle and aisle.

### **Back-to-Front (Start from Row 20 to Row 1; from Window, then Middle, finally Aisle)**
Seats passengers from the rear first to reduce aisle blocking.

### **WILMA (from Window, then Middle, finally Aisle)**
All window-seat passengers board first, then middle-seat passengers, then aisle-seat passengers.  
This minimizes seat-crossing interference.

### **Southwest Random Seat Assignment**
Simulates Southwest Airlines’ open seating system by randomly assigning passengers to seats and boarding them in random order.

### **Jason Steffen Method**
Based on physics research on optimal boarding:
- from Window, then Middle, finally Aisle
- Odd rows before even rows
- Back-to-front sorting within each category  
Designed to minimize aisle congestion and baggage interference.

---
# Performance Evaluation Framework
### **`measure_strategy()`**
Runs any boarding strategy **100–1000 times** using:  
- Fast simulation (`run_no_plot`)
- Fixed set of base passengers for fairness
- Averaged total boarding time (in seconds)

### Example:
```
measure_strategy(steffen_boarding, n=1000)
```

# Running the Simulation
### Visual Simulation (slow, animated)
To run a visual boarding simulation, first create a plane and generate a full passenger list using `make_passengers()`, then apply any boarding strategy function and load the resulting passenger order into the plane:
```
plane = Plane(num_rows=20)
passengers = plane.make_passengers()

ordered_passengers = steffen_boarding(passengers)

for p in ordered_passengers:
    plane.add_passenger(p)

plane.run()   # visualize animation of the boarding processn
```

### High-Speed Simulation (fast, no graphics)
```
measure_strategy(wilma_boarding, n=100)  
```

### Southwest Example
```
sw_passengers = southwest_random_seat_assignment(20)
plane = Plane(20)

for p in sw_passengers:
    plane.add_passenger(p)

plane.run()
```
---
### Scaling the Simulation to Different Aircraft Sizes

One of the strengths of our boarding model is that it can easily be adapted to represent airplanes of different sizes. The simulation is controlled primarily by the num_rows parameter in the Plane class. By adjusting this parameter, the model automatically recalculates the number of passengers, seat positions, aisle length, and all movement logic.

1. **Changing the Number of Rows**

To run the simulation on a larger or smaller aircraft, simply modify the num_rows argument when creating the Plane object:

```
plane = Plane(num_rows=30)   # Example: 30-row aircraft
passengers = plane.make_passengers()
```
This automatically updates:
- Total number of rows
- Seat count (6 seats per row: A–F)
- Total passengers (rows × 6)
- Aisle length and walking behavior

2. **Running Boarding Strategies on Any Plane Size**

All of our boarding strategies (Front-to-Back, Back-to-Front, WILMA, Southwest, and Steffen) scale automatically because each strategy sorts passengers based on their row and seat values. For example, WILMA on a 45-row aircraft:
```
plane = Plane(45)
passengers = plane.make_passengers()

ordered = wilma_boarding(passengers)

for p in ordered:
    plane.add_passenger(p)

plane.run()
```
3. **Fast Simulations for Larger Aircraft**

High-speed evaluations can also be scaled by passing the row count into measure_strategy():
```
measure_strategy(wilma_boarding, n=100, num_rows=45)
```
This allows quick comparison of boarding times for different plane sizes without running animations.

--- 

# Contributions
Tyler Webb - Plane Class and initial methods (Yeyao redid the step function, and Brennan added time to the run), README.md description, Model Idea, Simulation Setup, and Difficulties and Limitations in the final presentation.

Brennan Cannaday - Methodology, front to back and back to front loading testing and sim functions, report, bar chart visualization

Yeyao Zhou – Southwest and Steffen Boarding strategy research, implementation, and performance analysis

Leishaa Karaka - WilMA method, seat randomizer, strategy results explanation, analysis and conclusion, README.md section on scaling the simulation to different aircraft sizes, added code descriptions/documentation, report writing, and final presentation outline and slide bullet points.
