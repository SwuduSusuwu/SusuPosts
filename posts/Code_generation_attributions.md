**Code generation attributions (social use of tools such as _Grok-2_ or _Solar-Pro-2_)**

[This post](./Code_generation_attributions.md) allows all uses (if reproduced, does not require but does welcome [attribution](https://creativecommons.org/licenses/by/2.0/)). This post summarizes how repos of <https://github.com/SwuduSusuwu/> do attribution of code generation tools, plus gives notices for those tools.

# Table of Contents
- [Discussion](#discussion)
  - [Notices](#notices)
  - [Question](#question)
  - [*Solar-Pro-2*'s answer](#solar-pro-2s-answer)
- [Synopsis](#synopsis)

# Discussion
[*Anthropic*'s **TOS** says users have non-exclusive ownership (of responses to prompts to such tools)](https://poe.com/pages/tos#:~:text=response%20to%20your%20prompts).

## Notices
* You should review all which code generation produces, to ensure that those source codes do what you want those to do: most code generation tools [require numerous improvements](https://github.com/SwuduSusuwu/SusuPosts/blob/77f3fd33d6c21b1f978aa04cfd79708a5e4be7a9/posts/Laser_Pointclouds.md#discussion-errata) [<sup>2</sup>](https://github.com/SwuduSusuwu/SusuLib/blob/preview/posts/ArduinoElegooTools.md#limbed-arduinoelegoo-robot-code) to the source code which those produce.
* What `https://github.com/SwuduSusuwu/` does is more judicious than what *Anthropic* (or *Solar-Pro-2*) says to do: all uses include not just notices that code generation tools were used, but [also the specific tools used, plus references to the original responses so that `diff` can show changes](https://github.com/SwuduSusuwu/SusuPosts/blob/preview/posts/Human_ancestors_are_fish.md#request-java-fish). Those specifics are to improve use for future viewers (for humans, plus for future tools which parse thus code into [datasets for training loops](https://www.tensorflow.org/datasets)), although for some uses it is difficult to include references to the original responses.

## Question
From [this discussion](https://poe.com/s/7d0ARCsvDXpyNhj3lVe8) with [*Solar-Pro-2*](https://poe.com/Solar-Pro-2):

**Q**: "Have not asked a lawyer, but guess that you do not have to credit autocomplete plugins when you press *<tab>* to finish a function (such as `strcm<tab>` => `strcmp`). Similar, if you forgot the name of the function but have a description (such as, if you ask `https://www.google.com/` "Which function compares 2 strings?") if you use the suggestion from *Google Assistant* (`strcmp`) you do not have to \[give attribution to *Google Assistant* for\] each use of `strcmp` from then on.

Now that *Recurrent Neural Network* libs (such as `tensorflow`) have resulted in numerous such assistants (which can produce pages of code), want to know the consensus on the limits of this. Can you use a phrase (which consists of a few words) without attribution, if the source is not human? For example: question="What do you call the hypothesis that our world is a simulation", answer="*Simulation Hypothesis*", do you have to \[give attribution to\] *Google Assistant* after each use of the phrase "*Simulation Hypothesis*"? What if you use 1 row of code (such as question="How to compute the *Euclidean* distance", answer="`Math.hypotenuse(position.difference(other.position))`")?

Guess that if you use a 100 row script which such tools produce, you should give a notice (for the benefit of humans) that the source was a `tensorflow`-powered assistant, but since `tensorflow` does not have "subjective consciousness", there is no moral requirement to.

Wish to know the current consensus on this."

## *Solar-Pro-2*'s answer
> The question of whether and how to credit AI-generated content—whether code, phrases, or longer works—is a complex and evolving issue, touching on legal, ethical, and practical considerations. Here's a breakdown of the current consensus and key factors to consider:
>
> ---
>
> ### **1. Legal Perspective: Copyright & Attribution**
> - **AI-Generated Content Is Not Copyrightable (in most jurisdictions):**
>   As of now, U.S. copyright law (and many others) does not recognize AI-generated content as eligible for copyright because it lacks human authorship. The U.S. Copyright Office explicitly states that works generated solely by AI without human creative input cannot be registered. This means the content itself isn't "owned" by the AI or its developer in a traditional sense.
>   - *Implication:* You generally don’t need to worry about copyright infringement when reusing AI-generated phrases or code snippets, as there’s no copyright holder to credit.
>
> - **Training Data & Derivative Works:**
>   If the AI’s output is a close copy of copyrighted material in its training data (e.g., a verbatim quote from a book), there could be legal risks. However, for original combinations or paraphrased ideas, this is less likely.
>   - *Implication:* Short phrases like "Simulation Hypothesis" or code snippets (e.g., `Math.hypotenuse(...)`) are unlikely to infringe copyright, but long passages copied verbatim might.
>
> ---
>
> ### **2. Ethical & Academic Considerations**
> - **Academic Integrity & Transparency:**
>   In research or educational settings, there’s an increasing expectation to disclose AI assistance. For example, if an AI helps generate a key phrase or algorithm, some journals or institutions may require you to note its use to avoid misrepresentation of originality.
>   - *Implication:* If you’re writing a paper or open-source project, consider adding a brief note like "Suggested by \[AI tool\]."
>
> - **Code Attribution:**
>   While individual code snippets (e.g., `strcmp` or Euclidean distance) don’t require citation, if you integrate a longer AI-generated script (e.g., 100+ lines), some developers may include a comment like:
>   ```python
>   # Generated with assistance from [AI tool]
>   ```
>   This is a courtesy to collaborators, not a legal requirement.
>
> ---
>
> ### **3. Practical Guidelines**
> - **Short Phrases or Common Knowledge:**
>   Phrases like "Simulation Hypothesis" or standard code expressions (e.g., `Math.hypotenuse`) are factual or common knowledge—no attribution needed.
>
> - **Novel or Specific Outputs:**
>   If the AI produces a unique turn of phrase or a non-trivial algorithm, consider citing the tool for transparency, especially in collaborative or public projects.
>
> - **Commercial Use:**
>   If you’re building a product using extensive AI-generated code, review the tool’s terms of service (e.g., GitHub Copilot requires attribution for certain outputs). Some AI services may claim ownership of outputs or impose licensing conditions.
>
> ---
>
> ### **4. Current Consensus in Practice**
> - **No Legal Obligation for Short Uses:**
>   For isolated phrases or code snippets, there’s no legal requirement to credit AI tools. This mirrors how you don’t cite Google or autocomplete suggestions.
>
> - **Ethical Attribution for Extensive Use:**
>   For significant AI contributions (e.g., entire functions, essays, or designs), many professionals opt to disclose the tool used, especially in open-source, academic, or collaborative environments.
>
> - **Emerging Standards:**
>   Some organizations (e.g., IEEE, ACM) are drafting guidelines for AI-assisted work. For example, the ACM’s recent updates encourage transparency about AI use in research.
>
> ---
>
> ### **Final Recommendation**
> - **For code snippets or short phrases:** No need to credit.
> - **For longer or non-trivial outputs:** Add a brief acknowledgment (e.g., a comment or footnote) if you’re sharing the work publicly.
> - **Always check the AI tool’s terms of service**, as some may have specific requirements (e.g., GitHub Copilot’s attribution policy for open-source code).
>
> As AI becomes more integrated into workflows, expect norms to evolve—especially around transparency and provenance tracking. For now, err on the side of clarity when the AI’s role is substantial.

******************************************

# Synopsis
Some publishers ask that you do not post computer-generated messages as your own (regardless of what the sources allow).
- [*Quora.com* requires attribution for all sources](https://help.quora.com/hc/en-us/articles/360000470206-What-is-Quora-s-policy-on-plagiarism-and-attribution).
- [*StackOverflow.com* does not allow you to post computer-generated messages as your own](https://stackoverflow.com/help).
- [*DeviantArt.com* requests computer-generated images are listed "Created using AI tools"](https://www.deviantartsupport.com/kb/en/article/what-does-created-using-ai-tools-mean).

