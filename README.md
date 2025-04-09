# Behavioral Lensing

*Framing Model Behavior Through Interpretive Control*

## Project Status & Contributions

Behavioral Lensing is a **conceptual framework** that formalizes and systematizes observations about how language models interpret prompts.

The framework is currently under active development and curation. While formal contributions—such as Pull Requests—are not being accepted at this time, community engagement is welcome in the following ways:

- **Discussions**: Share your experiences, ask questions, and discuss implementations.
- **Issues**: Report specific limitations, or suggest improvements.
- **Experiments**: Share the results of your testing.

**Decision Process**: As the framework's author and maintainer, I make final decisions on its direction and implementation. I review all feedback and incorporate insights that align with the core vision.

*The contribution model will likely evolve as the framework matures. Star the repository to stay informed about changes to this policy.*

---

## Table of Contents

- [Overview](#overview)
- [The Problem Hidden in Plain Sight](#the-problem-hidden-in-plain-sight)
- [Symptoms of Misaligned Framing](#symptoms-of-misaligned-framing)
- [A Different Perspective](#a-different-perspective)
- [Summary of the Problem](#summary-of-the-problem)
- [Why This Matters](#why-this-matters)
- [Behavioral Lensing: The Definition](#behavioral-lensing-the-definition)
- [Core Components](#core-components)
  - [Interpretive Framing Block (IFB)](#interpretive-framing-block-ifb)
  - [Symbolic Anchors (SA)](#symbolic-anchors-sa)
  - [Task Reflection (TR)](#task-reflection-tr)
  - [Reasoning Path (RP)](#reasoning-path-rp)
  - [Clarifying Scope and Intent](#clarifying-scope-and-intent)
- [What This Enables](#what-this-enables)
- [Rethinking Existing Techniques Through a Behavioral Lens](#rethinking-existing-techniques-through-a-behavioral-lens)
  - [Chain-of-Thought (CoT)](#chain-of-thought-cot)
  - [Role Prompting](#role-prompting)
  - [Few-Shot Prompting](#few-shot-prompting)
  - [Instruction Tuning](#instruction-tuning)
  - [Self-Consistency Sampling](#self-consistency-sampling)
  - [Rewriting for Clarity](#rewriting-for-clarity)
- [When to Use It](#when-to-use-it)
- [Limitations & Failure Modes](#limitations--failure-modes)
- [Future Directions](#future-directions)
- [Try It Yourself](#try-it-yourself)
- [Glossary of Key Terms](#glossary-of-key-terms)
- [Summary](#summary)
- [The Shape of Invisible Control](#the-shape-of-invisible-control)
- [License (CC BY 4.0)](#license)

# Overview

Language models don't just follow instructions—they interpret them through an invisible frame. Behavioral Lensing provides a systematic approach for shaping how models understand and process tasks by controlling their interpretive stance. This framework enables more consistent, appropriate, and effective model behavior across diverse contexts and architectures.

> **Before you instruct a model, you shape what kind of model it thinks it should be.**  
>
> In language models, behavior is not just governed by what you ask—but by *how the model frames the asking*.  
>
> **Behavioral Lensing** is the intentional modulation of a model's interpretive posture. It is not a trick, nor a roleplay—it's a comprehensive strategy for directing the model’s generative trajectory.

These ideas are for anyone working with or building on top of language models—prompt engineers, toolmakers, researchers, educators, and anyone seeking more reliable, aligned, and intentional model behavior.

## The Problem Hidden in Plain Sight

Language models appear to follow instructions.  
But **they don't begin with instructions**—they begin with **assumptions**.

Every prompt is processed through a **transient interpretive frame**—a fleeting worldview shaped by roles, tone, symbols, and structural cues. This frame is the perspective through which the model perceives its task, and it governs everything downstream: tone, strategy, reasoning pattern, even what the model believes success looks like.

And this leads to a silent problem:

> **Most prompting issues aren't caused by poor instructions.**  
> They're caused by **unacknowledged framing.**

**Note on Terminology:** “Worldview” ≠ Identity or Belief.

To clarify the terms used throughout this document:
- A **lens** refers to any prompt element or structure that influences interpretation.  
- An **interpretive frame** is the internal context the model constructs from that lens—its momentary worldview.  
- “**Worldview**” is used informally to describe this transient stance, including values, tone, and task orientation.  

These are not fixed beliefs or traits, but **contextual scaffolds**—temporary structures that shape behavior *at the moment of prediction*.

This framing can be *productively leveraged*, but should not be mistaken for cognition or self-awareness.

### Symptoms of Misaligned Framing
These patterns reflect a deeper issue—**interpretive drift**—summarized below:

- The model completes the task *correctly*—but from the wrong interpretive frame (e.g., an executive analysis that lacks business focus).
- Tone, epistemic stance, or reasoning patterns shift mid-response without clear cause.
- Chain-of-thought prompts work inconsistently, especially across models or domains.
- Role prompting ("You are a doctor") gives wildly different results depending on wording—even with the same instructions.
- You optimize a prompt endlessly, only to find another model interprets it completely differently.

### A Different Perspective

Current prompt engineering focuses on:
- Better task phrasing.
- More examples.
- Clearer instructions.

But these treat *surface syntax*, not **interpretive structure**.

Meanwhile, alignment research treats "behavior shaping" as a training problem—something to fix with more data, more fine-tuning, or hard-coded rules.

What's missing is a toolkit for shaping the model’s **interpretive posture**—directly in context, before generation begins—using the very mechanism that powers the model: *language*.

*That's what Behavioral Lensing is for.*

### Summary of the Problem

| Problem                              | Traditional View                  | Behavioral Lensing View           |
|--------------------------------------|-----------------------------------|-----------------------------------|
| Prompt misfires                      | Poor phrasing                     | Misaligned interpretive frame      |
| CoT inconsistency                    | Weak examples or structure        | No reasoning stance was framed    |
| Role-prompt instability              | Underfitting or randomness        | Missing symbolic or value cues    |
| Cross-model behavior divergence      | "Model difference"                | Interpretive drift due to missing framing scaffold |
| Alignment failures in open-ended tasks | Bad instructions                  | Wrong *worldview* behind response |

> Behavioral Lensing isn’t about controlling the model’s response. It’s about controlling the lens through which the task is first understood.

Once that layer becomes visible, it becomes steerable.

## Why This Matters

Most prompting advice focuses on **what to say** to a model—better instructions, better examples, better phrasing.

But language models don’t just process content—they interpret it. Every prompt is filtered through a **transient worldview**, inferred from roles, tone, symbols, and structure. That frame shapes the entire prediction trajectory.

> **All prompting already shapes model behavior—Behavioral Lensing just makes that shaping intentional.**  
> It’s not a trick, a persona, or a one-off technique. It’s a shift in mindset: every prompt is a frame, and every frame conditions how the model behaves.

The difference is awareness. Instead of writing commands, you’re designing **interpretive conditions**. Instead of hoping the model gets it “right,” you're building **structures that shape what right looks like** from the start.

This approach gives you leverage that’s otherwise invisible:  
- Clearer reasoning.
- More consistent tone and stance.
- Stronger alignment with task intent.
- Better cross-model reproducibility.

Behavioral Lensing doesn’t constrain creativity—it scaffolds it. By making the interpretive layer visible, it becomes steerable.

## Behavioral Lensing: The Definition

**Behavioral Lensing** is a structured method of shaping an LLM's output by modifying the **interpretive conditions** under which it generates responses.

It operates on a simple principle:  
> **Models do not generate responses from a blank state. They generate from within a frame.**

By constructing that frame deliberately—through role, values, symbols, or epistemic stance—we **lens** the model's interpretive process. This does not change the model's architecture; it *changes the slope of its prediction path*.

## Core Components

While Behavioral Lensing is a broad framework for interpretive control, its most immediately actionable layer is built from four core components. These elements help shape **how** a language model interprets, understands, and reasons through a task:

- **Interpretive Framing Block (IFB)** – establishes the model’s initial stance.
- **Symbolic Anchors (SA)** – reinforce key values, tones, or priorities, often embedded within the IFB.  
- **Task Reflection (TR)** – surfaces the model’s current interpretive state.  
- **Reasoning Path (RP)** – guides the model’s thinking strategy during execution.

These components are **modular and composable**. They can be used independently, but they work best when layered—each one reinforcing and grounding the others. Symbolic Anchors often shape the tone and value orientation of the IFB, while Task Reflection and Reasoning Paths operate further downstream, steering processing and output behaviors.

They don't define the whole of Behavioral Lensing—but they provide a concrete entry point. Used together, they give you leverage not just over *what* the model says, but *how* it arrives there.

### Interpretive Framing Block (IFB)
An expressive preamble that gives the model an interpretive **stance**—a sense of who it is, what it values, and how it approaches the world.

> An IFB doesn’t define a persona. It establishes a **contextual posture**—a scaffold that shapes how the model frames the task ahead.

By presenting the model with a coherent worldview, the IFB **primes its latent posture**—nudging the internal dynamics that influence how it predicts tokens. This shaping happens **before any direct instructions are given**, curving the generation space so that task instructions land in an already-aligned interpretive slope.

**Example – UX Design Context:**

```text
Years of designing experiences have shown me that meaningful UX lives at the intersection of empathy, context, and constraint. I approach design not just as a craft, but as a conversation—between systems, users, and the invisible assumptions we embed in every interaction. With experience comes the clarity to recognize what truly matters, and the humility to listen first. I believe in solutions that are both elegant and earned—grounded in user realities, but reaching toward what's possible. For me, the best design is quietly transformative: it works, it fits, and it leaves people feeling understood.
```

**Purpose:**  
The IFB sets the **interpretive foundation**. It activates behavioral priors that influence what the model sees as relevant, natural, or appropriate—**guiding token prediction in a direction already useful to the task**. It doesn’t replace instructions. It aligns the model’s initial interpretive state so that those instructions are processed as intended.

### Symbolic Anchors (SA)
Key terms or phrases that **activate specific latent associations** in the model—biasing tone, priorities, or reasoning style without requiring explicit instruction.

> Symbolic Anchors are not directives. They shape how the model **interprets context** by reinforcing certain conceptual or behavioral patterns.

**Examples:**
- Action cues: “optimize”, “repair”, “investigate”, “streamline”  
- Value frames: “equitable”, “efficient”, “sustainable”, “sacred”  
- Identity markers: “mentor”, “strategist”, “hacker”, “archivist”

**Purpose:**  
Symbolic Anchors help align the model’s **interpretive substrate** with the intended worldview or mode of reasoning. By surfacing key signals early, they reduce ambiguity and steer the model’s internal representation space toward relevant clusters.

### Task Reflection (TR)
A brief, structured prompt that asks the model to **describe its current understanding** of the task, role, and intended strategy—**before** generating a final output.

> Task Reflection doesn’t evaluate performance. It exposes how the model is currently interpreting the situation—making internal assumptions visible and debuggable.

**Example Prompt:**

```text
Summarize your current understanding of the task, the role you are inhabiting, and the approach you intend to use.
```

**Purpose:**  
Task Reflection is a lightweight diagnostic and alignment tool:
- Surfaces the model’s active interpretive frame.
- Detects misalignment before task execution.
- Provides visibility into internal reasoning posture.

When used strategically, Task Reflection can also improve outcomes. By prompting the model to articulate its stance early, it **constrains the generation path** in useful ways—leveraging autoregressive mechanics to reduce drift and reinforce coherence throughout the response.

### Reasoning Path (RP)
The structure and style of instructions that guide the model’s **mode of reasoning**—based on the interpretive stance already established.

> Reasoning Paths are most effective when they **extend naturally from the Interpretive Framing Block**, reinforcing the model’s posture rather than competing with it.

**Examples of Reasoning Paths:**
- *Step-by-step analysis*:  
  “Break this down into clear stages and explain each one.”  
- *Comparative reasoning*:  
  “Compare the pros and cons of these two options.”  
- *Risk assessment*:  
  “Identify potential pitfalls and how to mitigate them.”  
- *Causal explanation*:  
  “Explain why this outcome is likely based on the input.”  
- *Iterative refinement*:  
  “Propose a draft, then suggest how to improve it.”  
- *Goal-oriented planning*:  
  “Outline the steps needed to achieve this result.”

**Purpose:**  
The Reasoning Path is the **operational layer** of prompting—task instructions, decision-making strategies, and output scaffolding—but its effectiveness depends on alignment with the model’s interpretive state. When reasoning instructions are congruent with the worldview established in the IFB, the model is more likely to follow the intended logic with consistency and depth.

**Integration:**  
In practice, most structured prompts already include some form of Reasoning Path, whether it’s asking for step-by-step thinking, a comparison, or a risk assessment. This component doesn’t require you to change your workflow, it makes what you're already doing **intentional**. The key is to ensure that your reasoning style aligns with the interpretive frame established earlier, so the model’s thinking path matches the worldview it’s operating within.

### Clarifying Scope and Intent

Before moving into applications, it’s worth clarifying what Behavioral Lensing is—and what it is not. While some components may resemble familiar prompting techniques, the purpose, structure, and function of this framework are distinct.

> Behavioral Lensing is not a style layer or persona builder. It’s a system for shaping how language models frame tasks—so that generation begins with the right interpretive posture.

**This is not:**

- **Persona construction**  
  Lensing does not simulate personalities or fictional agents. The goal is not to create characters, but to shape how a model frames the task it's given.

- **Voice or tone mimicry**  
  While lenses may affect language or style, the focus is not on aesthetics. Lensing is concerned with interpretive posture, not surface-level fluency.

- **Prompting shortcuts or exploits**  
  This is not about clever phrasing, jailbreaks, or optimization hacks. It is designed for task alignment, not circumvention.

- **A theory of model cognition**  
  Lenses are contextual scaffolds—not claims about understanding, memory, or internal mental state. Interpretive posture is simulated, not self-directed.

## What This Enables

| Benefit                     | Outcome |
|-----------------------------|---------|
| **Cross-model stability**   | Reduces behavioral variance across model versions and architectures. |
| **Role-consistent agents**  | Maintains tone, values, and reasoning style in long-horizon or multi-role systems. |
| **Faster debugging**        | Surfaces silent misalignments through reframing and frame inspection. |
| **Composable toolchains**   | Framing components are modular, portable, and easy to integrate into existing workflows. |
| **Behavior traceability**   | Knowing the applied lens improves understanding of *why* a model responded the way it did. |

## Rethinking Existing Techniques Through Behavioral Lensing

Many established prompting strategies already interact with the interpretive layer—but often do so **implicitly**, without naming or structuring that influence. Behavioral Lensing makes this layer **explicit**, giving practitioners a way to understand **why** certain techniques work, **when** they break down, and **how** to adapt them more reliably across contexts and models.

What follows isn’t a replacement—it’s a reframing. By viewing familiar strategies through the lens of interpretive control, we can explain their effects more precisely and extend their impact with intention.

### Chain-of-Thought (CoT)  
**Standard View:**  
Prompting the model to “think step by step” improves reasoning reliability.

**Behavioral Lensing View:**
CoT works not just by scaffolding logic, but by **incrementally constraining the model’s interpretive space**. Each step reduces ambiguity, guiding token prediction along a path that reinforces consistency with prior reasoning.

Because LLMs generate outputs token-by-token, early statements influence what the model considers likely or relevant later. CoT effectively **stabilizes the model’s worldview in progress**, anchoring it to a particular reasoning trajectory.

→ In lensing terms, CoT functions as **progressive interpretive anchoring**—shaping not just what the model does, but how it continues to interpret the task as it moves forward.

### Role Prompting  
**Standard View:**  
Assigning a role (e.g., “You are a lawyer”) helps shape the model’s tone, style, or decision-making strategy.

**Behavioral Lensing View:**  
Role prompts influence behavior by setting an **initial interpretive stance**—activating latent assumptions, language patterns, and domain-specific behaviors associated with that role. But roles on their own are often too shallow or underspecified to create consistent behavior.

Behavioral Lensing treats role prompts as **potential building blocks** for a more coherent interpretive frame. When integrated into a well-constructed IFB and supported by Symbolic Anchors, roles become more stable, controllable, and behaviorally aligned.

→ Role prompting is most effective when treated as **part of a structured lens**, not a standalone tactic.

### Few-Shot Prompting  
**Standard View:**  
Providing examples helps the model understand the task format and logic pattern.

**Behavioral Lensing View:**  
Examples do more than demonstrate structure—they **shape how the model interprets the task itself**. Each example implicitly communicates a reasoning style, tone, and set of priorities. Well-chosen examples can bias the model toward caution, pragmatism, creativity, or analysis—depending on what they signal.

In lensing terms, few-shot prompting works as **implicit interpretive anchoring**—guiding the model’s stance through modeled behavior rather than explicit instruction.

→ Few-shot examples don’t just show what to do. They **shape how the task is perceived.**

### Instruction Tuning  
**Standard View:**  
Training models on curated instruction-response pairs improves alignment and general task performance.

**Behavioral Lensing View:**
Instruction tuning shapes prompt interpretation by instilling a **default cooperative frame**. Models trained this way tend to assume they’re expected to be helpful, aligned, and human-facing—even before any role or task is specified.

This creates a **global interpretive lens**—a bias introduced at the training level that affects how instructions are processed across diverse contexts.

→ Instruction-tuned models aren’t just responsive—they’re **preconditioned** to interpret tasks through an instruction-following worldview.

### Self-Consistency Sampling  
**Standard View:**  
Generate multiple Chain-of-Thought completions and select the most frequent answer to improve reliability.

**Behavioral Lensing View:**  
Self-consistency isn't just about filtering noise—it reveals how consistently the model applies a reasoning stance across multiple runs. If a specific interpretation leads to similar reasoning paths repeatedly, it signals that the underlying interpretive frame is stable.

This makes self-consistency a practical way to **test interpretive robustness**—how reliable a particular framing is under repeated generation.

→ In lensing terms, self-consistency reflects the **stability of a model's interpretive alignment** over time.

### Rewriting for Clarity  
**Standard View:**  
Rewriting a prompt helps the model better understand the task or instructions.

**Behavioral Lensing View:**  
Rewrites often succeed not because the instructions were unclear, but because the original framing led the model to interpret the task in an unintended way. A new phrasing can shift the model’s **interpretive assumptions**, leading to different behavior—even if the task itself hasn’t changed.

→ In lensing terms, prompt rewrites often act as **unintentional reframing**—changing how the model understands what it's being asked to do.

## When to Use It

Behavioral Lensing is most effective in tasks where the model's **interpretive posture** meaningfully shapes outcomes. These include contexts that require stability, nuance, or consistent reasoning patterns—especially where ambiguity, longevity, or cross-model reliability are in play.

### Ideal Use Cases:
- **Agentic systems with long-horizon reasoning**
  - Multi-step planning or autonomous workflows.
  - Persistent chatbots that need consistent tone, goals, and reasoning stance across sessions.
  - Behavioral Lensing supports continuity by anchoring the model’s interpretive frame over time.

- **Ambiguous or open-ended tasks**
  - Creative writing with stylistic or tonal constraints.
  - Ethical, advisory, or judgment-based tasks with no single correct answer.
  - Interpretive scaffolding helps disambiguate intent and maintain coherence under uncertainty.

- **Alignment-sensitive contexts**
  - Legal, medical, or policy-related tasks where interpretive precision affects safety or validity.
	  - ⚠️ Use in high-stakes domains should be exploratory, carefully reviewed, and **never relied on as a substitute for expert judgment or regulated oversight**.
  - Brand-aligned generation where tone, value framing, and voice consistency matter.
  - Behavioral Lensing reduces drift and makes assumptions visible, testable, and steerable.

- **Cross-model consistency**
  - Ensuring similar outputs across model versions, providers, or inference environments.
  - Portable interpretive scaffolds (like IFBs and Symbolic Anchors) help normalize behavior despite architectural differences.

### Less Suitable For:
- Simple lookup or retrieval queries.
  - No interpretive space—factual grounding is the primary concern.

- Pure mathematical or symbolic computation.
  - Behavioral framing has limited impact unless explanation or educational value is required.

- Tasks with rigid format and minimal interpretive variance.
  - Use of lensing may introduce unnecessary complexity for fixed-structure outputs.

- Highly token-constrained scenarios.
  - Framing overhead may outweigh benefits unless interpretive alignment is critical to task success.

Even in these cases, **lightweight lensing**—such as a concise IFB or key Symbolic Anchor—can still improve clarity or reduce variability, particularly when operating across models or in sensitive domains.

## Limitations & Failure Modes

- **Overfitting**  
  Too rigid a framing can limit flexibility, leading the model to ignore valid alternative interpretations or edge cases.

- **Misreading as identity**  
  Interpretative Frames are context cues, not persistent traits. Behavioral Lensing shapes stance—not beliefs, memory, or intention. Avoid interpreting outputs as evidence of stable internal views.

- **Symbolic ambiguity**  
  Anchors may activate unintended associations, especially with abstract or ideologically loaded terms (e.g., “freedom,” “balance,” “justice”).

- **Anthropomorphic interpretation**  
  A well-framed lens may simulate domain fluency or intentionality—but it’s a surface behavior, not evidence of understanding or agency. Stay grounded in mechanism.

- **Lack of automation**  
  Currently, most lensing strategies require manual authoring or guided synthesis. Tooling for scalable, dynamic frame construction is still limited.

## Future Directions

- **Synthesis Tools**  
  Extract worldview scaffolds—such as IFBs or Symbolic Anchors—from existing text or model output. Useful for reverse-engineering implicit frames, generating reusable components, or adapting human-authored material into lens-compatible formats.

- **Session-Level Framing Persistence**  
  Strategies and tools to maintain a coherent interpretive frame across multi-turn or long-form interactions. Useful for aligning agent behavior with evolving goals and minimizing drift over time.

- **Framing Drift Monitoring**  
  Detect when a model’s interpretive posture shifts mid-session, enabling real-time adjustments or diagnostics.

- **Interpretive Comparators**  
  Analyze how different framing setups influence reasoning trajectories, output quality, or alignment stability.

- **Frame Libraries**  
  Curated, task-specific collections of IFBs, Symbolic Anchors, and Reasoning Paths for common domains or use cases.

- **Adaptive IFB Optimization**  
  Systems that recommend, adapt, or fine-tune framing elements based on task type, domain constraints, or behavioral goals.

## Try It Yourself

- **Prompt Sequence** → [IFB Constructor](./flows/ifb-contructor/)  
  Step-by-step prompts for building Interpretive Framing Blocks and evaluating alignment.

- **Live Examples** → [Example Evaluations](./examples/)  
  Side-by-side comparisons of standard vs IFB-enhanced outputs across multiple models.
  
## Glossary of Key Terms

| Term | Definition |
|------|------------|
| **Lens** | Any prompt element—role, symbol, tone, structure—that influences how a model interprets its task. The outer layer of interpretive control. |
| **Interpretive Frame** | The internal context the model constructs from a lens—a transient worldview that shapes its perception of the task. |
| **Worldview** | Informal shorthand for the interpretive frame—emphasizing tone, values, and orientation. Not a belief system or persistent identity. |
| **Interpretive Posture** | The model’s simulated stance during generation—activated by framing—which governs tone, strategy, and reasoning style. |
| **Interpretive Framing Block (IFB)** | A short, expressive preamble that sets the model’s interpretive stance before task instructions begin. |
| **Symbolic Anchor (SA)** | High-impact terms that trigger latent associations—such as values, methods, or identities—that guide the model’s interpretive process. |
| **Task Reflection (TR)** | A prompt asking the model to explain how it currently understands its task and role—used for alignment and diagnosis. |
| **Reasoning Path (RP)** | A structured logic strategy embedded in the instructions—step-by-step thinking, comparative analysis, etc.—meant to align with the interpretive frame. |
| **Inference Path** | The trajectory the model takes while generating output—guided by its interpretive frame and prior tokens. |
| **Interpretive Drift** | A shift in the model’s interpretive frame mid-generation or across turns, leading to inconsistent behavior. |
| **Latent Behavior** | Behavioral tendencies the model can express when prompted—shaped by pretraining, and activated or suppressed by context. |

## Summary

Behavioral Lensing isn’t a workaround—it’s an architectural layer.\
It gives structure to what the model infers before it acts.

> Instruction is not the highest control layer.\
> **Interpretation is.**

By surfacing that layer—and naming it—**we regain leverage**.

## The Shape of Invisible Control

You don't point the model down a path.  
 
*You tilt the terrain it walks on—subtly shaping what feels likely, appropriate, or correct.*  
 
Behavioral Lensing is the quiet architecture of slope—the shaping of what a model sees as obvious, likely, resonant.  

This subtle influence isn't merely decorative—**It's foundational.**

***Explore the examples. Try the flows. See what shifts when you shift the frame.***

## License

This work is licensed under [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/).

**What this means:**
- You are free to use, adapt, modify, and build upon this framework.
- You can use it for any purpose, including commercial applications.
- You must give appropriate credit, provide a link to the license, and indicate if changes were made.
