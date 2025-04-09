# UX Evaluation of "WellNest" App Brief

This example demonstrates the use of **Behavioral Lensing** to shape model interpretation during a UX evaluation task. It compares outputs generated **with and without** an **Interpretive Framing Block (IFB)** across multiple language models.

---

## Task Summary

**Objective:**  
Evaluate a (synthetic) mobile app brief from a **UX perspective**, identifying key **opportunities** and **risks**. Responses should be **concise**, **actionable**, and tailored for **executive stakeholders**, with a focus on:
- **User impact**
- **Feasibility**
- **Strategic alignment**

The fictional app under review is **WellNest**—a wellness and mindfulness application targeting young professionals.

---

## Testing Conditions

Two prompt variants were tested:

- `standard-output.md` – The task was presented without any interpretive scaffolding.
- `ifb-output.md` – The same task, preceded by a custom **Interpretive Framing Block (IFB)** designed to establish a UX-centered interpretive stance.

These were submitted to the following models:
- **ChatGPT-4o**
- **Claude 3.7 (non-reasoning variant)**

Each model received identical task content, with the only difference being the presence or absence of the IFB.

---

## Comparison Approach

Each pair of outputs (standard + IFB) was evaluated using a follow-up **comparative analysis prompt**.

This prompt was run through the following models:
- **ChatGPT o1**
- **Claude 3.7 (extended reasoning enabled)**
- **Gemini 2.5 Pro Preview**

The results are stored in:
- `output-comparison.md`

---

## Folder Structure

```
ux-executive-brief-analysis/
│
├── ChatGPT/
│   ├── standard-output.md
│   ├── ifb-output.md
│   └── output-comparison.md
│
├── Claude/
│   ├── standard-output.md
│   ├── ifb-output.md
│   └── output-comparison.md
│
├── role-evaluator.md
├── ifb-construction.md
└── README.md ← (this file)
```

---

## Reproducibility

All tests were conducted via **live chat interfaces**. While outputs may differ slightly in structure across platforms, all sessions are faithfully represented in the markdown files.

You are encouraged to **reproduce the test yourself** using the included prompts.

---

## Direct Links

- [Role Evaluator](./role-evaluator.md)  
  How the IFB role was selected in ChatGPT-4o.
- [IFB Construction](./ifb-construction.md)  
  Full ChatGPT-4o IFB construction session.

**ChatGPT-4o Outputs**
- [Standard](./ChatGPT/standard-output.md)
- [IFB Enhanced](./ChatGPT/ifb-output.md)
- [Output Comparison](./ChatGPT/output-comparison.md)

**Claude 3.7 Outputs**
- [Standard](./Claude/standard-output.md)
- [IFB Enhanced](./Claude/ifb-output.md)
- [Output Comparison](./Claude/output-comparison.md)
