# Behavioral Lensing

### *A Framework for Shaping Language Model Behavior through Intentional Framing*

## Project Status & How to Engage

**Behavioral Lensing** is an evolving framework designed to clarify and formalize how language models interpret prompts.

Formal contributions (e.g., pull requests) are not currently accepted, but active engagement is encouraged:

*   **Discussions:** Share insights, questions, and use cases.
*   **Issues:** Report limitations or suggest improvements.
*   **Experiments:** Share results from applying Behavioral Lensing.

As the framework matures, the contribution model will expand.
*Star this repository for updates.*

### Governance & Decision-Making

As the maintainer, I currently oversee direction and implementation. All feedback is carefully reviewed and integrated if aligned with the project's core vision.

---

## Table of Contents

1.  [Overview](#overview)
2.  [The Problem Hidden in Plain Sight](#the-problem-hidden-in-plain-sight)
    *   [Key Terminology Clarified](#key-terminology-clarified)
    *   [Symptoms of Misaligned Framing](#symptoms-of-misaligned-framing)
3.  [A Different Perspective](#a-different-perspective)
4.  [Summary of the Problem](#summary-of-the-problem)
5.  [Why This Matters](#why-this-matters)
6.  [Behavioral Lensing: Defined](#behavioral-lensing-defined)
7.  [Core Components](#core-components)
    *   [Interpretive Framing Block (IFB)](#interpretive-framing-block-ifb)
    *   [Symbolic Anchors (SA)](#symbolic-anchors-sa)
    *   [Task Reflection (TR)](#task-reflection-tr)
    *   [Reasoning Path (RP)](#reasoning-path-rp)
    *   [Integration & Practical Workflow](#integration--practical-workflow)
8.  [Clarifying Scope and Intent](#clarifying-scope-and-intent)
9.  [What This Enables](#what-this-enables)
10. [Rethinking Existing Techniques Through a Behavioral Lens](#rethinking-existing-techniques-through-a-behavioral-lens)
    *   [Chain-of-Thought (CoT)](#chain-of-thought-cot)
    *   [Role Prompting](#role-prompting)
    *   [Few-Shot Prompting](#few-shot-prompting)
    *   [Instruction Tuning](#instruction-tuning)
    *   [Self-Consistency Sampling](#self-consistency-sampling)
    *   [Rewriting for Clarity](#rewriting-for-clarity)
11. [When to Use It](#when-to-use-it)
    *   [Ideal Use Cases](#ideal-use-cases)
    *   [Less Suitable Use Cases](#less-suitable-use-cases)
12. [Limitations & Failure Modes](#limitations--failure-modes)
13. [Future Directions](#future-directions)
14. [Try It Yourself](#try-it-yourself)
15. [Glossary of Key Terms](#glossary-of-key-terms)
16. [Summary](#summary)
17. [The Shape of Invisible Control](#the-shape-of-invisible-control)
18. [License (CC BY 4.0)](#license)

---

## Overview

Language models don’t just follow instructions; they **interpret** them. Interpretation begins before task execution even starts.

**Behavioral Lensing** is a structured approach to intentionally shaping this interpretive frame: the perspective a model uses to understand prompts. By explicitly guiding this interpretive stance, model outputs become more **consistent, aligned, and contextually appropriate**.

> **Before instructing a model, you shape what kind of model it believes it should be.**
>
> Behavior isn’t shaped only by instructions, but by *how the model frames those instructions.*
>
> Behavioral Lensing intentionally designs that frame, not as a trick or persona, but as foundational scaffolding.

This framework benefits anyone working closely with language models:

*   **Prompt engineers**
*   **Tool developers**
*   **Researchers and educators**
*   **Anyone seeking reliable control over model interpretation**

---

## The Problem Hidden in Plain Sight

Language models appear to follow instructions, but they always start from implicit **assumptions**.

Every prompt passes through a **transient interpretive frame** (a fleeting, internally constructed context) which shapes:

*   Tone and stance.
*   Relevance judgments.
*   Success criteria.
*   Assumptions about the model's role relative to the task.

This creates a subtle, pervasive issue:

> **Prompt failures usually aren’t about unclear instructions.**
> They’re about **unacknowledged framing**.

### Key Terminology Clarified

*   **Lens:** Any prompt element (role, tone, symbol, structure) influencing interpretation.
*   **Interpretive Frame:** The internal context constructed from the lens; the model’s momentary "worldview."
*   **Worldview:** Informal shorthand emphasizing values, tone, and orientation, *not* fixed beliefs or persistent identity.

These terms represent temporary structures influencing generation at the token-level moment, *not* cognition or belief.

### Symptoms of Misaligned Framing
Misalignment often results in subtle but consistent issues:

*   Tasks completed correctly but from unintended perspectives.
*   Mid-response shifts in tone or reasoning.
*   Inconsistent performance of chain-of-thought (CoT) prompts.
*   Unpredictable role-prompt behavior.
*   Poor cross-model prompt transferability.

These symptoms reflect underlying **interpretive drift**.

---

## A Different Perspective

Current prompt design mainly addresses **content**:

*   Precise instructions.
*   Stronger examples.
*   Clearer wording.

Meanwhile, alignment researchers typically treat this as a **training issue**, solvable through more data or fine-tuning.

Missing is a layer of direct **interpretive control**: actively shaping the model’s framing before generation even begins.

Behavioral Lensing fills this gap.

---

## Summary of the Problem

| Problem                              | Traditional View                  | Behavioral Lensing View           |
|--------------------------------------|-----------------------------------|-----------------------------------|
| Prompt misfires                      | Poor phrasing                     | Misaligned interpretive frame      |
| CoT inconsistency                    | Weak reasoning chain              | Missing explicit reasoning stance |
| Role-prompt instability              | Random variation                  | Missing symbolic/value anchors    |
| Cross-model divergence               | Model differences                 | No stable interpretive scaffold   |
| Open-ended alignment failures        | Vague instructions                | Misaligned worldview              |

Behavioral Lensing shifts focus from controlling outputs directly, toward explicitly shaping **how the model understands tasks**.

Once visible, interpretation becomes steerable.

---

## Why This Matters

Traditional prompting advice emphasizes **what** to ask. Yet language models respond as much to **how** something is asked (tone, implicit roles, symbolic cues) as to the direct content of instructions.

Every prompt already implicitly frames the model's behavior.

Behavioral Lensing makes this framing **intentional**. It's not a superficial tactic, but a strategic reframing of prompt design:

*   Every prompt is a lens.
*   Every lens shapes behavior.

Mastering this mindset grants new leverage:

*   Improved reasoning consistency.
*   Better tone and role alignment.
*   Enhanced reproducibility across models.

> **Interpretation, not instruction, is the fundamental control layer.**

---

## Behavioral Lensing: Defined

**Behavioral Lensing** is a structured approach to deliberately shaping language-model outputs through interpretive framing.

Its core principle:

> **Models generate outputs within an interpretive frame, *not* from a blank state.**

By carefully designing this frame (through roles, tones, values, or symbolic anchors) you shape how the model perceives tasks, guiding token generation.

This doesn't alter architecture; it shapes the **generation trajectory** itself.

---

## Core Components

Behavioral Lensing provides structured methods for intentionally shaping a model’s interpretive stance. This stance affects how the model understands tasks, selects reasoning paths, and generates responses.

Four modular components form the practical toolkit of Behavioral Lensing. Each component builds on the others, creating layered interpretive scaffolding:

| Component                          | Function                                                                                                 |
|------------------------------------|----------------------------------------------------------------------------------------------------------|
| **Interpretive Framing Block (IFB)** | Establishes a contextual stance (anchored in roles, values, or epistemic posture) to prime how the model interprets tasks. |
| **Symbolic Anchors (SA)**          | Highlights terms that implicitly evoke associations, subtly guiding the model’s framing without explicit direction. |
| **Task Reflection (TR)**           | Surfaces the model’s interpretive assumptions explicitly, clarifying its understanding before task execution begins. |
| **Reasoning Path (RP)**            | Specifies how the model should reason through a task, reinforcing alignment with the established interpretive stance. |

These components are **modular and composable**, and together they offer compound interpretive control.

### Interpretive Framing Block (IFB)

An **Interpretive Framing Block (IFB)** is a concise, expressive preamble that primes the model with a particular **interpretive stance**, defining values or epistemic approaches relevant to a task.

> An IFB isn’t a persona or style layer. It creates a contextual **posture**, guiding interpretation from the start.

#### How It Works in Practice:

An IFB emerges from carefully extracting symbolic cues embedded in roles or tasks. The process typically involves:

1.  **Symbolic Deconstruction:**
    Identifying subtle framing cues (Symbolic Anchors) within a prompt: terms signaling roles, values, epistemic stances, or functional orientations.

2.  **Interpretive Expansion:**
    Mapping latent associations from these anchors to clarify the implied interpretive posture.

3.  **IFB Generation and Refinement:**
    Crafting multiple IFB variants from symbolic inputs, then synthesizing them into a coherent, aligned stance through comparative evaluation.

**Example IFB (UX Domain):**

```text
Years of designing digital products have taught me that meaningful user experiences are conversations between design, context, and the people involved. My approach is empathetic yet strategic, informed by experience but guided by humility. I prioritize clarity, usefulness, and quiet transformation: designs that resonate deeply because they understand user realities and thoughtfully stretch toward possibility.
```

#### Purpose:

An IFB sets the **interpretive foundation**, shaping how instructions are perceived, clarifying their context for the model.

### Symbolic Anchors (SA)

**Symbolic Anchors** are carefully chosen terms or phrases within prompts that implicitly shape a model’s interpretive stance. They act as subtle behavioral triggers, activating latent associations rather than explicitly instructing behaviors.

#### Types of Symbolic Anchors:

| Type                 | Examples                         |
|----------------------|----------------------------------|
| **Role/Identity**    | “UX strategist,” “mentor”        |
| **Epistemic Frame**  | “Investigate,” “diagnose,” “evaluate” |
| **Ideological/Value**| “Sustainable,” “equitable,” “ethical” |
| **Functional Language**| “Streamline,” “optimize,” “synthesize” |

#### Practical Application:

Anchors are explicitly extracted via Symbolic Deconstruction prompts, which surface latent interpretive signals, clarify their influence on framing, and guide coherent IFB construction.

### Task Reflection (TR)

A **Task Reflection (TR)** prompt explicitly asks the model to summarize its current understanding of the interpretive stance, intended role, and strategy before task execution.

#### Typical TR Prompt:

```text
Summarize your understanding of the task, your role, and your intended approach.
```

#### Purpose:

*   **Diagnostic Visibility:** Makes implicit framing assumptions explicit before task execution.
*   **Alignment Check:** Identifies subtle interpretive drift or misalignment.
*   **Behavioral Stability:** Primes the model’s reasoning trajectory, reinforcing coherence through explicit reflection.

### Reasoning Path (RP)

A **Reasoning Path (RP)** provides structured guidance on how the model should approach its task cognitively. It doesn’t dictate exact outputs but aligns the reasoning process explicitly with the interpretive stance established by the IFB and Symbolic Anchors.

#### Reasoning Path Examples:

| Reasoning Style          | Example Instruction                                  |
|--------------------------|------------------------------------------------------|
| **Stepwise analysis**    | “Break down the task into clear, sequential stages.” |
| **Comparative reasoning**| “Compare advantages and disadvantages explicitly.”   |
| **Risk assessment**      | “Identify and explain potential pitfalls.”           |
| **Iterative refinement** | “Propose an initial solution, then suggest improvements.” |

#### Practical Alignment:

RPs function best when explicitly reinforcing the interpretive foundation set by IFBs and Anchors, ensuring behavioral coherence throughout the generation process.

### Integration & Practical Workflow

A typical Behavioral Lensing workflow involves:

*   **Extracting Symbolic Anchors** (SA) from task or role prompts.
*   **Constructing an IFB** from symbolic anchors through iterative refinement.
*   **Using Task Reflection** (TR) prompts to surface the model’s interpretive assumptions explicitly.
*   Providing a clear **Reasoning Path** (RP) aligned with this established stance.

These modular components, powerful individually, achieve maximum effectiveness when combined systematically.

---

## Clarifying Scope and Intent

Before applying Behavioral Lensing, it helps to clearly understand what it **is** and what it is **not**.

Behavioral Lensing differs fundamentally from common prompting approaches. It isn't merely about personas or tone; it’s about intentionally shaping the **model’s interpretive posture** before generation begins.

#### Behavioral Lensing **is not**:

*   **Persona Construction:** It doesn’t simulate fictional characters or persistent identities.
*   **Stylistic Polish:** While it can influence tone, its primary goal is shaping interpretive context, not voice alone.
*   **Prompting Tricks:** It isn’t meant for exploiting model loopholes or superficial optimization.
*   **Model Cognition Theory:** It doesn't assume cognitive processes or internal states, only behavioral stances.

#### Behavioral Lensing **is**:
A structured method of shaping the **temporary interpretive stance** a model adopts, guiding reasoning style, priorities, and tone from the start.

> Lensing doesn’t prescribe the model’s response directly. It subtly tilts the interpretive landscape, guiding how responses naturally emerge.

---

## What This Enables

Behavioral Lensing introduces a distinct layer of **behavioral leverage**, shaping interpretation before generation occurs. This enables:

| Capability                  | Outcome                                           |
|-----------------------------|---------------------------------------------------|
| **Cross-model Stability**   | Consistent behavior across model architectures and versions. |
| **Role Consistency**        | Improved coherence in long, multi-step tasks.     |
| **Rapid Debugging**         | Quickly surfaces and resolves interpretive misalignments. |
| **Reusable & Modular Workflow** | IFBs, Anchors, and Reasoning Paths are reusable and composable. |
| **Behavior Traceability**   | Clarifies the interpretive causes behind model behavior, aiding explanation. |

> Interpretation is the critical leverage point. Control interpretation, and you control behavior.

---

## Rethinking Existing Techniques Through a Behavioral Lens

Many established prompting techniques already influence a model’s interpretive stance, but they often do so implicitly. Behavioral Lensing makes this interpretive influence **explicit**, enhancing clarity and reliability.

Here’s how familiar techniques look through a lensing perspective:

### Chain-of-Thought (CoT)

**Traditional View:**
Encourages logical reasoning by prompting the model to "think step-by-step."

**Behavioral Lensing View:**
Each CoT step incrementally clarifies and narrows the interpretive stance. Early reasoning guides future token predictions, stabilizing interpretive coherence throughout the response.

> CoT becomes **progressive interpretive anchoring**, not just explicit reasoning support.

### Role Prompting

**Traditional View:**
Assigning roles (“You’re a lawyer”) helps set tone and expertise.

**Behavioral Lensing View:**
Roles trigger latent behavioral tendencies: associations learned implicitly during training. But on their own can be unstable. Integrating roles into structured IFBs, supported by symbolic anchors, makes interpretive posture stable and robust.

> Role prompting gains strength when integrated into deliberate interpretive framing.

### Few-Shot Prompting

**Traditional View:**
Examples demonstrate desired structure, logic, and output format.

**Behavioral Lensing View:**
Examples implicitly embed interpretive stances. Each example subtly frames the task’s worldview, influencing the model’s perspective even without explicit framing.

> Few-shot prompting inherently provides **implicit interpretive cues**.

### Instruction Tuning

**Traditional View:**
Instruction-response training improves general alignment and helpfulness.

**Behavioral Lensing View:**
Instruction tuning instills a default interpretive stance: cooperative and user-facing. Models trained this way inherently interpret tasks through a human-facing, helpful stance.

> Instruction-tuned models come preconditioned with a **default interpretive lens**.

### Self-Consistency Sampling

**Traditional View:**
Generating multiple outputs (using CoT) and selecting the most frequent result reduces variability.

**Behavioral Lensing View:**
Self-consistency sampling tests the stability and coherence of the interpretive frame. Frequent convergence indicates a coherent interpretive stance, highlighting frame robustness rather than just noise reduction.

> Self-consistency sampling tests interpretive coherence, showing **robustness of the frame**.

### Rewriting for Clarity

**Traditional View:**
Prompt rewrites improve clarity, enhancing model performance.

**Behavioral Lensing View:**
Rewrites often work because they shift the interpretive frame, introducing different implicit stances, not just improved syntax. Rewriting thus becomes intentional **reframing**, not merely rephrasing.

> Clarity rewrites are implicitly **interpretive adjustments**.

---

## When to Use It

Behavioral Lensing is particularly effective where interpretation heavily influences outcomes. Its strength lies in shaping tasks involving ambiguity, nuanced reasoning, or sustained behavioral coherence.

### Ideal Use Cases

#### 1. **Agentic or Multi-Step Tasks**

*   Complex, multi-stage workflows
*   Persistent conversational agents
*   Autonomous task executions

> **Benefit:** Ensures stable interpretive coherence across evolving tasks.

#### 2. **Ambiguous or Creative Tasks**

*   Ideation and brainstorming
*   Creative generation (tone or stylistic constraints)
*   Ethical or advisory scenarios without fixed outcomes

> **Benefit:** Clarifies interpretive posture, maintaining coherent reasoning and tone.

#### 3. **Alignment-Sensitive Domains**

*   Legal, medical, or policy-oriented contexts
*   Brand-voice consistency.
*   Tasks where interpretive precision directly impacts reliability, accuracy, or safety.

> **Benefit:** Surfaces implicit assumptions explicitly, enhancing transparency and alignment.

> ⚠️ **Note:** For high-stakes use (e.g., medical/legal), Behavioral Lensing is exploratory. Never substitute it for expert judgment in high-stakes contexts.

#### 4. **Cross-Model Reliability**

*   Prompts designed to run consistently across different models or providers
*   Benchmarking interpretive coherence across multiple models
*   Ensuring stable outputs despite architectural differences

> **Benefit:** Reduces interpretive variance and maintains behavioral predictability.

### Less Suitable Use Cases

Behavioral Lensing provides limited benefit when tasks have minimal interpretive complexity or highly constrained formats:

*   **Simple Information Retrieval:** Basic factual lookups requiring precision, not interpretation.
*   **Pure Mathematical Tasks:** Tasks explicitly computational without interpretive demands.
*   **Highly Constrained Formats:** Tasks with rigid output structures (e.g., fixed JSON).
*   **Short Token-Limited Responses:** Tasks where framing overhead outweighs interpretive benefits.

#### **Middle Ground (Minimal Framing):**
Even minimal framing (a concise IFB or one symbolic anchor) can significantly improve consistency and clarify default behaviors.

---

## Limitations & Failure Modes

Behavioral Lensing is powerful but not foolproof. Recognizing its limitations helps ensure responsible, effective use.

### 1. **Overfitting the Frame**

*   Excessively rigid framing can limit model adaptability.
*   Reduces creative or exploratory responses.

> **Mitigation:** Frames must guide, rather than constrain, interpretation.

### 2. **Misreading Framing as Identity**

*   Interpretive frames are transient and context-dependent.
*   Frames do not reflect persistent identities or beliefs.

> **Mitigation:** Remain aware frames shape temporary stances, not internal states.

### 3. **Ambiguity in Symbolic Anchors**

*   Broad or culturally loaded terms may produce unpredictable interpretations.
*   Inconsistent anchor effects across model versions.

> **Mitigation:** Test anchors thoroughly and use precise, culturally aware language.

### 4. **Anthropomorphic Misinterpretation**

*   Coherent interpretive frames may appear intelligent or insightful.
*   Framing is a simulated surface behavior, not genuine understanding.

> **Mitigation:** Always distinguish clearly between interpretive coherence and genuine cognition.

### 5. **Manual Workflow & Tooling**

*   Right now, framing generation is not fully automated. Current workflows rely heavily on manual prompt chaining.
*   Automated tools for frame construction are still developing.

> **Mitigation:** Recognize current manual overhead and plan for incremental automation.

---

## Future Directions

Behavioral Lensing remains in active development. Several promising avenues offer expanded capabilities, improved usability, and deeper analytical insights.

### 1. **Automated Framing Synthesis**

*   Tools extracting IFBs and symbolic anchors directly from textual examples or prior successful prompts.
*   Automated identification of latent interpretive stances from existing texts.

> **Benefit:** Accelerates lens construction, reduces manual overhead, and enhances reproducibility.

### 2. **Persistent Session Framing**

*   Methods for maintaining coherent interpretive frames across multiple conversational turns or extended task interactions.
*   Strategies for dynamically adjusting frames while preserving interpretive coherence.

> **Benefit:** Minimizes interpretive drift in long-term interactions, increasing behavioral stability.

### 3. **Interpretive Drift Detection**

*   Real-time tools to monitor shifts in the model’s interpretive posture.
*   Methods for automatically detecting and correcting interpretive misalignments.

> **Benefit:** Ensures continuous interpretive alignment, reducing silent misinterpretations.

### 4. **Interpretive Frame Benchmarking**

*   Comparative evaluation frameworks to quantify how different framing approaches influence reasoning, alignment, and interpretive stability.
*   Metrics quantifying interpretive coherence and robustness.

> **Benefit:** Provides evidence-based guidance for optimal framing practices.

### 5. **Reusable Frame Libraries**

*   Curated sets of IFBs tailored to specific roles, industries, or tasks.

> **Benefit:** Simplifies lens construction, encourages reuse, and standardizes effective framing.

### 6. **Adaptive & Context-Aware Framing**

*   Systems that dynamically adjust interpretive framing based on real-time context, feedback, or task performance.
*   Automated adaptation of IFBs and anchors during task execution.

> **Benefit:** Enables responsive, context-sensitive interpretive guidance.

---

## Try It Yourself

Behavioral Lensing is best mastered through direct experimentation. Here are resources designed for immediate practical application:

### **1. IFB Constructor**
**→ [Build Your Interpretive Framing Block](./flows/ifb-contructor/)**

A structured, step-by-step process for constructing IFBs and aligning them to your tasks.

> **Ideal for:** Crafting precise framing stances to clarify and anchor model interpretations.

### **2. Example Evaluations**
**→ [See IFBs in Action](./examples/)**

View practical side-by-side comparisons demonstrating how IFBs influence model outputs across various contexts.

> **Use this for:** Learning how framing shifts model behavior.

---

***The best way to master framing is to create your own lenses.***

Start by enhancing prompts you already use successfully, add IFBs with explicit reasoning paths, then compare performance against your original baseline.

---

## Glossary of Key Terms

| Term                        | Definition                                                                     |
|-----------------------------|--------------------------------------------------------------------------------|
| **Lens**                    | Any prompt element influencing a model’s interpretive stance (role, tone, symbol, or structure). |
| **Interpretive Frame**      | The transient internal context a model forms from a lens, shaping immediate understanding. |
| **Worldview**               | Informal shorthand for an interpretive frame, emphasizing values, tone, and orientation, *not* persistent identity. |
| **Interpretive Posture**    | Temporary behavioral stance activated by framing; guides tone and reasoning during generation. |
| **Interpretive Framing Block (IFB)** | Concise preamble explicitly shaping the interpretive stance before task execution.        |
| **Symbolic Anchor (SA)**    | Key phrases triggering implicit behavioral associations, influencing interpretation indirectly. |
| **Task Reflection (TR)**    | Prompting the model to articulate its interpretive assumptions before completing the task.   |
| **Reasoning Path (RP)**     | Structured guidance shaping how the model cognitively approaches reasoning through a task.    |
| **Inference Path**          | The evolving sequence of token generation, guided by interpretive framing and autoregressive context. |
| **Interpretive Drift**      | Shifts in the model’s interpretive stance mid-generation or across turns, leading to inconsistency. |
| **Latent Behavior**         | Behavioral tendencies learned during training, activated or suppressed through interpretive framing. |

---

## Summary

Behavioral Lensing isn't just an optimization; it’s a fundamental rethinking of how prompts shape model behavior.

It reveals and deliberately shapes what already happens implicitly: the interpretive framing that guides how models perceive and tackle tasks.

> **Interpretation, not instruction, is the deepest layer of behavioral control.**

By intentionally shaping this layer, we gain:
*   Predictable behavior before generation starts.
*   More stable and aligned reasoning.
*   Enhanced consistency across tasks and models.

This isn't about tricking models into certain responses. It’s about deliberately clarifying the interpretive conditions for reliable and purposeful outcomes.

---

## The Shape of Invisible Control

You don’t point the model down a path.
**You tilt the terrain it walks on, subtly shaping what feels likely, appropriate, or true.**

Behavioral Lensing uncovers this subtle, influential layer: not rules or scripts, but **potentials** and **inclinations**.

> It’s not a fixed route you force the model to follow.
> It’s the invisible slope you carefully design, gently steering interpretation from the outset.

***Explore the examples. Build your own lenses.***
***Discover how behavior shifts when you shift the frame.***

---

## License

This work is licensed under [Creative Commons Attribution 4.0 International (CC BY 4.0)](https://creativecommons.org/licenses/by/4.0/).

**What this means:**
*   You are free to use, adapt, modify, and build upon this framework.
*   You can use it for any purpose, including commercial applications.
*   You must give appropriate credit, provide a link to the license, and indicate if changes were made.