# Little's Lab: Flow Line & Buffer Studio

An interactive discrete-event simulator and pedagogical decision-support tool designed for Operations Management coursework at the **University of Mannheim**.

The application models stochastic serial flow production lines, visualizes the mechanics of **Blocking-After-Service (BAS)** and **Starvation**, demonstrates **Little's Law**, and benchmarks optimal buffer distribution profiles against the **Bowl Phenomenon**

Live Demo: [littles-lab.vercel.app](https://littles-lab.vercel.app/)

---

## 🏭 Core Operations Management Concepts Modeled

1. **Serial Flow Line Dynamics**:
   * Simulates a $10$-machine line with $9$ intermediate decoupling buffers ($M_1 \to B_1 \to M_2 \dots B_9 \to M_{10}$).
   * Baseline targets: $E[TH] \approx 0.764 \text{ pcs/min}$ and $E[WIP_q] \approx 22.91 \text{ workpieces}$ under uniform capacity ($C_i = 5$).
2. **BAS (Blocking-After-Service)**:
   * When machine $M_i$ completes processing but buffer $B_i$ is at full capacity ($B_i = C_i$), $M_i$ freezes in a blocked state, unable to release the item or start the next job. Blocking waves propagate upstream.
3. **Starvation**:
   * When machine $M_i$ is idle but preceding buffer $B_{i-1} = 0$, $M_i$ is starved of workpieces. Station $M_1$ is never starved (infinite raw material supply), whereas $M_{10}$ suffers cascading downstream starvation waves.
4. **The Bowl Phenomenon & Buffer Allocation**:
   * Evaluates strategic allocation of additional buffer storage ($+5$ units, $C_{\text{total}} = 50$).
   * Demonstrates that allocating decoupling capacity symmetrically toward the center of the line ($B_4, B_5, B_6$) maximizes marginal throughput while dampening two-way blocking and starvation shockwaves.
5. **Little's Law Validation**:
   * Dynamically evaluates queue cycle time:
     $$CT_q = \frac{E[WIP_q]}{E[TH]}$$

---

## ✨ Features & Architecture

* **Stochastic Monte Carlo Engine**: Processing times are continuously sampled via inverse transform sampling:
  $$T = -\frac{\ln(1 - U)}{\mu}$$
  with rate $\mu = 1.0$ ($c_e = 1.0$).
* **Real-Time Canvas Telemetry**: Central conveyor track with color-coded status badges for each station:
  * 🟢 **Working**
  * 🔴 **Blocked** (downstream buffer full)
  * 🟠 **Starved** (upstream buffer empty)
* **Instant Steady-State Fast-Forward**: A dedicated computational bypass running $15{,}000$ sub-steps instantaneously to skip the transient warm-up phase and converge directly to asymptotic steady-state metrics.
* **Dynamic Adaptive Chart Scaling**: Live telemetry bar chart with auto-scaling y-axes that adapt when custom buffer capacities exceed standard limits ($C_i > 7$).
* **Course Benchmark Reference**: Direct reference reproduction of Exercise Session 3 (Problem 1) including analytical proofs, distribution graphs, and rules of thumb (MTTF, MTTR, bottleneck isolation).
* **Strategy Comparison Table**: Multi-scenario evaluation showing marginal decoupling efficiency:
  $$\frac{\Delta E[TH]}{\Delta E[WIP_q]}$$
* **Mannheim Branding**: Schloss Navy (`#001A3F`) and Academic Cyan (`#008AC9`) design hierarchy.
* **Zero Dependencies**: Pure, standalone vanilla HTML5/JavaScript, Tailwind CSS (CDN), Chart.js, and Lucide icons.

---

## 🚀 Local Deployment

Since Little's Lab is a single-file application, no build steps or package managers (`npm`/`yarn`) are required:

1. Clone the repository:
   ```bash
   git clone [https://github.com/anne-philippi/littles-lab.git](https://github.com/anne-philippi/littles-lab.git)
   cd littles-lab
