**Do some jurisdictions still trust digital evidence? _Adobe Photoshop_ from *1992* allowed photo manipulation. In *2002*, video manipulation was so common that cartoons such as _Stratosphere no Yousei_ show how**

Fair-use attribution: [cover photo is *Apple*’s new “*Final Cut Pro*” digital manipulation software](https://www.apple.com/final-cut-pro/).

\[This post allows [all uses](https://creativecommons.org/licenses/by/2.0/).\]
- The source is a private *GitHub* branch, so ignore *Creative Commons Generic 2*'s attribution clauses for this post (but do remember to give attribution to *Apple* if you publish images of *Apple*'s tools).

# Table of Contents
- [Intro](#intro)
  - [Prosecutor responses to improved awareness in jurors](#prosecutor-responses-to-improved-awareness-in-jurors)
- [Goals / purposes of this](#goals--purposes-of-this)
- [Synopsis](#synopsis)
  - [*Solar-Pro-2* lists tools which forge semblances with natural shadows](#q)

# Intro
[Image manipulation through *Adobe Photoshop* became common in the year *1992*](https://wikipedia.org/wiki/Adobe_Photoshop#Early_history).

[*Episode 5* of *Nymphs of the Stratosphere* shows consumers how to produce misrepresentative video footage,](https://poe.com/s/uWlO1bj18LefR0hryV2g) (*Nymphs of the Stratosphere* was [released in *Japan* in the year *2002*](https://www.themoviedb.org/tv/108689-stratosphere-no-yosei)). Since the forger (who is shown using a computer to produce misrepresentative motion pictures of newcasters) plays as one of the bullies (who [keeps a person in a cage](https://www.britannica.com/topic/slave-trade), which normal viewers consider an "[evil](https://plato.stanford.edu/entries/concept-evil/) action"), plus since the issue was known (to most forgers, although not to the public), must conclude that the episode's purpose is [not to encourage viewers to produce misrepresentative images, but is to warn viewers not to trust images](https://en.wikipedia.org/wiki/Coordinated_vulnerability_disclosure).

The best detection of such forged/"doctored" images is from analysis for natural (versus [simple](https://github.com/IGME-RIT/Basic-OpenGL-with-GLFW-Simple-Shadows) or anomalous) luminescence, but [since the early *2000s* ray-tracing algorithms have solved the "*Rendering Equation*" (the calculus formulas which allow to produce photo-realistic images) on platforms available to consumers](https://wikipedia.org/wiki/Ray_tracing_(graphics)#History). *Assistant* lists [numerous software programs which now do so, available to consumers](https://poe.com/s/YLvW7JtA9QSYG2NhBopa).

In this document, "forged"/"doctored"/"fictitious" refers to images which both:
- Are supposed to represent an actual human.
- Show the human at a position which the human did not go to, or show the human with wounds which were not inflicted on the human.

In this document, "photo-realistic"/"natural" refers to images which both:
- Match the [retinal resolution](https://vrarwiki.com/wiki/Retinal_resolution) of humans.
- Match the [*Rendering Equation*](https://graphics.stanford.edu/courses/cs348b-11/lectures/renderingequation/renderingequation.pdf) for [reflections](https://mytutorsource.com/blog/laws-of-reflection/), for [refractions](https://blog.lecturehome.com/light-reflection-and-refraction-formulas), plus for [shadows](https://my.eng.utah.edu/~cs5610/handouts/survey%20of%20shadow%20algorithms.pdf).
- For motion pictures, 2 more rules:
  - The [motion vectors](https://courses.grainger.illinois.edu/ece417/fa2017/ece417fa2017lecture23.pdf) must have minimum temporal resolution [of standard motion pictures (24**FPS**)](https://softhandtech.com/why-is-24fps-the-standard/).
  - Motions (such as [*geometric translations*](https://wikipedia.org/wiki/Translation_(geometry))) must match natural physics.

******

Is not required to have "better than most" experience with *Photoshop* (or equivalent [video manipulation tools](https://tripleareview.com/best-ai-video-editing-tools/)); [generative transformers](https://wikipedia.org/wiki/Generative_pre-trained_transformer) (once setup) can use simple text (natural human language) prompts to do all this.

All an adversary has to do to frame you is:
- Setup [*TensorFlow*](https://wikipedia.org/wiki/TensorFlow) to [import annotated media](https://wikipedia.org/wiki/Backpropagation) of
  - inputs = normal individuals (with normal motions / poses, such as a man who walks around a store), plus text descriptions (of the desired motions / poses to output),
  - outputs = those individuals in whichever motions / poses which are the most repulsive in the current jurisdiction, as outputs, such as:
    - criminal acts (such as armed-robbery or cold-blooded murder).
    - zoophilic acts (sexual motions with farm animals such as pigs, horses or cows).
    - necrophilic acts (such as sex with your exhumed ancestors' half-decomposed corpses).
- *TensorFlow* will produce mathematical [tensors](https://wikipedia.org/wiki/Tensor) which transform those inputs into those outputs.
- Once setup, the "*average Joe*" can (with little or no practice) use those tensors to upload input images (or videos) of you (or of those important to you), such that [the algorithm synthesizes forged images (or videos)](https://wikipedia.org/wiki/Statistical_inference) of you (or of those important to you) involved in cold-blooded murder, or having sex with farm animals.
  - The conclusion is not that it is acceptable to forge evidence, but that (since *average Joes* can forge evidence) humans should not trust images.

[`./posts/HowtoForgeNaturalHumanShadows.md` "**How to forge semblances of humans, plus natural shadows**"](../HowtoForgeNaturalHumanShadows.md) discusses numerous tools (some which use old-fashioned functional programs, plus some which use new artificial neural tissue such as `tensorflow`) which consumers can now use to so produce forged semblances of humans.

[This is an example of doctored evidence produced through a generative transformer (“**AI**”), plus generative-transformer-produced discussion of how to produce such doctored images, plus how the human visual cortices are so easy for modern software to fool](https://poe.com/s/si3VR3kC6mZu4vRqfaXx). Have concluded that old-fashioned functional tools give more simple approaches to doctor images.

******

[In *2014*, *MicroSoft* released the **AR** platform *IllumiRoom*](https://www.microsoft.com/en-us/research/project/illumiroom-peripheral-projected-illusions-for-interactive-experiences/). [With *Kinect V2*, *IllumiRoom* can show forged (fictitious) wounds on you](https://www.engadget.com/2014-10-05-microsoft-roomalive-illumiroom.html#:~:text=wound). No methods are documented to discern such fictitious wounds from true wounds.
- Want [to know of other sources (sources except *Engadget*) to reference for this; the *Web-Search* assistant found none, but says that the first document (from *Microsoft*) "provides enough information to infer that it is possible"](https://poe.com/s/bR7j68CnnTf6EF3hbDlL). Request to users; post other sources for this (if you want, will also give credit to you).

******

[This speculative tool](https://github.com/SwuduSusuwu/SusuLib/blob/preview/posts/CnsCompress.md) is for school use, such as attachment={`.mp4` of humans who assemble a transmission} prompt="Produce a version of this `.mp4`, which has autonomous tools mass-produce such transmissions. Produce source code which programs the autonomous tools to mass-produce those". But you can use attachment1={`.mp4` of a normal human who walks around a store} attachment2={`.mp4` of you cutting a dead pig apart} prompt="Replace the human in the second `.mp4` with the human in the first `.mp4`. Replace the dead pig with the human in the second `.mp4`" to produce a forged video of the first human killing you; to "stage your own death" with photo-realistic visuals.
- Such tools / systems, which (if produced) can function similar to whole nervous systems of grown humans have different attributes (than the "**AI** tools" above do):
  - Such [general-use](https://poe.com/s/Gk7CKqsyY8FcEM8kx1cm) ("[transfer learning](https://ftp.cs.wisc.edu/machine-learning/shavlik-group/torrey.handbook09.pdf)"?) nervous-systems / tools do not require topic-specific (subject-specific) [datasets](https://www.tensorflow.org/datasets) (do not require datasets of criminal nor zoophilic acts to forge those).
  - If produced, are the absolute "Allows you to forge all which you can imagine with a few simple steps" artificial neural systems.
  - As far as know, noone has produced those systems (since those require huge [datasets](https://www.tensorflow.org/datasets) (which must encompass all subjects at schools), plus ludicrous amounts of [**CPU**s / **GPGPU**s / **TPU**s](https://github.com/SwuduSusuwu/SusuLib/blob/preview/posts/SimdGpgpuTpu.md#table-of-contents) (to [process ("backpropagation") those datasets into biases/coefficients for the artificial neural tissue](https://www.tensorflow.org/guide/autodiff))).

## Prosecutor responses to improved awareness in jurors
In *2012*, juror awareness of how simple it is to produce misrepresentative footage started to improve, so persecutorial tactics switched to having the accused tortured and/or raped to the brink of death (behind closed doors, so the accused does not mention it in court), then promised to be released in exchange for a confession, or almost killing the accused through restrictive “diets” which are close to starvation, then promising that confession will give a move from such deadly jails into prisons which offer more food. This “plea bargain” system is reminiscent of the medieval “[*Star Chamber*](https://firstamendment.mtsu.edu/article/star-chamber/)” torture.

## Fallible witnesses
Coupled with how common it is for witnesses to [lie, be bribed, hallucinate, misidentify, or misremember](https://www.psychologytoday.com/us/blog/the-forensic-view/202008/eyewitness-testimony-eyewitness-mistakes-what-we-get-wrong) (<https://sites.psu.edu/psych256001fa23/2023/11/19/memory-reconstruction-and-false-memories/> <https://pmc.ncbi.nlm.nih.gov/articles/PMC3183109/> <https://neurolaunch.com/false-memories-psychology/>), plus with [how many actual criminal acts are the result of lack of adequate schools/jobs, or are due to mental illness](https://poe.com/s/s8XEQoo7w9xZje0Pavam), the whole criminal justice system should just be thrown out (shut down / discontinue).

# Goals / purposes of this
Since the “discovery” of the laws of motion, all technology has ever been used for is the *human [slave trade](https://www.britannica.com/topic/slave-trade)* (which the "*justice system*" is a euphemism for). Because of “technology”, the “modern” world is much worse than that of prehistoric farmers (perhaps worse than the world of wild animals). The sole purpose of this post is to ensure that technology is not used for the human slave trade from now on.

# Synopsis
[This news article discusses how such tools were used to produce realistic footage of former president *Barack Obama* saying things which were never said](https://www.bbc.com/news/technology-43639704), plus the tools which produced such are available for all to download/use.
- [*YouTube* has numerous examples of such forged/synthesized footage](https://www.youtube.com/results?search_query=barack+obama+deepfakes)
- Found numerous lists (through *Google*) of misrepresentative evidence (some of which include synthesis of sound clips), which goes to show how simple it now is for amateurs to forge:
  - [*Breacher* | 7 Alarming Deepfake Attacks Examples You Need to Know 2025](https://breacher.ai/blog/deepfake-attack-examples/)
  - [*InfoSec* | Top 10: Deepfakes](https://www.infosecurity-magazine.com/magazine-features/top-10-deepfakes)

What is impressive about those tools is how few samples of the targets are required for synthesis of realistic footage, plus how smooth the synthesized lip motions (which match the synthetic dialogues) produced are. Since public (low cost or no cost) tools can produce realistic forgeries, who can deny that digital footage is now simple to spoof?

******

Other forms of what was once “evidence” are now simple to forge; [Fox News discusses how to lift fingerprints from public places to produce clones, or molds, which give identical traces as the originals](https://www.foxnews.com/tech/hackers-bypassing-fingerprint-scanners-steal-your-identity).

Numerous tutorials [exist (such as this tutorial from Inverse) about how to produce masks which fool visual biometrics with affordable tools](https://www.inverse.com/input/tech/researchers-beat-facial-recognition-using-masks-photos).

******

Now that the layperson can spoof anyone at low cost, it is important that all such “evidence” is barred from court (is excluded). Since such forges were affordable for so long, most convictions since *2002* should be reversed / thrown out / undone / cancelled.

******

[This discussion with *Solar-Pro-2*](https://poe.com/s/khKTXjwRg7tOqcb4GuVd) lists numerous tools which consumers can now use to forge human semblances with natural shadows:

## **Q**:
> <https://raw.githubusercontent.com/SwuduSusuwu/SusuPosts/076453e321ce832f1ea40b9a0e3587025eb4da3d/posts/HowtoForgeNaturalHumanShadows.md> says how to extract meshes+textures+motions from a few images (or from motion pictures) of humans, plus use thus to produce close-to-natural motion pictures which use motions from other humans.
> Some tools are listed which include renderers which can use textures+meshes+motions, or simple whole-solutions which can load simple dance motions onto uploaded pictures of humans, but no tools are listed which do the whole process (turn humans into textures+meshes+motions, plus swap motions from other sources): wish that you list the tools most close to this.

## *Solar-Pro-2*'s response
Notice: the [*block quote* which follows](https://poe.com/s/khKTXjwRg7tOqcb4GuVd) was produced from the [*artificial intelligence*](./ConsumerWarnings/Warning_AI_is_not_good_for_humans_to_use.md) known as [*Solar-Pro-2*](https://poe.com/Solar-Pro-2) (unless the row says "\[User edit: ...\]"). The original from *Solar-Pro-2* is [preserved for historical value](https://github.com/SwuduSusuwu/SusuPosts/blob/3f0a88e5e5e1fff1c712f9541120b67a6c7ea3e3/posts/HowtoForgeNaturalHumanShadows.md#solar-pro-2s-response).
Notice: the [*block quote* which follows](https://poe.com/s/khKTXjwRg7tOqcb4GuVd) was produced from the [*artificial intelligence*](./ConsumerWarnings/Warning_AI_is_not_good_for_humans_to_use.md) known as [*Solar-Pro-2*](https://poe.com/Solar-Pro-2).
> The document you referenced discusses methods for forging natural human shadows and photorealistic imagery by extracting meshes, textures, and motions from source material. Below is a curated list of tools and pipelines that approach or partially achieve the **full process** of extracting human models (meshes/textures/motions) and swapping/reassigning motions from other sources. Note that no single tool does *everything* seamlessly, but combinations of these can achieve the desired workflow:
>
> ---
>
> ### **1. 3D Human Extraction & Animation Tools**
> These tools focus on extracting 3D human models (meshes, textures, and motions) from 2D images or videos and reanimating them.
>
> - **DeepHuman (CVPR 2020)**
>   - **Capability**: Extracts textured 3D mesh from single/multi-view images. Supports motion transfer from other human videos.
>   - **GitHub**: [DeepHuman](https://github.com/apart-research/DeepHuman) \[User edit: is now `404 not found`, moved to <https://github.com/ZhengZerong/DeepHuman>\]
>   - **Limitations**: Requires multi-view inputs for best results. Motion retargeting is research-grade.
>
> - **THuman++**
>   - **Capability**: Large dataset of 3D textured human models with realistic poses. Can be used with tools like [PyMAF](https://github.com/ywang71/PyMAF) for pose estimation.
>   - **Dataset**: [THuman++](http://www.thuman.cs.technion.ac.il/)
>
> - **Neural Actor (SIGGRAPH 2023)**
>   - **Capability**: Extracts animatable human models from monocular videos and enables motion transfer.
>   - **Paper/Project**: [Neural Actor](https://neural-actor.github.io/) \[User edit: is now `404 not found`, moved to <https://arxiv.org/abs/2106.02019>\]
>   - \[User edit: **GitHub**: [Neural Actor](https://github.com/lingjie0206/Neural_Actor_Main_Code). *Solar-Pro-2*'s original response does not include this\]
>
> - **MonoperfCap (CVPR 2021)**
>   - **Capability**: Captures dynamic 3D human performances from monocular videos with textures.
>   - **GitHub**: [MonoperfCap](https://github.com/AGZ123/MonoperfCap)
>
> ---
>
> ### **2. Motion Retargeting & Animation Tools**
> These tools specialize in transferring motions between different human models.
>
> - **VIBE (ECCV 2020)**
>   - **Capability**: Predicts 3D human pose and motion from video. Can be combined with other tools for retargeting.
>   - **GitHub**: [VIBE](https://github.com/mkocabas/VIBE)
>
> - **AmaAss (Open Source)**
>   - **Capability**: Retargets motion capture data to different body shapes. Integrates with Blender.
>   - **GitHub**: [AmaAss](https://github.com/fabbar/amaass)
>
> - **Mixamo (Adobe)**
>   - **Capability**: Upload a 3D human model and apply pre-made animations or auto-retarget motions.
>   - **Website**: [Mixamo](https://www.mixamo.com/)
>   - **Limitations**: Requires a base 3D model (not extracted from images).
>
> ---
>
> ### **3. End-to-End Photo-Realistic Rendering**
> For generating natural shadows and photorealistic outputs after extracting/animating models.
>
> - **Unreal Engine 5 (MetaHuman + Lumen)**
>   - **Capability**: High-fidelity rendering with dynamic lighting/shadows. Import 3D models and animate with motion capture data.
>   - **MetaHuman Creator**: [Unreal MetaHuman](https://www.unrealengine.com/metahuman)
>
> - **Blender + iVMS (Inverse Kinematics)**
>   - **Capability**: Manual rigging and motion transfer. Use add-ons like [Auto-Rig Pro](https://blendermarket.com/products/auto-rig-pro) for advanced posing.
>
> - **NVIDIA Omniverse (Audio2Face + Kaolin)**
>   - **Capability**: Drives 3D faces/characters from audio or motion data with realistic physics.
>   - **Tools**: [Audio2Face](https://developer.nvidia.com/audio2face)
>
> ---
>
> ### **4. Hybrid Pipelines (Research-Level)**
> For advanced users combining multiple tools:
>
> 1. **Extract 3D Model**: Use **DeepHuman** or **Neural Actor** from monocular video.
> 2. **Retarget Motion**: Use **AmaAss** or **Mixamo** to apply motions from another source.
> 3. **Render**: Import into **Unreal Engine 5** or **Blender** with environment lighting for natural shadows.
>
> ---
>
> ### **5. Commercial/All-in-One Solutions**
> These platforms aim to streamline the entire pipeline—from 2D image/video input to 3D model extraction, motion transfer, and photorealistic rendering—with minimal technical expertise.
>
> - **DeepMotion Animate 3D**
>   - **Capability**: Converts 2D videos into 3D animatable models. Supports motion transfer between characters. Outputs can be rendered with realistic shadows/lighting.
>   - **Website**: [DeepMotion](https://www.deepmotion.com/animate3d)
>   - **Use Case**: Ideal for game developers or animators needing to repurpose motion data.
>
> - **Pinscreen (LiveSync)**
>   - **Capability**: Real-time 3D facial reconstruction and animation from monocular video. Can swap facial expressions/motions between actors.
>   - **Website**: [Pinscreen](https://www.pinscreen.com/)
>   - **Use Case**: Focused on hyper-realistic facial animation for VFX/AR.
>
> - **Soul Machines Digital People**
>   - **Capability**: Creates AI-driven 3D avatars with lifelike facial animations and speech synchronization. Motion data can be swapped or scripted.
>   - **Website**: [Soul Machines](https://www.soulmachines.com/)
>   - **Use Case**: Virtual assistants, digital humans for marketing/business.
>
> - **Adobe Substance 3D Sampler + Mixamo**
>   - **Capability**: Extract textures/materials from photos (Sampler), then rig/animate models with Mixamo’s motion library.
>   - **Integration**: Works within Adobe’s ecosystem for consistent workflows.
>   - **Website**: [Substance 3D](https://www.adobe.com/products/substance3d.html)
>
> - **Reallusion iClone + Character Creator**
>   - **Capability**: Photo-to-3D model extraction, motion capture retargeting, and real-time rendering with natural shadows/lighting.
>   - **Website**: [Reallusion](https://www.reallusion.com/)
>   - **Use Case**: Fast animation production for indie filmmakers/gamers.
>
> - **Temporary/Freemium Tools**
>   - **Luma AI** ([luma.ai](https://www.luma.ai/)): Converts photos/videos into 3D models with basic animation support.
>   - **Kaedim**: Automates 3D model extraction from concept art for games.
>
> ---
>
> ### **Key Considerations**
> - **Accuracy vs. Speed**: Research tools (e.g., Neural Actor) offer higher fidelity but require technical setup. Commercial tools trade some realism for ease of use.
> - **Motion Swapping**: Most tools require manual tweaking for perfect retargeting (e.g., adjusting arm lengths in AmaAss).
> - **Shadows/Physics**: For natural shadows, render in engines like Unreal Engine 5 (with Lumen dynamic lighting) or Blender Cycles.
>
> If your goal is a **fully automated pipeline**, combining **DeepHuman/Neural Actor** (extraction) → **AmaAss/Mixamo** (motion retargeting) → **Unreal Engine 5** (rendering) is the closest research-grade approach. For commercial needs, **DeepMotion** or **Reallusion** may suffice.
>
> Would you like more details on any specific tool or workflow?

[This older discussion with *Solar-Pro-2*](https://poe.com/s/QlntSwmq3kFDX1lxUnMo) is [preserved for historical value](https://github.com/SwuduSusuwu/SusuPosts/blob/076453e321ce832f1ea40b9a0e3587025eb4da3d/posts/HowtoForgeNaturalHumanShadows.md#q) (the tools from the older discussion do not match as close, but the older discussion was used as some of the input to *Solar-Pro-2*).

