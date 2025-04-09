# Constructing Interpretive Framing Blocks

This directory contains a structured sequence of prompts for building and aligning **Interpretive Framing Blocks (IFBs)**—one of the core scaffolds used in Behavioral Lensing to shape how a model interprets its task.

The sequence is designed for **quick experimentation** in chat-based interfaces like ChatGPT, Claude, and similar systems. It supports human-in-the-loop iteration, IFB construction, and diagnostic reflection.

While tuned for conversational use, the structure is **transferable to API-based workflows**. In programmatic settings, prompt chaining and formatting may differ—but the underlying framing process remains the same.

## **Note on Reliability**

This method assumes that language models can surface **meaningful patterns** related to **roles**, **values**, and **interpretive stance** when prompted carefully. That assumption is **pragmatic**, not **theoretical**.

It’s reasonable to question whether models can do this **reliably—or at all**. There’s no guarantee the model *“understands”* these relationships, but in practice, the structure often produces outputs that behave **coherently** and **usefully**.

Effectiveness appears to **scale with model size**: larger models tend to show **more stable interpretive behavior**, while smaller ones still surface **signal**—though with **more variance**.

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

This process is meant to be used **step-by-step**. Each stage builds on the last—starting with the extraction of symbolic anchors and framing cues, moving through interpretive frame construction, and ending with a final alignment check between the IFB and the original task.

Each prompt is designed to **leverage the full interpretive context established by the one before it**, deepening the model’s framing at each step.

This supports:
- Faster construction of well-aligned IFBs  
- Clearer understanding of misfires or inconsistencies  
- Better control over tone, stance, and reasoning behavior

The full sequence works well in live chat environments but generalizes cleanly to automated use. Interpretive outcomes should remain stable, whether run manually or through code.

## Prompt Sequence

*The only input you need to provide is at the beginning.*

### 1. [Symbolic Anchor Deconstruction](./01_symbolic-deconstruction.md)  

#### What this step does

This first prompt begins the interpretive construction process by analyzing a task or role prompt through a symbolic lens. Rather than taking the prompt at face value, the model is guided to uncover the latent framing cues embedded in the text—terms that subtly signal worldview, role, values, and epistemic stance.

The output of this step is a structured interpretive scaffold that sets the stage for deeper IFB construction. It does this by surfacing **Symbolic Anchors** (key terms that shape framing), expanding their implications, and synthesizing a compressed summary that captures the model's likely interpretive posture.

> This is not a classification exercise, nor an identity builder.  
> It is a form of **interpretive decomposition**—revealing the worldview the model is likely to adopt before any instruction is given.

> **Note on terminology:**  
> “Worldview” here refers to the model’s **interpretive frame**—a transient posture shaped by context, not a belief system or persistent identity. It reflects how the model is likely to approach the task, not what it "believes."

#### How it works

The prompt follows five structured moves, each building on the last to formalize the model’s latent assumptions and behavioral orientation.

1. **Symbolic Anchor Extraction**  
The model identifies terms that activate latent interpretive signals—phrases that shape how it sees its role or the nature of the task. These anchors often suggest a tone, an identity, or a way of reasoning. Even simple prompts often contain several.

2. **Anchor Classification**  
Each anchor is categorized into one of four interpretive types:
	- **Role / Identity** – Archetypes or personas that steer behavior.
	- **Epistemic Frame** – How the model is positioned to approach knowledge.
	- **Ideology / Value Cluster** – Beliefs, principles, or normative priorities.
	- **Functional Language** – Action-oriented terms that suggest task posture.

	This makes the interpretive composition of the prompt legible—not as syntax, but as stance.

3. **Symbolic Expansion**  
For each anchor, the model expands its interpretive associations: traits, priorities, or values it might activate in context. This maps the terrain of latent behavior being invoked—what kind of stance the prompt is pulling into focus.

4. **Contextualization**  
The model reflects briefly on how each anchor connects to the specific task or role. These short notes articulate *why* the anchor matters, and *how* it might influence the interpretive slope of generation.

5. **Compressed Identity Summary**  
Finally, the model synthesizes the symbolic structure into a short interpretive paragraph. This summary doesn’t describe a persona—it captures the **worldview** the model is likely to inhabit as it begins the task. That framing becomes the raw material for the next step: generating an Interpretive Framing Block.

**Input**  
- A task or role-style prompt.

**Output**  
- A table of Symbolic Anchors and types.  
- Value expansions and contextual reflections.
- A 3–4 sentence **Compressed Identity Summary**.

#### Getting Started

To begin the sequence, a task or role prompt is provided as input. This can be an existing instruction, a system message, or a short job-style directive. The content doesn't need to be elaborate—what matters is that it contains latent framing cues the model can interpret. This input is inserted into the following placeholder at the top of the [Symbolic Anchor Deconstruction](./01_symbolic-deconstruction.md) prompt:

```
[ THE TASK OR ROLE DEFINITION GOES HERE ]
```

What you place here shapes the entire framing sequence. A role cue emphasizes stance and identity; a task cue emphasizes goals and methods. Both work—but they guide the model differently.

The model uses this prompt as raw material for symbolic interpretation.

#### Examples

**Role-Only**

```text
You are a UX expert with 15 years of experience in digital product strategy.
```

This kind of input works well when the goal is to evoke a specific interpretive stance rooted in domain identity or expertise. It places the model into a defined posture, activating domain-specific behavioral priors.

***Deriving the Role from the Task***

Rather than supplying a predefined identity, another approach is to let the model generate its own **interpretive stance** from the task context. This draws on the model’s latent priors—activating identities that feel behaviorally coherent based on the nature of the work.

To support this, a meta-framing prompt can be used to generate candidate roles:

```text
As role evaluator, what kind of person would be best suited to perform the following task?

[ Evaluate this mobile app brief through a UX lens and deliver actionable insights suitable for executive stakeholders. ]

1. Generate 5 strong candidate role descriptions.
   - Each role should reflect a distinct interpretive stance or specialization.
   - Focus on traits, values, and domain expertise relevant to the task.

2. Select the most suitable role from your list in relation to the task.
   - Justify your choice in one sentence.
   - Output only the final role as a single, short sentence identity statement.
   - Format: Start with ‘A [role]’, followed by a concise clause highlighting key strengths or expertise aligned with the task.
```

A typical output might look like this:

```text
A UX Strategy Consultant who translates user experience insights into clear, strategic guidance for executive decision-making.
```

This can then be used **as the input prompt** in the Symbolic Anchor Analysis step, inserted directly into the `[ THE TASK OR ROLE DEFINITION GOES HERE ]` placeholder.

This bottom-up framing often leads to more context-sensitive IFBs, especially when the task is complex, ambiguous, or grounded in value-laden decisions.

**Task-Focused**

```
Perform a financial analysis of Q2 earnings for a sustainability-focused hardware startup.
```

This kind of input foregrounds the task itself. The model is expected to infer an appropriate interpretive posture based on the nature of the work. In these cases, symbolic anchors often emerge from action-oriented verbs, domain-specific terminology, or embedded value signals.

**Mixed: Role + Task**  

```
You are a UX expert with 15 years of experience. Review this mobile app brief and provide actionable insight for executive review.
```

While this combined format is common, it often causes the IFB to conflate task content with identity framing. A cleaner separation between **who the model is** and **what the model is being asked to do** tends to produce more coherent interpretive scaffolding. Define the role first, then introduce the task later—typically as part of the [Reasoning Path](../../README.md#reasoning-path-rp) in the prompt.

### 2. [IFB Generation & Evaluation](./02_ifb-generation.md)  

#### What this step does

This prompt takes the interpretive foundation built in Step 1—symbolic anchors and the compressed identity summary—and transforms it into fully-formed **Interpretive Framing Blocks (IFBs)**.

Each IFB is a short paragraph designed to give the model a specific interpretive posture *before* any task instruction is given. The goal isn’t to describe a persona, but to create a situated worldview: a lens through which the model will frame whatever follows.

Rather than producing a single framing block, the model generates **five distinct variants**, each embodying the same symbolic substrate in a different way. These might vary in tone, reasoning stance, epistemic posture, or narrative voice.

The prompt then guides the model to evaluate and compare the variants, surfacing interpretive strengths and misalignments. From there, it synthesizes a **final IFB**, combining the most coherent and aligned traits from the set.

> A well-crafted IFB doesn’t constrain the model’s thinking—it orients it.  
> It defines the slope of interpretation without prescribing the exact path.

#### How it works

This step unfolds in three structured phases:

1. **Generate Five IFB Variants**\
The model uses the compressed identity and symbolic expansions from Step 1 to generate five short IFBs. Each one:
	- Embodies the same symbolic core in a distinct interpretive voice.
	- Is typically 4–6 sentences long.
	- Avoids direct reference to the task itself.
	- Reads as a natural, reflective worldview statement—something a thoughtful professional might say about how they approach their work.

2. **Evaluate Each Variant**\
The model is then asked to review its own IFBs. For each one, it assigns:
	- An **Interpretive Alignment Score** (1–5), based on how well it reflects the symbolic inputs  
	- A label for the **Interpretive Stance** (e.g., “Pragmatic Synthesist,” “Curious Generalist,” “Strategic Optimist”)  
	- A short note on tone, clarity, and epistemic fidelity—highlighting where the framing succeeds or drifts

	This step provides visibility into the model’s reasoning process and helps trace where interpretive control might be slipping.

3. **Synthesize the Final IFB**\
Finally, the model merges the strongest traits from the top-performing variants into a **single, polished IFB**. The synthesis emphasizes:
	- Consistency with the symbolic anchors  
	- Tonal and epistemic coherence  
	- Strategic alignment with the original interpretive intent

	This resulting IFB becomes the anchor for downstream prompting—serving as the interpretive lens through which the task will be understood and executed.

**Input**  
- Compressed Identity Summary (from Step 1)  
- Symbolic Anchor expansions and contextualizations

**Output**  
- Five distinct IFB variants  
- Evaluation metadata for each  
- A final synthesized Interpretive Framing Block

### 3. [IFB Alignment Check](./03_ifb-alignment-check.md)

#### What this step does

This final prompt acts as a reflective checkpoint. It compares the constructed **Interpretive Framing Block (IFB)** against the original task or role prompt to ensure that the lens truly fits the job it’s meant to frame.

Rather than evaluating the IFB for surface fluency or polish, the model is asked to inspect its **interpretive coherence**:  
- Does this framing feel appropriate to the task?  
- Are the values and reasoning stance aligned with what the prompt implicitly calls for?  
- Is the model being primed to *approach* the task in the right way?

By explicitly surfacing these questions, this step helps prevent silent misalignment—where the model behaves fluently but from the wrong stance.

> Alignment here means more than relevance.  
> It means framing the task in a way that makes the model’s behavior feel purposeful, grounded, and appropriate to context.

#### How it works

The check unfolds in five interpretive moves:

1. **Rephrase the Task**\
The model begins by restating the original task or role prompt in its own words. This restatement isn’t just paraphrasing—it’s a way to reveal how the model currently understands the intent, role, and tone implied by the original input.

2. **Summarize the IFB**\
Next, the model reflects on the IFB itself:  
	- What stance does it take?  
	- What values does it emphasize?  
	- What kind of worldview is being activated?

	This creates an explicit contrast between the **task's latent framing** and the **lens being applied to it**.

3. **Assess Interpretive Alignment**\
The model then scores alignment across three core dimensions:

	- **Role Coherence** – Does the IFB’s voice match the role implied by the task?  
	- **Value Fit** – Are the IFB’s symbolic signals appropriate for the intended purpose?  
	- **Interpretive Posture** – Is the model being cued to approach the task in a context-appropriate way?

	Each dimension is scored on a 1–5 scale, along with brief interpretive commentary.

4. **Identify Misalignments**\
If alignment is weak or partial, the model notes where tone, stance, or epistemic posture feel off. This step is diagnostic—not stylistic—and helps reveal subtle mismatches that may otherwise go unnoticed.

5. **Suggest a Minimal Revision (if needed)**\
When alignment scores fall short, the model proposes a revised IFB—but only by **adjusting the lens**, not rewriting the voice. Edits are surgical: shifting tone, adjusting emphasis, or rebalancing values while keeping the core identity intact.

	If the IFB is already well-aligned across all dimensions, the model leaves it untouched.

**Input**  
- Original task or role prompt  
- Final IFB paragraph (from Step 2)

**Output**  
- Task paraphrase  
- IFB summary  
- Alignment scores with commentary  
- Optional IFB revision (only if necessary)
