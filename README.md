# Airline Planning Optimization: Managing Flight Disruptions ✈️🌩️

## 📖 Project Overview
Weather events are a major threat to the airline industry. When a snowstorm or heavy rain hits, airports cannot operate at full capacity, leading to unavoidable flight cancellations and aircraft re-routing. 

This project tackles the complex decision-making process during such disruptions: **Which flights should be operated, which should be cancelled, and how should aircraft be re-routed to minimize the total revenue lost?**

This repository is the result of a step-by-step learning journey, initially inspired by the [Gurobi Aviation Planning Case Study](https://colab.research.google.com/github/Gurobi/modeling-examples/blob/master/aviation_planning/airlineplanning.ipynb#scrollTo=706f85d8), but ultimately rebuilt using **Google OR-Tools** to solve the full-scale problem without commercial license restrictions.

## 📊 The Dataset
The project uses real-world flight data in France (from the ROADEF 2009 Challenge), which includes:
- **35 Airports**
- **608 Flights**
- **85 Aircraft**

## 🚀 My Learning Journey (The 3 Phases)

This project was developed in three distinct phases as part of my learning process in Operations Research and Mathematical Optimization:

### Phase 1: Data Parsing & Network Visualization
- **Goal:** Understand the raw data and how an airline network operates.
- **Actions:** Imported flight rotations, starting/ending positions of aircraft, and passenger itineraries using `pandas`. Built Flight-to-Flight transitions to map out all feasible next-flights for each aircraft.
- **Outcome:** Successfully modeled the aircraft routes as a Directed Acyclic Graph (DAG) and visualized the network using `networkx` and `pygraphviz`.

### Phase 2: Understanding the Optimization Logic (Gurobi)
- **Goal:** Grasp the mathematical modeling behind the decision-making process.
- **Actions:** Studied the Gurobi sample code to deeply understand:
  - **Decision Variables:** $x_{a,f}$ (whether aircraft $a$ operates flight $f$) and $y_{a,f_1,f_2}$ (routing sequence).
  - **Objective Function:** Minimizing the total revenue lost from cancelled flights.
  - **Constraints:** Flow-balance constraints (ensuring continuous flight paths from source to sink), flight traversal logic, and airport capacity limits based on the disruption level ($\alpha$).

### Phase 3: Scaling Up with Google OR-Tools (Pywraplp)
- **Goal:** Overcome the Gurobi free-license limitations (which restricts the number of variables/constraints) to solve the entire dataset.
- **Actions:** Translated the entire mathematical model from Gurobi's syntax to **Google OR-Tools (`pywraplp`)** using the **SCIP** solver backend.
- **Outcome:** Successfully solved the complete dataset (35 airports, 608 flights, 85 aircraft). I also implemented an interactive `ipywidgets` slider that allows users to dynamically adjust the disruption level ($\alpha$) from 0 (complete shutdown) to 1 (business as usual) and instantly observe the optimization results.

## 🛠️ Technologies Used
- **Python** 
- **Google OR-Tools (`pywraplp` / SCIP)**: For linear and integer programming optimization.
- **Pandas**: For data manipulation and preprocessing.
- **NetworkX & Matplotlib / PyGraphviz**: For analyzing and visualizing the flight network.
- **ipywidgets**: For building the interactive disruption slider.

## 💻 How to Run
The code is best executed in a Jupyter Notebook environment like Google Colab.

1. Clone the repository.
2. Upload the `airlineplanning.ipynb` notebook to Google Colab.
3. Run the cells sequentially. 
4. At the bottom of the notebook, interact with the **Alpha Slider** to set the disruption capacity (e.g., 0.5 means airports operate at 50% capacity) and watch the OR-Tools solver calculate the optimal flight network and financial loss in real-time.

## 📜 Acknowledgements
- Data and original mathematical model structure adapted from the [Gurobi Optimization Examples](https://github.com/Gurobi/modeling-examples).
