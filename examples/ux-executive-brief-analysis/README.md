# UX Executive Brief Analysis: WellNest App
## *Comparing Standard Prompts vs. Behavioral Lensing for Strategic Insight*

This example explores the application of **Behavioral Lensing** to enhance the quality and relevance of outputs for a specific, high-stakes task: evaluating a product brief from a User Experience (UX) perspective for executive stakeholders. It demonstrates how shaping the model's interpretation *before* processing the task can lead to more focused, actionable, and strategically aligned insights compared to standard prompting methods.

## The Challenge & Goal

The objective was to evaluate a synthetic mobile app brief ("WellNest," a wellness app for young professionals) from a critical UX standpoint. The desired output wasn't just a generic summary, but a concise, actionable analysis identifying key **opportunities** and **risks**, tailored for an **executive audience**. This requires focusing sharply on:

*   User impact
*   Feasibility concerns
*   Strategic alignment

Achieving this level of targeted analysis often requires more than straightforward instructions; it demands nuanced interpretation, a common challenge for standard LLM prompting.

## Methodology: Standard vs. Interpretive Framing

To assess the impact of Behavioral Lensing, two distinct approaches were compared using identical task inputs:

1.  **Standard Prompting:** The evaluation task was presented directly to the LLMs without specific interpretive guidance.
2.  **Behavioral Lensing (IFB):** The same task was presented, but preceded by a custom **Interpretive Framing Block (IFB)**. This IFB was designed to prime the model with a UX-centric interpretive stance, focusing its "attention" on the core evaluation criteria relevant to the task.

These two approaches were tested across the following generation models:

*   **ChatGPT-4o**
*   **Claude 3.7**

The effectiveness of each approach was then assessed via a follow-up **comparative analysis prompt** submitted to capable evaluation models:

*   **ChatGPT-o1**
*   **Claude 3.7** (with extended reasoning enabled)
*   **Gemini 2.5 Pro Preview**

The detailed results of these comparisons, examining differences in strategic focus, actionability, and alignment, can be found in the `output-comparison.md` files.

## Explore the Data

The outputs and comparisons are organized by model. Supporting files detail the IFB construction process.

**Supporting Files:**

*   [IFB Role Selection (ChatGPT-4o)](./role-evaluator.md)
*   [IFB Construction Session (ChatGPT-4o)](./ifb-construction.md)

**ChatGPT-4o Results:**

*   [Standard Output](./ChatGPT/standard-output.md)
*   [IFB Enhanced Output](./ChatGPT/ifb-output.md)
*   [Output Comparison](./ChatGPT/output-comparison.md)

**Claude 3.7 Results:**

*   [Standard Output](./Claude/standard-output.md)
*   [IFB Enhanced Output](./Claude/ifb-output.md)
*   [Output Comparison](./Claude/output-comparison.md)

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

## Reproducibility Note

Tests were conducted via live chat interfaces. While minor formatting variations might occur if reproduced, the content represents the sessions accurately. You are encouraged to reproduce the test yourself using the included prompts and IFB details.
