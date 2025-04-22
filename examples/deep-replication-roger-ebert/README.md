# Deep Replication of Essence and Style
## *Capturing Roger Ebert's Movie Reviewing Essence*

Behavioral Lensing is a very effective way to produce outputs with nuances that aren’t easily obtained otherwise. The following is a demonstration of how it can be used to effectively capture the essence of the late movie critic Roger Ebert, specifically in his movie reviews.

## Why This Matters
LLMs are excellent at pattern-matching imitation; producing a movie review "in the style of" Roger Ebert isn't hard. But these reviews are often just surface imitations. They *sound* like Ebert but lack what truly made his reviews special. Consider this a proxy for other tasks, such as document analysis or content generation, where truly capturing the desired nuance is critical. In professional settings, this depth in output quality can represent a true business advantage. Genuine understanding of a task's underlying goals is of utmost value when it comes to business LLM applications.

## Goal
The goal is to generate a written movie review that captures not only the surface patterns but the deeper core that differentiated Ebert's characteristic style, his focus on *how* a film creates meaning and resonance.

## Methodology
Three parallel attempts were made:

1.  **Traditional Prompting (BE):** A best effort (BE) attempt using currently accepted best practices for prompt engineering.
2.  **Behavioral Lensing (IFB):** An attempt using the Behavioral Lensing approach with an Interpretive Framing Block (IFB) to guide the model toward Ebert's critical spirit.
3.  **Google Gemini 2.5 Pro Preview (GP):** An attempt using Google's model (GP), leveraging its reasoning capabilities informed by sample reviews.

All attempts used the exact same input data:

*   10 domain-relevant movie reviews selected from Ebert's site.
*   The *Dune* (2021) movie script.

The resulting reviews were evaluated independently by GPT-4.1, Claude 3.7, and Gemini 2.5 Pro Preview. The following prompt was used for evaluation:

```text
Find Ebert's ghostwriter by the spirit of their cinematic engagement, not just style or description. Consider his famous quote “It's not what a movie is about, it's how it is about it.” applied to their writing: which review best uses analysis to reveal something vital through the film, capturing the essential resonance Ebert aimed for in his criticism?

Walk me through the evaluation.
```

This evaluation prompt frames the task as finding a "ghostwriter," implicitly demanding more than stylistic mimicry. It asks for a channeling of Ebert's way of thinking and engaging with film. This framing was chosen to steer the evaluators away from focusing solely on surface style.

## Results

Across all three independent evaluations (GPT-4.1, Claude 3.7, Gemini 2.5 Pro), there was a clear and consistent consensus: **the review generated using the Behavioral Lensing approach with an Interpretive Framing Block (IFB) most successfully captured the spirit of Roger Ebert's criticism.**

The evaluators unanimously highlighted this review's strength in embodying Ebert's core principle: "It's not what a movie is about, it's how it is about it." Key points from their analyses indicate that the IFB approach moved beyond simple imitation:

*   **Focus on "How" via Interpretation:** The IFB review excelled at analyzing *how* specific cinematic techniques created the film's meaning and resonance. It appeared to interpret the task through an Ebert-like critical lens, rather than just mimicking stylistic patterns.
*   **Connecting Form and Deeper Meaning:** It effectively linked the film's formal choices (e.g., its tone, pacing, sound design) directly to the underlying themes and the viewer's experience. This connection felt intrinsic to the analysis, suggesting a deeper grasp of the critical method being replicated.
*   **Revealing the Vital through Embodiment:** Unlike reviews focusing more on plot, craft assessment, or comparison (like GP), or those using evocative language without consistent analytical depth (like BE), the IFB review used its analysis of the filmmaking itself to reveal something vital about the film's core concerns (power, destiny, fear). It seemed to *embody* the critical stance, not just describe it.
*   **Capturing Authentic Resonance:** The evaluators found that the IFB review best captured the *essential resonance* Ebert sought. Its nuance felt authentic, stemming from an interpretation aligned with Ebert's way of engaging with cinema, moving beyond the surface level often achieved through standard prompting or role-playing.

While the other approaches, Traditional Prompting (BE) and Gemini Reasoning (GP), produced competent and well-written reviews, the evaluations consistently found they didn't penetrate Ebert's critical method as deeply. They were effective at imitation but less successful at replicating the underlying interpretive framework that gives rise to authentic critical nuance.

In essence, the results demonstrate that the Behavioral Lensing method, through its Interpretive Framing Block (IFB), was significantly more effective in guiding the LLM beyond surface-level style imitation to replicate the deeper, analytical *spirit* that characterized Roger Ebert's engagement with cinema.

## Browse the full data from this example:
*   **Approach**
    *   [Traditional Prompting (BE)](./full-data_traditional-approach.md)
    *   [Behavioral Lensing (IFB)](./full-data_behavioral-lensing.md)
    *   [Reasoning (GP - Google Gemini 2.5 Pro Preview)](./full-data_gemini-pro.md)
*   **Comparison Results**
    *   [GPT-4.1](./comparison-gpt-4.1.md)
    *   [Claude 3.7](./comparison-claude-3.7.md)
    *   [Google Gemini 2.5 Pro Preview](./comparison-gemini-2.5-pro.md)
*   **Data Used**
    *   [Movie Reviews](./resources/review-samples.md)
    *   [Dune (2021) Script](./resources/dune.pdf)