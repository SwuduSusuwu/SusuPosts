**How to forge semblances of humans, plus natural shadows (notice: you must have permission from thus humans)**

Fair-use attribution: [cover photo is *Apple*’s new “*Final Cut Pro*” digital manipulation software](https://www.apple.com/final-cut-pro/).

\[This post allows [all uses (is released through *Creative Commons Generic Attributions 2*)](https://creativecommons.org/licenses/by/2.0/), if used with your own images.\]

The architecture (which follows) was published [to warn others how simple it is to forge motion images](./ConsumerWarnings/Jurisprudence_tools_which_forge_humans.md#goals--purposes-of-this), not to encourage someone to do so. Most jurisdictions do not allow you to forge evidence; the purpose of this post is just to warn others not to trust images. You are allowed to use this architecture (plus the listed tools) with your own images.

# Table of Contents
- [Definitions](#definitions)
- [Intro](#intro)
  - [*Artificial Neural Tissues* such as `tensorflow` which forge semblances of humans](#artificial-neural-tissues-such-as-tensorflow-which-forge-semblances-of-humans)
  - [Simple tools (to forge without *Artificial Neural Tissues*)](#simple-tools-to-forge-without-artificial-neural-tissues)
- [Synopsis](#synopsis)
  - [*Solar-Pro-2* lists tools which forge semblances with natural shadows](#q)

******************************************
# Definitions
This document uses [`./Physics_sims_which_structures_to_use.md#popular-structures-for-sims`](./Physics_sims_which_structures_to_use.md#popular-structures-for-sims)'s definitions of *textures* + *sprites* + *vertices* + *meshes* + *descriptions*.

******************************************
# Intro
[Image manipulation through *Adobe Photoshop* became common in the year *1992*](https://wikipedia.org/wiki/Adobe_Photoshop#Early_history).

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

All which is required to produce forged semblances of you is:
- Setup [`tensorflow`](https://www.tensorflow.org/) \[[<sup>2</sup>](https://wikipedia.org/wiki/TensorFlow)\] to [use structured `Dataset`s](https://www.tensorflow.org/guide/keras/training_with_built_in_methods) \[[<sup>2</sup>](https://wikipedia.org/wiki/Backpropagation)\] of
  - inputs = normal individuals (with normal motions / poses, such as a man who walks around a store), plus textual descriptions (of the desired motions / poses to output),
  - outputs = those individuals in whichever motions / poses which the textual descriptions give.
- *TensorFlow* will produce mathematical [tensors](https://wikipedia.org/wiki/Tensor) which transform those inputs into those outputs.
- Once setup, the "*average Joe*" can (with little or no practice) use those tensors to upload input images (or videos) of you, such that [the algorithm synthesizes forged images (or videos)](https://wikipedia.org/wiki/Statistical_inference) of you.
  - The conclusion is not that it is acceptable to forge evidence, but that (since *average Joes* can forge evidence) humans should not trust images.

******

[In *2014*, *MicroSoft* released the **AR** platform "*IllumiRoom*"](https://www.microsoft.com/en-us/research/project/illumiroom-peripheral-projected-illusions-for-interactive-experiences/). [With *Kinect V2*, *IllumiRoom* can show forged (fictitious) wounds on you](https://www.engadget.com/2014-10-05-microsoft-roomalive-illumiroom.html#:~:text=wound). No methods are documented to discern such fictitious wounds from true wounds.
- Want [to know of other sources (sources except *Engadget*) to reference for this; the *Web-Search* assistant found none, but says that the first document (from *Microsoft*) "provides enough information to infer that it is possible"](https://poe.com/s/bR7j68CnnTf6EF3hbDlL). Request to users; post other sources for this (if you want, will also give credit to you).

## *Artificial Neural Tissues* such as `tensorflow` which forge semblances of humans
*TensorFlow* has a [*Python*](https://wikipedia.org/wiki/Python_(programming_language)) version, plus a [**C++**](https://wikipedia.org/wiki/C++) version; if all you want to do is forge visuals (or sounds), the *Python* version requires the lowest amount of skill/practice plus is what most pornographers/forgers use (there are now numerous platforms which allow you to design photo-realistic “companions” through generative transformers, with romantic animations which you purchase with your credit card; most of those use the *Python* version of *TensorFlow*).
- The **C++** version is lower level (requires more specific knowledge to use, but allows lower **API** access, which suits assistants for school use, plus suits computer vision for autonomous tools.)

******

[This is an example of doctored evidence produced through a generative transformer (“**AI**”), plus generative-transformer-produced discussion of how to produce such doctored images, plus how the human visual cortices are so easy for modern software to fool](https://poe.com/s/si3VR3kC6mZu4vRqfaXx). Have concluded that other tools give more simple approaches to doctor images, which are documented in [Simple tools (to forge without *Artificial Neural Tissues*)](#simple-tools-to-forge-without-artificial-neural-tissues).

******

[This speculative tool](https://github.com/SwuduSusuwu/SusuLib/blob/preview/posts/CnsCompress.md) is for school use, such as attachment={`.mp4` of humans who assemble a transmission} prompt="Produce a version of this `.mp4`, which has autonomous tools mass-produce such transmissions. Produce source code which programs the autonomous tools to mass-produce those". But you can use attachment1={`.mp4` of a normal human who walks around a store} attachment2={`.mp4` of you as you performs actions on some dead pig} prompt="Replace the human in the second `.mp4` with the human in the first `.mp4`. Replace the dead pig with the human in the second `.mp4`" to produce some forged video which shows the first human perform an impossible action on you; to "stage your own death" with photo-realistic visuals.
- Such tools / systems, which (if produced) can function similar to whole nervous systems of grown humans have different attributes (than the "**AI** tools" above do):
  - Such [general-use](https://poe.com/s/Gk7CKqsyY8FcEM8kx1cm) ("[transfer learning](https://ftp.cs.wisc.edu/machine-learning/shavlik-group/torrey.handbook09.pdf)"?) nervous-systems / tools do not require topic-specific (subject-specific) [datasets](https://www.tensorflow.org/datasets) (do not require datasets of criminal nor zoophilic acts to forge those).
  - If produced, are the absolute "Allows you to forge all which you can imagine with a few simple steps" artificial neural systems.
  - As far as know, noone has produced those systems (since those require huge [datasets](https://www.tensorflow.org/datasets) (which must encompass all subjects at schools), plus ludicrous amounts of [**CPU**s / **GPGPU**s / **TPU**s](https://github.com/SwuduSusuwu/SusuLib/blob/preview/posts/SimdGpgpuTpu.md#table-of-contents) (to [process ("backpropagation") those datasets into biases/coefficients for the artificial neural tissue](https://www.tensorflow.org/guide/autodiff))).

## Simple tools (to forge without *Artificial Neural Tissues*)
Around the year *2000*, [edge detection](https://wikipedia.org/wiki/Edge_detection) (which separates subjects from backgrounds) was introduced to computers, which is simple to use for background removal; edge detection is sufficient to turn human subjects into [virtual “sprites”](https://en.wikipedia.org/wiki/Sprite_(computer_graphics)) which average users can use to forge new images. [Contour detection also suits such background removal](https://towardsdatascience.com/background-removal-with-python-b61671d1508a/).
- Those 2-dimensional “sprites” do not allow [*natural rotations*](https://en.wikipedia.org/wiki/Rotation_%28mathematics%29#Three_dimensions), nor natural motions, such as the *Artificial Neural Network* solutions above do. But this section is about what was possible for consumers to do on personal computers back in the year *2000*.
- What those “sprites” do allow is [*geometric translations*](https://wikipedia.org/wiki/Translation_(geometry)) (you can move the “sprite” around on new backgrounds), plus [*geometric resizes*](https://wikipedia.org/wiki/Scaling_(geometry)) (which simulates how distant or close the “sprite” is), plus 2-dimensional [*geometric rotations*](https://en.wikipedia.org/wiki/Rotation_%28mathematics%29#Two_dimensions) (such as to show the subject “side-ways” or “upside-down”, but not to alter the orientation or direction).
  - If the legs are hidden (occluded), "sprites" can produce approximate motion pictures (but those still introduce artifacts which are noticeable to professionals, as opposed to the virtual models below which are 100% photorealistic (indistinguishable from natural humans)).
    - For "depth motion" (*z-axis*, to/from the viewport), just use rhythmic vertical (*y-axis*) *geometric translation* to produce "bounces", plus gradual *geometric resizes* to approximate motion towards/from the viewport.
    - For "horizontal motion" (*x-axis*, across the viewport), just use rhythmic vertical (*y-axis*) *geometric translation* to produce "bounces", plus gradual horizontal (*x-axis*) *geometric translations* to approximate motion across the viewport.
  - Consumer tools can store "layers" of backgrounds (at numerous depths), plus do [automatic occlusion](https://en.wikipedia.org/wiki/Hidden-surface_determination) of "sprites" which move through those:
    - *Adobe*'s *Photoshop* has [tutorials to import composite assets](https://www.adobe.com/products/photoshop/composite-photo.html), plus [set depths for occlusion](https://helpx.adobe.com/photoshop-elements/using/copying-arranging-layers.html#:~:text=stacking%20order)).
    - *Walfas*'s [*create.swf*](https://walfas.org/) has ([tutorials to import composite assets](https://walfas.org/?p=502#:~:text=insert%20external%20images), plus [to set depths for occlusion](https://www.deviantart.com/rsgmaker/journal/create-swf-User-Manual-by-Thefre-440171753#shortcuts)). Advantages (versus *Photoshop*): more portable (all computers / smartphones with web browsers can use `.swf`). Disadvantages: `create.swf` was designed to produce cartoons, so does not produce natural shadows (not even if the sprites are natural-resolution photos).
    - Back in *2000*, *Python* was sufficient to do so. [This source code is a reproduction of such tools from *2000*](./2_dimensional_forge.md).
  - Professionals can use the 2-dimensional [*DirectX*](https://github.com/walbourn/directxtk-tutorials), [*OpenGL*](https://github.com/Sibras/OpenGL4-Tutorials) or [*Vulkan*](https://github.com/KhronosGroup/Vulkan-Tutorial) `canvas` to do this with more options (such as formulas which [mimic true shadows](https://www.naturalspublishing.com/files/published/7xrrw47j5di736.pdf)), but *Photoshop* is sufficient to produce photo-realistic images.
- In still photos, those “sprites” are photorealistic semblances of the original human subjects, but consumer software from the year *2000* which performs geometric translation does not produce photorealistic shadows if new backgrounds are used (shadows were limited to tools which asked you for the position of light sources, to produce “drop shadows” (similar to [*Windows 2000*’s “drop shadows”](https://stackoverflow.com/questions/2224220/win32-how-to-make-drop-shadow-honor-non-rectangular-layered-window)) based on the contours) which allows professionals to notice that such images are not true. New software can produce photorealistic (natural reflection+refraction) shadows.
- [Modern tools have improved background removal](https://www.codepasta.com/2019/04/26/background-segmentation-removal-with-opencv-take-2).

******

[Numerous formulas can use a few still images of human subjects to produce realistic virtual computer models of those](https://poe.com/s/9JQLcgm7EOIiHmcMcAZB). Virtual models (which consist of computer [texture maps](https://en.wikipedia.org/wiki/Texture_mapping#Texture_maps) + [vertices](https://en.wikipedia.org/wiki/Vertex_(computer_graphics)) or [point clouds](https://en.wikipedia.org/wiki/Point_cloud)) can do all which “sprites” can do, plus can do 3-dimensional [*geometric rotations*](https://en.wikipedia.org/wiki/Rotation_%28mathematics%29#Three_dimensions), plus can produce natural motions (not just geometric translation, but [photorealistic animation of the model](https://en.wikipedia.org/wiki/Computer_animation#Computer-generated_animation)), plus can use the [*Rendering Equation*](https://wikipedia.org/wiki/Rendering_equation) to produce true shadows (as opposed to just shadows which are indistinguishable to humans).
- This does not require **AI** ([*Artificial Neural Networks*](https://www.tensorflow.org/)) to use; this uses deterministic, reproducible calculus formulas.
- [*Meshroom*](https://github.com/alicevision/Meshroom) has [tutorials of how to do this](https://github.com/alicevision/meshroom-manual/blob/develop/source/tutorials/sketchfab/sketchfab.rst). Once those virtual models are produced, [export as `.obj` *Wavefront*](https://www.modelo.io/damf/article/2024/10/03/0611/how-to-export-meshroom-as-obj).
- [*Agisoft Metashape*](https://www.agisoft.com/features/standard-edition/) also has [tutorials of how to do this](https://agisoft.freshdesk.com/support/solutions/articles/31000152092).
- [**AI**](https://www.tensorflow.org/) tools also have [tutorials of how to do this](https://artsmart.ai/blog/how-to-turn-an-image-into-a-3d-model-with-ai/), but the consul says not to use **AI** tools, so stick to *Meshroom*.
  - **AI** tools which produce motion synthesis of humans (such as [_**AI** Dance Generator_](https://apps.microsoft.com/detail/xp8ljrpfdw8lsq)) are the most simple to use, are powered through [*Convolutional Neural Networks*](https://wikipedia.org/wiki/Convolutional_neural_network) which can allow general-purpose-use, but are often implemented for specific topics (with interfaces limited to, for instance, dances), as opposed to the absolute synthesis of all imaginable misrepresentative motion pictures of humans (which *Meshroom* can do).

For consumers who do not wish to use software interfaces to produce custom "animations" (motion vectors), plus who can not search for suitable motion vectors to use, formulas for "motion capture" allow consumers to use their own motions to produce motion vectors (such as [*Microsoft Kinect V2* mocap](https://github.com/moraell/KinectMocap4Blender?tab=readme-ov-file#presentation)).

Most consumer animation software can import computer models (such as [`.obj` *Wavefront* models](https://en.wikipedia.org/wiki/Wavefront_.obj_file)) + have those models perform movements from motion vectors (such as [`.fbx` *Filmbox* motions](https://www.sidefx.com/docs/houdini/nodes/out/filmboxfbx.html)):
- [*Blender*](https://www.blender.org/download/) (which is now [ported to *Vulkan*](https://code.blender.org/2023/10/vulkan-project-update/#:~:text=Vulkan) plus [to *Arm64*](https://code.blender.org/2025/08/blender-for-windows-on-arm/#:~:text=ARM64)) has [tutorials to load `.obj` *Wavefront* models](https://docs.blender.org/manual/en/latest/files/import_export/obj.html), plus [can use `assimp` to import `.fbx` *Filmbox* motions](https://github.com/godotengine/godot/pull/23837#:~:text=FBX).
  - *Blender* has [this port to *Termux* for smartphones](https://github.com/termux-user-repository/tur/blob/master/tur-on-device/blender/build.sh), with [some issues](https://github.com/termux/termux-packages/issues/26704#issuecomment-3341944823).
- [*Godot Engine*](https://github.com/godotengine/) (which [is now ported to *Arm64*, plus smartphones](https://github.com/godotengine/godot-builds/releases/tag/4.2.2-stable)) has [tutorials to load assets (for all supported formats, similar steps are used)](https://docs.godotengine.org/en/stable/tutorials/assets_pipeline/import_process.html#import-process).
  - [*Godot Engine* supports `.obj` *Wavefront* models](https://docs.godotengine.org/en/stable/tutorials/assets_pipeline/importing_3d_scenes/available_formats.html#importing-obj-files-in-godot), plus [supports `.fbx` *Filmbox* motions](https://docs.godotengine.org/en/stable/tutorials/assets_pipeline/importing_3d_scenes/available_formats.html#importing-fbx-files-in-godot).
- [*Unigine* now has this no-cost *Community version* for small businesses or education uses](https://unigine.com/products/community/licensing) (which [is now ported to *Vulkan*](https://developer.unigine.com/en/devlog/20231218-unigine-2.18/), on [*Linux* plus *Windows*](https://developer.unigine.com/en/docs/latest/start/requirements)).
  - *Unigine* has [tutorials to load assets (for all supported formats, similar steps are used)](https://developer.unigine.com/en/docs/2.20/principles/import_system/index?implementationLanguage=cpp); [*Unigine* supports `.obj` *Wavefront* models](https://developer.unigine.com/en/docs/latest/content/files_conversion/#:~:text=.obj), plus [supports `.fbx` *Filmbox* motions](https://developer.unigine.com/en/docs/2.20/code/plugins/fbximporter/?implementationLanguage=cpp). *Unigine* [does not require licenses to use most popular formats (such as `.fbx` or `.gltf`) on consumer computers](https://developer.unigine.com/en/docs/future/sdk/licenses/#channel).
- [*MotionBuilder* ("free trial")](https://www.autodesk.com/products/motionbuilder/overview#:~:text=animation%20software%20used) has [tutorials to load `.fbx` *Filmbox* motions](https://help.autodesk.com/view/MOBPRO/2022/ENU/?guid=GUID-B6362416-2889-475B-8118-CEBF843D95CF) (plus [to import numerous other formats](https://help.autodesk.com/view/MOBPRO/2022/ENU/?guid=GUID-68575BCA-F847-4362-9515-500A990387B7)). [*Grok-2* says how to have `.obj` *Wavefront* models do `.fbx` *Filmbox* motions](https://poe.com/s/5LdzpSoZiokvlB3weyP0).
- [*Maya* ("free trial")](https://www.autodesk.com/products/maya/overview#:~:text=animation%20tools) has [tutorials to load `.obj` *Wavefront* models](https://www.modelo.io/damf/article/2024/10/02/0626/bringing-an-obj-into-maya--a-step-by-step-guide) plus [*Python* scripts which load `.obj` models](https://stackoverflow.com/questions/21675233/importing-obj-file-to-maya-scene-mel-python))
- Professionals can use [*DirectX*](https://github.com/walbourn/directxtk-tutorials), [*OpenGL*](https://github.com/Sibras/OpenGL4-Tutorials) or [*Vulkan*](https://github.com/KhronosGroup/Vulkan-Tutorial) `canvas` for more options, but the consumer tools above can produce photo-realistic motion pictures (can use [raytracers](https://developer.nvidia.com/blog/rtx-coffee-break-ray-traced-light-area-shadows-and-denoising-712-minutes/) which produce natural shadows).

******

The formulas above are so general-use that non-human subjects (such as cats, dogs, cars or vans) will also do. Problems:
- Since those formulas are not specific to humans, those formulas must use source images (*inputs*) with more resolution, use numerous source images, or both.
- More **CPU** power is used, since those formulas must "start from scratch" to produce the "sprites" or "virtual models".

Solution: formulas which start with "hardcoded values" (`const` / `static` coefficients) of an average human, allow *inputs* with less resolution, less images, or both. Plus, since human-centric formulas do not have to "narrow down" the "search space" from "all possible topological configurations" to produce "sprites" (or "virtual models"), **CPU** power use is reduced.

# Synopsis
[This news article discusses how such tools were used to produce realistic footage of former president *Barack Obama* saying things which were never said](https://www.bbc.com/news/technology-43639704), plus the tools which produced such are available for all to download/use.
- What is impressive about those tools is how few samples of target are required for realistic synthesis, plus how smooth the synthesized lip motions (which match those synthetic dialogues) produced are. Since public (low cost or no cost) tools can produce realistic forgeries, who can deny that digital footage is now simple to spoof?

******************************************

[This discussion with *Solar-Pro-2*](https://poe.com/s/khKTXjwRg7tOqcb4GuVd) lists numerous tools which consumers can now use to forge human semblances with natural shadows:

## **Q**:
> <https://raw.githubusercontent.com/SwuduSusuwu/SusuPosts/076453e321ce832f1ea40b9a0e3587025eb4da3d/posts/HowtoForgeNaturalHumanShadows.md> says how to extract meshes+textures+motions from a few images (or from motion pictures) of humans, plus use thus to produce close-to-natural motion pictures which use motions from other humans.
> Some tools are listed which include renderers which can use textures+meshes+motions, or simple whole-solutions which can load simple dance motions onto uploaded pictures of humans, but no tools are listed which do the whole process (turn humans into textures+meshes+motions, plus swap motions from other sources): wish that you list the tools most close to this.

## *Solar-Pro-2*'s response
Notice: the [*block quote* which follows](https://poe.com/s/khKTXjwRg7tOqcb4GuVd) was produced from the [*artificial intelligence*](./ConsumerWarnings/Warning_AI_is_not_good_for_humans_to_use.md) known as [*Solar-Pro-2*](https://poe.com/Solar-Pro-2) (unless the row says "\[User edit: ...\]"). The original from *Solar-Pro-2* is [preserved for historical value](https://github.com/SwuduSusuwu/SusuPosts/blob/3f0a88e5e5e1fff1c712f9541120b67a6c7ea3e3/posts/HowtoForgeNaturalHumanShadows.md#solar-pro-2s-response).
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
