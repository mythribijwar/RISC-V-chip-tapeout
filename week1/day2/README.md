# Day 4: Gate-Level Simulation (GLS), Verilog Assignment Types, and Synthesis-Simulation Mismatch

Today’s focus is on three core areas of RTL design that directly impact simulation accuracy and synthesis reliability:

- ✅ **Gate-Level Simulation (GLS)**
- ⚠️ **Blocking vs. Non-Blocking Assignments in Verilog**
- 🧩 **Synthesis-Simulation Mismatch**

The session includes conceptual insights and practical labs to reinforce each topic.

---

## Table of Contents

- [1. What is Gate-Level Simulation (GLS)?](#1-what-is-gate-level-simulation-gls)
- [2. Understanding Synthesis-Simulation Mismatches](#2-understanding-synthesis-simulation-mismatches)
  - [2.1 Common Causes](#21-common-causes)
  - [2.2 Missing or Incomplete Sensitivity Lists](#22-missing-or-incomplete-sensitivity-lists)
- [3. Blocking vs. Non-Blocking Assignments in Verilog](#3-blocking-vs-non-blocking-assignments-in-verilog)
  - [3.1 Blocking Assignments (`=`)](#31-blocking-assignments-)
  - [3.2 Non-Blocking Assignments (`<=`)](#32-non-blocking-assignments-)
  - [3.3 Comparison Table](#33-comparison-table)
- [4. Labs](#4-labs)
- [5. Summary](#5-summary)

---

## 1. What is Gate-Level Simulation (GLS)?

**Gate-Level Simulation (GLS)** involves simulating the **post-synthesis netlist** to verify the behavior and timing of your design after it’s been translated into logic gates.

### 🛠 Purpose of GLS

- ✅ Validate that synthesis preserved the design functionality.
- ⏱ Perform timing checks using annotated delays (via SDF files).
- 🔍 Verify scan chains and DFT (Design for Test) logic.

### 🔄 When is GLS Performed?

- **Post-Synthesis**: After RTL is synthesized into a netlist.
- **Pre-Layout**: Before physical design, to catch functional issues early.

### 🧪 Types of GLS

| Type             | Description                                                                 |
|------------------|-----------------------------------------------------------------------------|
| Functional GLS   | Logic-only simulation (zero-delay or unit-delay), no real-world timing.    |
| Timing GLS       | Uses timing annotations to simulate actual delays (SDF back-annotation).    |

---

## 2. Understanding Synthesis-Simulation Mismatches

A **synthesis-simulation mismatch** occurs when the behavior of the RTL simulation doesn't match the behavior of the synthesized netlist (GLS or actual hardware).

### 2.1 Common Causes

- ❌ Use of **non-synthesizable constructs**: `initial`, `#delay`, file I/O, etc.
- 🤷‍♂️ **Ambiguous RTL**: Missing `else` branches, incomplete sensitivity lists.
- 🛠 **Tool interpretation differences**: Synthesis and simulation tools may interpret loosely-written RTL differently.

---

### 2.2 Missing or Incomplete Sensitivity Lists

Incorrect sensitivity lists in combinational `always` blocks can lead to simulation mismatches, even if synthesis behaves correctly.

#### 🧠 Why It Matters

- **Simulation** depends on the sensitivity list to know when to re-evaluate the `always` block.
- If not all input signals are included, the block won’t respond to their changes during simulation.
- This may cause incorrect outputs or behavior that seems like a **latch** or **double-edge-triggered flip-flop**.

#### 🧨 Example: Incomplete Sensitivity List

```verilog
// Incorrect — only 'sel' is in the sensitivity list
always @(sel) begin
  if (sel)
    y = a;
  else
    y = b;
end
```

**Issue**: If `a` or `b` changes while `sel` does not, `y` won’t update — this **can appear** like double-edge-triggered logic during simulation, even though it's not.

#### ✅ Correct Form: Use `@(*)` or full list

```verilog
// Correct — automatically includes all RHS signals
always @(*) begin
  if (sel)
    y = a;
  else
    y = b;
end
```

Or older Verilog:

```verilog
always @(a or b or sel)
```

> ✅ `@(*)` is recommended for combinational logic — ensures correct simulation behavior and avoids mismatches.

---

## 3. Blocking vs. Non-Blocking Assignments in Verilog

Verilog provides two assignment types in procedural blocks: **blocking (`=`)** and **non-blocking (`<=`)**. Using them appropriately is crucial for correct synthesis and simulation behavior.

---

### 3.1 Blocking Assignments (`=`)

- **Used in:** Combinational logic.
- **Execution:** Executes sequentially in the order written.
- **Syntax Example:**

```verilog
always @(*) begin
  a = b & c;
  d = a | e;  // 'a' is already updated when this line runs
end
```

---

### 3.2 Non-Blocking Assignments (`<=`)

- **Used in:** Sequential logic (flip-flops).
- **Execution:** Schedules the update at the **end** of the current time step.
- **Syntax Example:**

```verilog
always @(posedge clk) begin
  q <= d;
end
```

---

### 3.3 Comparison Table

| **Feature**                                | **Blocking (`=`)**                      | **Non-Blocking (`<=`)**                     |
|-------------------------------------------|-----------------------------------------|---------------------------------------------|
| Operator                                   | `=`                                     | `<=`                                         |
| Execution Order                            | Immediate, sequential                   | Deferred, parallel (end of time step)       |
| Suitable for                               | Combinational logic                     | Sequential logic (registers)                |
| Simulation Behavior                        | Executes in code order                  | Updates after time step                     |
| Risk of Race Conditions                    | High in sequential logic                | Low                                          |
| Common Usage                               | Temp/intermediate combinational values  | Clocked processes, flip-flops               |

---

## 4. Labs

✅ You’ll apply today’s concepts in real simulation and synthesis tools:

- Run a gate-level simulation using a netlist and SDF file.
- Analyze a mismatch scenario and fix ambiguous RTL.
- Experiment with blocking vs. non-blocking assignments in lab modules.
- Test sensitivity list mismatches and correct them using `@(*)`.

---

## 5. Summary

| **Topic**                         | **Key Takeaway**                                                                      |
|----------------------------------|----------------------------------------------------------------------------------------|
| Gate-Level Simulation (GLS)      | Simulates post-synthesis logic and timing; validates real-world behavior              |
| Synthesis-Simulation Mismatch    | Caused by non-synthesizable or ambiguous RTL; avoided by disciplined coding practices |
| Blocking vs. Non-Blocking        | Blocking (`=`) for combinational; Non-blocking (`<=`) for sequential logic            |
| Sensitivity Lists                | Use `@(*)` to ensure all dependencies are included in combinational logic             |

Mastering these concepts ensures more reliable, predictable, and hardware-accurate digital designs.
