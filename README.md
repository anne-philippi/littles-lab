# Little's Lab: Flow Line & Buffer Allocation Studio

An interactive web simulator and visual dashboard modeling a 10-machine serial flow line with intermediate decoupling buffers, designed around **Exercise Session 3: Problem 1 (Design and Management of Flow Lines)** at **Universität Mannheim**.

---

## 🏭 Overview

In serial manufacturing systems, deterministic models fall short because stochastic variance triggers two disruptive phenomena:
1. **Blocking-After-Service (BAS)**: An upstream station finishes a part but cannot discharge it because the downstream buffer is full.
2. **Starvation**: A downstream station sits idle because the upstream buffer is empty.

**Little's Lab** allows students and researchers to interactively explore how buffer capacity decouples stations, maximizes expected throughput $E[TH]$, minimizes expected work in process $E[WIP_q]$, and verifies Little's Law ($WIP = TH \times CT$) in real time.

---

## 🚀 Key Features

* **10-Station Animated Factory Canvas**: Live simulation of $M_1 \dots M_{10}$ with 9 intermediate buffers ($B_1 \dots B_9$), tracking real-time station states (Working, Blocked, Starved).
* **Empirical Benchmark Match**: Validated baseline replicating the exact exercise conditions:
  * Effective processing times: $\mu = 1.0\text{ pcs/min}$ (exponentially distributed)
  * Uniform baseline capacity: 5 per buffer (45 total)
  * Target output: $E[TH] \approx 0.764\text{ pcs/min}$, $E[WIP_q] \approx 22.91\text{ workpieces}$
* **Exercise 1 Benchmark Recreation**: Interactive high-resolution chart matching the decreasing buffer inventory curve ($B_1 = 3.48$ down to $B_9 = 1.59$) with theoretical explanations.
* **The +5 Buffer Allocation Experiment**: Interactive comparison testing the optimal **Bowl Phenomenon** against front-loaded and end-loaded allocations.
* **Concept Modals**: In-app educational dialogs for $E[TH]$, $E[WIP_q]$, $CT_q$, BAS Blocking, and Starvation.

---

## 🛠️ Tech Stack

* **Frontend**: HTML5, Canvas API, Tailwind CSS
* **Visualization**: Chart.js
* **Icons**: Lucide Icons
* **Architecture**: Standalone client-side application (zero dependencies, zero build steps)

---

## 📦 Getting Started

Clone the repository and open `index.html` in any web browser:

```bash
git clone [https://github.com/](https://github.com/)<anne-philippi>/littles-lab.git
cd littles-lab
open index.html
