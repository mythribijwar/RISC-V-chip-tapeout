## ⚙️ 1. What Is Static Timing Analysis (STA)?

**STA (Static Timing Analysis)** is the process of verifying that a digital circuit meets its **timing requirements** — without running functional simulations.

It ensures that:
- All signals **arrive on time** (setup check)
- No signals **arrive too early** (hold check)

STA checks every possible **path between flip-flops and I/O pins** to confirm that the design works correctly at the target clock frequency.

---

## 🕒 2. The Two Main STA Checks

| Check Type | Meaning | Timing Goal | Violates When | Path Type | Worst Corner |
|-------------|----------|--------------|----------------|-------------|----------------|
| **Setup Check** | Data must arrive **before** the next clock edge | Path delay ≤ Clock period | Data arrives **too late** | **Maximum delay (slow path)** | **Slow** (ss, low V, high T) |
| **Hold Check** | Data must **not arrive too early** after the same clock edge | Path delay ≥ Hold time | Data arrives **too early** | **Minimum delay (fast path)** | **Fast** (ff, high V, low T) |

### 🧠 Intuition

- **Setup check → “Don’t be late.”**  
  The signal must reach the next register *before* the next clock tick.

- **Hold check → “Don’t be too early.”**  
  The signal must stay stable *for a short time* after the current clock tick.

---

## ⚡ 3. Key STA Terms and Their Meanings

| Term | Description | Simple Meaning |
|------|--------------|----------------|
| **Path Delay** | Time taken for data to travel between flip-flops or from input to output | How long it takes the signal to move |
| **Slack** | Difference between **required time** and **actual arrival time** | “Timing safety margin” |
| **Positive Slack** | Design meets timing | Data is on time or early enough |
| **Negative Slack** | Design fails timing | Data is too late or too early |
| **WNS (Worst Negative Slack)** | The **most negative slack** among all paths | The **worst single path** in the design |
| **TNS (Total Negative Slack)** | The **sum of all negative slacks** | The **total timing failure** across all violating paths |
| **Setup Slack** | Slack value for setup (max delay) checks | “Am I too late?” |
| **Hold Slack** | Slack value for hold (min delay) checks | “Am I too early?” |

---

## 🧩 4. Understanding WNS (Worst Negative Slack)

- **WNS** represents the *most negative* slack value found in the design.
- There are actually **two separate WNS values**:
  - **Setup WNS** → From setup analysis (max delay)
  - **Hold WNS** → From hold analysis (min delay)

### ✅ Important Points

- The STA tool runs both setup and hold analysis internally.
- A single **`report_wns`** usually shows the **most negative** value overall — whether it came from setup or hold.
- Therefore:
  > **WNS = Most negative among the worst setup and worst hold slacks**

Both **setup WNS ≥ 0** and **hold WNS ≥ 0** are required for the design to meet timing.

---

## 🧮 5. Understanding TNS (Total Negative Slack)

- **TNS** is the **sum of all negative slacks** for a particular analysis.
- Like WNS, there are **two separate TNS values**:
  - **Setup TNS** → Total of all negative setup slacks  
  - **Hold TNS** → Total of all negative hold slacks  

### 🧠 Intuition

| Situation | WNS | TNS | Meaning |
|------------|----:|----:|----------|
| Only one path fails | -0.20 | -0.20 | One critical path failing |
| Many paths fail | -0.20 | -15.0 | Many paths have violations |
| All slacks ≥ 0 | 0 | 0 | ✅ Timing clean |

### 💡 Relationship

| Metric | Measures | What It Tells You |
|---------|-----------|-------------------|
| **WNS** | The *worst* violating path | “How bad is the single worst path?” |
| **TNS** | The *sum* of all violations | “How many paths are failing and how badly overall?” |

---

## 🧭 6. PVT Corners and Timing Behavior

**PVT** stands for **Process, Voltage, and Temperature** — the three factors that affect circuit speed.

| Corner Type | Process | Voltage | Temperature | Effect on Delay | Typically Used For |
|--------------|----------|----------|--------------|-----------------|--------------------|
| **SS (Slow-Slow)** | Slow transistors | Low voltage | High or low | Longest delay | **Setup check** |
| **FF (Fast-Fast)** | Fast transistors | High voltage | Low or high | Shortest delay | **Hold check** |
| **TT (Typical-Typical)** | Nominal process | Typical voltage | Room temperature | Reference point | Functional verification |

✅ STA must be run at multiple PVT corners to ensure the design works correctly in **all real-world conditions**.

---

