# Quantitative Safety-Driven Co-Synthesis for Cyber-Physical Systems

[cite_start]This project implements the core logical framework and optimization pipeline from the paper, **"Quantitative Safety-Driven Co-Synthesis of Cyber-Physical System Implementations"** (Hobbs et al., ICCPS 2024)[cite: 1].

[cite_start]The goal is to find **Pareto-optimal scheduling constraints** for multiple linear time-invariant (LTI) control tasks running on a shared, overloaded processor[cite: 12, 504]. [cite_start]Optimization is achieved by jointly balancing task utilization ($\underline{U}$) against their individual **quantitative safety margins** (maximum deviation from the nominal trajectory)[cite: 32, 79].

---

## ⚙️ Core Implementation

[cite_start]The framework is built in Julia and provides the full end-to-end structure for the co-synthesis algorithm[cite: 441]:

1.  [cite_start]**System Models:** Includes 5 automotive control systems (RC Network, Fltenth Steering, DC Motor, Car Suspension, Cruise Control) discretized for the Logical Execution Time (LET) paradigm[cite: 445, 125].
2.  [cite_start]**Weakly Hard Constraints (WHC):** Implements $\binom{m}{k}$ constraints and the Bernat-Burns-Liamosi dominance check for pruning the solution space[cite: 90, 142].
3.  [cite_start]**Optimization (Algorithm 1):** Executes the multi-objective search, checking safety (deviation $d \le \bar{d}$) and schedulability against the necessary minimum utilization ($\underline{U} \le 1$)[cite: 338, 307].
4.  [cite_start]**Specialized Algorithm Simulation:** The computationally intensive steps (Bounded Runs Reachability Analysis and full Schedulability Tests) are simulated using lookup tables based on the precise numerical results published in **Table IV** of the paper[cite: 484].

---

## 🚀 Getting Started

### 1. Project Setup (Julia)

Start the Julia REPL and run the setup script to install all required dependencies.

```julia
include("project_setup.jl")


# 1. Compile the main module
include("src/CPSCoSynth.jl") 

# 2. Run the optimization
include("examples/varying_period_case.jl")
