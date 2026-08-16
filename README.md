# 🧮 Circuit Analysis Learning Lab

An interactive, beginner-friendly Streamlit web application for undergraduate
Physics and Electronics students learning the key theorems and systematic
methods used to analyse linear circuits.

## 📖 Project Overview

This is a single-file Streamlit application built as a self-contained virtual
learning laboratory — the eighth module in a series alongside Logic Gates,
Electronic Components, Electrical Fundamentals, Measurements & Instruments,
Diodes & Rectifiers, Transistors & Amplifiers, and Digital Electronics. It
builds directly on the Electrical Fundamentals module (Ohm's Law, series/
parallel resistance, basic Kirchhoff's Laws) by covering the more powerful
tools needed for circuits with multiple sources, multiple loops, and
non-series-parallel resistor networks.

It covers 8 circuit elements/sources and 11 theorems/analysis methods, each
with a plain-English explanation and key facts, plus 10 live interactive
calculators and simulators driven by real Python linear algebra and circuit
theory (not hard-coded results) — including a genuine Thevenin/Norton
calculator, a Cramer's-rule nodal analysis solver, and a Delta-Wye
transformation calculator.

No external APIs, AI models, databases, or internet services are used. The
whole app runs locally with just `streamlit`, `pandas`, and `matplotlib`.

## ✨ Features

- **🏠 Introduction** — why special analysis methods are needed, the two
  broad strategies (systematic equations vs. simplification theorems), and
  the crucial linearity requirement.
- **🔎 Circuit Elements & Sources Explorer** — expandable cards for 8
  elements (Ideal/Practical Voltage & Current Sources, Dependent Sources,
  Ground/Reference Node, Wheatstone Bridge, Loaded Voltage Divider), each
  with a real SVG schematic symbol, key property, plain-English explanation,
  applications, and — for 3 of them — a live interactive calculator.
- **📐 Theorems & Analysis Methods** — a filterable Pandas reference table
  of all circuit elements plus expandable cards for 11 theorems/methods:
  KCL, KVL, Nodal Analysis, Mesh Analysis, Thevenin's Theorem, Norton's
  Theorem, Superposition, Maximum Power Transfer, Source Transformation,
  Delta-Wye Transformation, and Millman's Theorem.
- **🎛️ Interactive Simulator** — a central hub with 7 live theorem
  simulators: Thevenin & Norton Equivalents, Maximum Power Transfer (with a
  power-vs-load-resistance plot showing the peak at RL=Rth), Source
  Transformation (bidirectional), Delta-Wye Transformation (bidirectional),
  Superposition Theorem, Millman's Theorem, and a genuine 2-node Nodal
  Analysis solver using Cramer's rule.
- **🔬 Practical Applications** — expandable cards showing these theorems at
  work in audio amplifier design, battery/power supply characterisation,
  antenna matching, precision measurement, circuit simulation software, and
  three-phase power systems.
- **🧪 Troubleshooting Lab** — 5 realistic beginner troubleshooting scenarios
  with multiple-choice questions and immediate, explained feedback.
- **📝 Quiz** — 10 multiple-choice questions (3 options each), scored out of
  100%, with a review of correct/incorrect answers, a progress bar, balloons
  for high scores, and a retake option.
- **Dashboard header** — quick stats shown via `st.metric()` on every page.

## 🎯 Learning Objectives

By the end of this module, a student should be able to:

1. Explain why a source's internal resistance causes real-world "voltage
   sag" under load, and calculate it.
2. Calculate the Thevenin and Norton equivalents of a simple resistive
   network.
3. Apply the Maximum Power Transfer Theorem to find the optimal load
   resistance, and explain why it maximises power (not voltage).
4. Apply Superposition to analyse a circuit with multiple independent
   sources, one at a time.
5. Convert between equivalent voltage-source and current-source
   representations (Source Transformation).
6. Convert between Delta and Wye resistor networks.
7. Set up and solve a simple nodal analysis system, and calculate a
   Wheatstone bridge's balance condition.

## 🧩 Elements & Theorems Covered

**Circuit Elements & Sources:** Ideal Voltage Source, Ideal Current Source,
Practical Voltage Source, Practical Current Source, Dependent (Controlled)
Source, Ground/Reference Node, Wheatstone Bridge, Loaded Voltage Divider.

**Theorems & Analysis Methods:** Kirchhoff's Current Law, Kirchhoff's
Voltage Law, Nodal Analysis, Mesh Analysis, Thevenin's Theorem, Norton's
Theorem, Superposition Theorem, Maximum Power Transfer Theorem, Source
Transformation, Delta-Wye (Δ-Y) Transformation, Millman's Theorem.

## ⚙️ Installation

```bash
pip install -r requirements.txt
```

## ▶️ Running the Application

```bash
streamlit run app.py
```

Then open the local URL Streamlit prints in your terminal (usually
`http://localhost:8501`).

## 🗂️ Project Structure

```
.
├── app.py             # The complete Streamlit application (single file)
├── requirements.txt    # Python dependencies
└── README.md           # This file
```

Inside `app.py`, code is organised into clearly separated sections:

- Page config and custom CSS
- Pure calculation functions (`practical_source_terminal_voltage`,
  `loaded_voltage_divider`, `wheatstone_balance`,
  `thevenin_voltage_divider`, `norton_from_thevenin`,
  `max_power_transfer`, `power_delivered`, `source_transform_v_to_i`/
  `_i_to_v`, `delta_to_wye`/`wye_to_delta`, `superposition_two_sources`,
  `millmans_theorem`, `nodal_2node_solve`, …)
- The `CIRCUIT_ELEMENTS` and `ANALYSIS_METHODS` data dictionaries
- SVG schematic symbol generator (`draw_circuit_element_svg`) — every
  symbol is flattened to a single line of HTML before being injected, so
  Streamlit's Markdown renderer never mis-parses an embedded blank line as
  the end of the HTML block
- Interactive `render_*` functions (one per calculator/simulator), each
  reusable across the Explorer and Simulator pages via a `key_prefix` so
  widget keys never collide, plus an `EXTRA_SIMULATORS` dict for
  theorem-level simulators not tied to a single circuit element
- Quiz and troubleshooting data
- Session-state initialisation
- Sidebar navigation and the top dashboard
- One block per page (Introduction, Circuit Elements & Sources, Theorems &
  Analysis Methods, Simulator, Applications, Troubleshooting, Quiz)

## 🎓 Educational Use

This app is intended for classroom use, self-study, or as a lab companion
in an introductory circuit theory or electrical engineering course, ideally
after the Electrical Fundamentals module — this material assumes Ohm's Law
and basic series/parallel resistance are already familiar.

## 🧪 Testing Notes

Every calculator and simulator in this app was directly executed through a
realistic Streamlit stub during development — including every page, every
individual calculator/simulator, and BOTH branches of every two-option radio
button (e.g. Delta→Wye and Wye→Delta, V→I and I→V source transformation) —
specifically to catch runtime widget-type mismatches and logic errors that a
simple "does it load" check would miss. All physics/math results were also
independently verified (e.g. RL=Rth confirmed as the power-delivery peak,
Delta↔Wye round-trips confirmed symmetric, source transformation confirmed
to round-trip back to the original values).

## 🚀 Future Improvements

- Add a full mesh analysis solver (currently only nodal analysis has a
  dedicated numeric solver).
- Add an interactive circuit diagram where students place components and
  see live Thevenin/Norton reduction.
- Add printable/exportable student progress reports.
- Cross-link directly into the Electrical Fundamentals module's Kirchhoff's
  Laws simulator.
