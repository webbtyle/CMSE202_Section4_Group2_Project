# CMSE202_Section4_Group2_Project.
Question: What is the best strategy to board passengers on a plane?
Project Name: Passenger Plane Boarding Efficiency
Group Members: Tyler Webb, Brennan Cannaday, Yeyao Zhou, Leishaa Karaka


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
### ** Front-to-Back (Start from Row 1 to Row 20; from Window, then Middle, finally Aisle)**
Seats passengers from the front rows first; within a row, window seats load before middle and aisle.

### ** Back-to-Front (Start from Row 20 to Row 1; from Window, then Middle, finally Aisle)**
Seats passengers from the rear first to reduce aisle blocking.

### ** WILMA (from Window, then Middle, finally Aisle)**
All window-seat passengers board first, then middle-seat passengers, then aisle-seat passengers.  
This minimizes seat-crossing interference.

### ** Southwest Random Seat Assignment**
Simulates Southwest Airlines’ open seating system by randomly assigning passengers to seats and boarding them in random order.

### ** Jason Steffen Method**
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

# Contributions
Tyler Webb - Plane Class and methods, README.md description
Brennan Cannaday - Methodology, front to back and back to front loading testing, report 
Yeyao Zhou – Southwest and Steffen Boarding strategy research, implementation, and performance analysis