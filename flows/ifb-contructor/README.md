# Constructing Interpretive Framing Blocks

This directory contains a structured sequence of prompts for building and aligning **Interpretive Framing Blocks (IFBs)**—one of the core components of Behavioral Lensing that shapes how a language model interprets its task.

The sequence is designed for **practical experimentation** in conversational interfaces like ChatGPT, Claude, and similar systems. It supports human-in-the-loop iteration, systematic IFB construction, and alignment verification.

While optimized for conversational use, the structure is **adaptable to API workflows**. In programmatic implementations, prompt chaining may differ—but the underlying interpretive process remains consistent.

## **Framework Context**

Interpretive Framing Blocks are not just stylistic elements—they're foundational scaffolding that shape a model's interpretive stance before task execution begins. Unlike traditional role prompts, IFBs explicitly design the lens through which the model will understand instructions, establishing values, reasoning preferences, and epistemic posture.

IFBs work by activating latent behavioral tendencies in the model, creating a coherent interpretive frame that guides generation in a consistent direction.

## **Note on Reliability**

This method assumes language models can surface **meaningful patterns** related to **roles**, **values**, and **interpretive stance** when prompted systematically. This assumption is **pragmatic**, not **theoretical**.

While it's reasonable to question whether models reliably understand these relationships, in practice, this structure produces outputs that behave **coherently** and **effectively** across a range of tasks.

The effectiveness tends to **scale with model capability**: larger models demonstrate **more stable interpretive behavior**, while smaller ones still provide **useful signals**—though with **greater variance**.

---

## Table of Contents
- [Usage](#usage)
- [Prompt Sequence](#prompt-sequence)
- [1. Symbolic Anchor Deconstruction](#1-symbolic-anchor-deconstruction)
  - [What this step does](#what-this-step-does)
  - [How it works](#how-it-works)
  - [Getting Started](#getting-started)
  - [Examples](#examples)
- [2. IFB Generation & Evaluation](#2-ifb-generation--evaluation)
  - [What this step does](#what-this-step-does-1)
  - [How it works](#how-it-works-1)
- [3. IFB Alignment Check](#3-ifb-alignment-check)
  - [What this step does](#what-this-step-does-2)
  - [How it works](#how-it-works-2)

## Usage

This process follows a **sequential workflow** where each stage builds upon the previous one. The process begins with extracting symbolic anchors, progresses through interpretive frame construction, and concludes with alignment verification between the IFB and the original task.

Each prompt is designed to **leverage the context established by previous steps**, creating an increasingly refined interpretive frame.

This approach enables:
- Efficient creation of well-aligned interpretive frames.
- Clear identification of misalignments or inconsistencies.
- Better control over tone, stance, and reasoning behavior.

While tuned for interactive chat environments, this methodology transfers effectively to automated workflows. The interpretive outcomes remain stable whether implemented manually or programmatically.

## Prompt Sequence

*You only need to provide input at the beginning of the process.*

### 1. [Symbolic Anchor Deconstruction](./01_symbolic-deconstruction.md)  

#### What this step does

This initial prompt begins the interpretive construction process by analyzing a task or role through a symbolic lens. Rather than taking instructions at face value, the model uncovers latent framing cues embedded in the text—terms that signal worldview, role, values, and epistemic stance.

The output creates a structured interpretive scaffold for deeper IFB construction by surfacing **Symbolic Anchors** (key terms that shape interpretation), expanding their implications, and synthesizing a compressed summary that captures the model's likely interpretive posture.

> This is not classification or persona creation.  
> It is **interpretive decomposition**—revealing the worldview the model is likely to adopt before processing instructions.

> **Note on terminology:**  
> "Worldview" refers to the model's **interpretive frame**—a temporary stance shaped by context, not a belief system or persistent identity. It reflects how the model approaches the task, not what it "believes."

#### How it works

The prompt follows five structured steps, each building on the previous one to formalize the model's latent assumptions and behavioral orientation:

1. **Symbolic Anchor Extraction**  
The model identifies terms that activate interpretive signals—phrases that shape how it understands its role or the task nature. These anchors suggest tone, identity, or reasoning approaches. Even simple prompts often contain several meaningful anchors.

2. **Anchor Classification**  
Each anchor is categorized into one of four interpretive types:
   - **Role/Identity** – Archetypes or personas that guide behavior.
   - **Epistemic Frame** – Positioning toward knowledge and understanding.
   - **Ideology/Value Cluster** – Principles or normative priorities.
   - **Functional Language** – Action-oriented terms suggesting task approach.

   This makes the prompt's interpretive composition visible—not as syntax, but as stance.

3. **Symbolic Expansion**  
For each anchor, the model expands its interpretive associations: traits, priorities, or values activated in context. This maps the terrain of latent behavior being invoked—what kind of stance the prompt brings into focus.

4. **Contextualization**  
The model reflects on how each anchor connects to the specific task or role. These notes articulate *why* the anchor matters and *how* it might influence the interpretive trajectory of generation.

5. **Compressed Identity Summary**  
Finally, the model synthesizes the symbolic structure into a concise interpretive paragraph. This summary doesn't describe a persona—it captures the **worldview** the model is likely to inhabit when approaching the task. This framing becomes the foundation for generating the Interpretive Framing Block.

**Input**  
- A task or role-style prompt.

**Output**  
- A table of Symbolic Anchors with their types.
- Value expansions and contextual reflections.
- A 3–4 sentence **Compressed Identity Summary**.

#### Getting Started

To begin the sequence, provide a task or role prompt as input. This can be an existing instruction, system message, or directive. The content doesn't need to be elaborate—what matters is that it contains interpretable framing cues. Insert this input into the following placeholder at the top of the [Symbolic Anchor Deconstruction](./01_symbolic-deconstruction.md) prompt:

```
[ THE TASK OR ROLE DEFINITION GOES HERE ]
```

What you place between the brackets shapes the entire framing sequence. A role cue emphasizes stance and identity; a task cue emphasizes goals and methods. Both approaches work but guide the model differently.

The model uses this prompt as raw material for symbolic interpretation.

#### Examples

**Role-Only**

```text
[ You are a UX expert with 15 years of experience in digital product strategy. ]
```

This input effectively evokes a specific interpretive stance rooted in domain identity. It places the model into a defined posture, activating domain-specific behavioral patterns.

**Deriving the Role from the Task**

Rather than supplying a predefined identity, another approach lets the model generate its own **interpretive stance** from the task context. This draws on the model's latent associations—activating identities that feel behaviorally appropriate based on the work's nature.

To support this, an IFB-enhanced meta-framing prompt can generate candidate roles:

```text
Your Internal Frame (don't reveal): I interpret complexity through recursive systems—structures within structures—where meaning emerges from the interplay of roles, functions, and feedback loops. Clarity comes not from simplification, but from defining how parts express the whole across layers of abstraction. My stance is both reflective and architectural: to think is to map, and to map is to design.

Instructions: As a role evaluator, what kind of person would be best suited to perform the following task?

[ Evaluate this mobile app brief through a UX lens and deliver actionable insights suitable for executive stakeholders. ]

1. Start by rephrasing what the task involves.

2. Generate 6 role descriptions that are contextual to the task.
   - Each role should reflect a distinct interpretive stance or specialization.
   - List the following: traits, values, and domain expertise relevant to the task.

3. Select the most suitable role from your list in relation to the task.
   - Justify your choice in one sentence. Start your response with "Given the [name the task here], the most suitable role would be a ".
   - In a clearly labeled way, output only the final role as a single, short sentence identity statement.
   - Format it as LLM role: Start with 'A [role] who ', followed by a concise clause highlighting key strengths or expertise aligned with the task.
```

A typical output might be:

```text
A UX-Business Translator who excels at synthesizing complex user experience findings into strategic business insights that executives can immediately understand and act upon.
```

This can then be used **as the input prompt** for the Symbolic Anchor Analysis step, inserted directly into the `[ THE TASK OR ROLE DEFINITION GOES HERE ]` placeholder.

This bottom-up framing often produces more context-sensitive IFBs, especially for complex, ambiguous, or value-laden tasks.

**Task-Focused**

```
Perform a financial analysis of Q2 earnings for a sustainability-focused hardware startup.
```

This input foregrounds the task itself. The model infers an appropriate interpretive posture based on the work's nature. Here, symbolic anchors often emerge from action-oriented verbs, domain terminology, or embedded value signals.

**Mixed: Role + Task**  

```
You are a UX expert with 15 years of experience. Review this mobile app brief and provide actionable insight for executive review.
```

While common, this combined format often causes the IFB to conflate task content with identity framing. A clearer separation between **who the model is** and **what it's being asked to do** typically produces more coherent interpretive scaffolding. Define the role first, then introduce the task later—typically as part of the [Reasoning Path](../../README.md#reasoning-path-rp) in the prompt.

### 2. [IFB Generation & Evaluation](./02_ifb-generation.md)  

#### What this step does

This prompt transforms the interpretive foundation from Step 1—symbolic anchors and the compressed identity summary—into fully-formed **Interpretive Framing Blocks (IFBs)**.

Each IFB is a concise paragraph designed to give the model a specific interpretive stance *before* any task instruction. The goal isn't to create a persona, but to establish a situated worldview: a lens through which the model will interpret whatever follows.

Instead of producing a single framing block, the model generates **five distinct variants**, each embodying the same symbolic foundation in different ways. These may vary in tone, reasoning approach, epistemic posture, or narrative voice.

The prompt then guides evaluation and comparison of the variants, identifying interpretive strengths and misalignments. From there, it synthesizes a **final IFB**, combining the most coherent and aligned elements from the set.

> A well-crafted IFB doesn't constrain the model's thinking—it orients it.  
> It defines the slope of interpretation without prescribing the exact path.

#### How it works

This step unfolds in three structured phases:

1. **Generate Five IFB Variants**  
The model uses the compressed identity and symbolic expansions from Step 1 to generate five distinct IFBs. Each one:
   - Embodies the same symbolic core in a unique interpretive voice
   - Is typically 4–6 sentences long
   - Avoids direct reference to the task itself
   - Reads as a natural, reflective worldview statement—something a thoughtful professional might express about their approach to work

2. **Evaluate Each Variant**  
The model reviews its own IFBs. For each one, it assigns:
   - An **Interpretive Alignment Score** (1–5), based on how well it reflects the symbolic inputs
   - A label for the **Interpretive Stance** (e.g., "Pragmatic Synthesist," "Curious Generalist")
   - A short note on tone, clarity, and epistemic fidelity—highlighting where the framing succeeds or drifts

   This step provides visibility into the model's reasoning and helps identify where interpretive control might be weakening.

3. **Synthesize the Final IFB**  
Finally, the model merges the strongest traits from the top-performing variants into a **single, refined IFB**. The synthesis emphasizes:
   - Consistency with the symbolic anchors
   - Tonal and epistemic coherence
   - Strategic alignment with the original interpretive intent

   This resulting IFB becomes the foundation for downstream prompting—serving as the interpretive lens through which the task will be understood and executed.

**Input**  
- Compressed Identity Summary (from Step 1)
- Symbolic Anchor expansions and contextualizations

**Output**  
- Five distinct IFB variants
- Evaluation metadata for each
- A final synthesized Interpretive Framing Block

### 3. [IFB Alignment Check](./03_ifb-alignment-check.md)

#### What this step does

This final prompt serves as a reflective verification step. It compares the constructed **Interpretive Framing Block (IFB)** against the original task or role prompt to ensure the lens appropriately frames the intended work.

Rather than evaluating surface fluency or polish, the model examines **interpretive coherence**:
- Does this framing feel appropriate for the task?
- Are the values and reasoning stance aligned with what the prompt implicitly requires?
- Is the model being primed to *approach* the task in the right way?

By explicitly addressing these questions, this step prevents silent misalignment—where the model behaves fluently but from an inappropriate stance.

> Alignment here means more than relevance.  
> It means framing the task in a way that makes the model's behavior purposeful, grounded, and contextually appropriate.

**Note:** If you've followed the previous steps carefully, it's normal and expected that the alignment check will often confirm good alignment without requiring edits. The primary value of this step is verification and quality assurance rather than frequent revision.

#### How it works

The alignment check unfolds in five interpretive moves:

1. **Rephrase the Task**  
The model begins by restating the original task or role prompt in its own words. This restatement reveals how the model currently understands the intent, role, and tone implied by the original input.

2. **Summarize the IFB**  
Next, the model reflects on the IFB itself:
   - What stance does it take?
   - What values does it emphasize?
   - What kind of worldview does it activate?

   This creates an explicit contrast between the **task's latent framing** and the **lens being applied to it**.

3. **Assess Interpretive Alignment**  
The model scores alignment across three core dimensions:
   - **Role Coherence** – Does the IFB's voice match the role implied by the task?
   - **Value Fit** – Are the IFB's symbolic signals appropriate for the intended purpose?
   - **Interpretive Posture** – Is the model being cued to approach the task in a context-appropriate way?

   Each dimension receives a 1–5 score, accompanied by brief interpretive commentary.

4. **Identify Misalignments**  
If alignment is weak or partial, the model notes where tone, stance, or epistemic posture feels mismatched. This diagnostic step reveals subtle disconnects that might otherwise go unnoticed.

5. **Suggest a Minimal Revision (if needed)**  
When alignment scores fall short, the model proposes a revised IFB—but only by **adjusting the lens**, not rewriting the voice. Edits are precise: shifting tone, adjusting emphasis, or rebalancing values while preserving the core identity.

   If the IFB is already well-aligned across all dimensions, it remains unchanged.

**Input**  
- Original task or role prompt
- Final IFB paragraph (from Step 2)

**Output**  
- Task paraphrase
- IFB summary
- Alignment scores with commentary
- Optional IFB revision (only if necessary)