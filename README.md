# 📠 Theory of Computation: Monus Function Turing Machine

**Subject:** Theory of Computation (Unit 5: Turing Machines)

---

## 📌 Overview
This project is an interactive, web-based simulator of a **Deterministic Turing Machine (TM)** designed to compute the **Monus Function** (proper subtraction). 

While standard Turing Machine assignments often focus on simple language recognition (e.g., palindromes or strings), this simulator demonstrates a more complex variant from the Unit 5 syllabus: **The Turing Machine as a Computer of Integer Functions.** The application provides a real-time, step-by-step visual representation of state transitions and **Instantaneous Descriptions (IDs)**, proving the computability of proper subtraction using unary arithmetic.

---

## 🧮 The Mathematical Concept
The Monus function, denoted as `m ∸ n`, is defined as:
* `m - n` (if `m ≥ n`)
* `0` (if `m < n`)

Standard subtraction cannot be natively computed on a standard TM tape because TMs do not inherently understand negative numbers. The Monus function solves this and is a foundational concept in recursive function theory.

### Formal Definition (7-Tuple)
The machine is formally defined as `M = (Q, Σ, Γ, δ, q0, q_accept, q_reject)`:

* **Q (States):** `{q0, q1, q2, q3, q4, q5, q_accept, q_reject}`
* **Σ (Input Alphabet):** `{1, -}` (Unary representation)
* **Γ (Tape Alphabet):** `{1, -, _}` (Where `_` represents a blank cell)
* **q0:** The initial state
* **q_accept:** The halting/accepting state
* **δ (Transition Function):** Encoded within the application logic via a state-action mapping matrix.

---

## ⚙️ The Algorithm (Shuttle & Cross-Out)
The simulator processes an input tape formatted as `[m ones] - [n ones]` (e.g., `11111-11` for 5 ∸ 2). The algorithmic logic is as follows:

1. **State q0:** Read the leftmost `1` of integer `m` and overwrite it with a blank (`_`). Move right. (If a `-` is read instead, `m` is empty, meaning `m ≤ n`. Transition to cleanup state `q5`).
2. **States q1, q2:** Shuttle the Read/Write head all the way to the right, crossing the `-` separator, until the end of integer `n` is found.
3. **State q3:** Step left and erase the rightmost `1` of integer `n`. 
    * *Edge Case:* If the head reads the `-` sign instead, integer `n` is completely exhausted. The machine overwrites the `-` with a `1` (restoring the final borrowed integer) and halts in `q_accept`.
4. **State q4:** Shuttle the Read/Write head all the way back to the left until the first blank (`_`) is found. Step right to reset to the start of the string.
5. **Loop:** Return to `q0` and repeat until halting.

---

## 🚀 Features & Simulation Complexity
* **Instantaneous Descriptions (IDs):** The UI strictly adheres to theoretical principles by rendering the exact ID (`X1 ... q Xi ... Xn`) at every step. The active tape cell, current state, and action log update synchronously.
* **Dynamic Infinite Tape:** The underlying JavaScript array dynamically expands with blank symbols (`_`) if the Read/Write head moves beyond the current bounds, perfectly simulating infinite memory.
* **Modern UI/UX:** "Vibe Coded" with a neon-dark aesthetic, featuring manual stepping for academic review and an auto-play feature to watch the computation unfold.

---

## 💻 Local Setup

**To run locally:**
1. Clone this repository.
2. Open `index.html` in any modern web browser (no build tools or dependencies required).
