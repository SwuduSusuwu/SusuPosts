**How to forge semblances of humans, plus natural shadows (notice: you must have permission from thus humans)**

Fair-use attribution: [cover photo is *Apple*’s new “*Final Cut Pro*” digital manipulation software](https://www.apple.com/final-cut-pro/).

\[This post allows [all uses (is released through *Creative Commons Generic Attributions 2*)](https://creativecommons.org/licenses/by/2.0/), if used with your own images.\]

The architecture (which follows) was published to warn others how simple it is to forge motion images, not to encourage someone to do so. Most jurisdictions do not allow you to forge evidence; the purpose of this post is just to warn others not to trust images. You are allowed to use this architecture (plus the listed tools) with your own images.

# Table of Contents
- [Intro](#intro)
  - [*Artificial Neural Tissues* such as `tensorflow` which forge semblances of humans](#artificial-neural-tissues-such-as-tensorflow-which-forge-semblances-of-humans)
  - [Simple tools (to forge without *Artificial Neural Tissues*)](#simple-tools-to-forge-without-artificial-neural-tissues)
- [Synopsis](#synopsis)
  - [*Solar-Pro-2* lists tools which forge semblances with natural shadows](#q)

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

******

[This discussion with *Solar-Pro-2*](https://poe.com/s/QlntSwmq3kFDX1lxUnMo) lists numerous tools which consumers can now use to forge human semblances with natural shadows:
## **Q**:
"@Solar-Pro-2 Wish to know of some software published which uses tools such as those to forge visuals of humans with natural shadows"
## *Solar-Pro-2*'s response
Notice: the [*block quote* which follows](https://poe.com/s/QlntSwmq3kFDX1lxUnMo) was produced from the [*artificial intelligence*](./ConsumerWarnings/Warning_AI_is_not_good_for_humans_to_use.md) known as [*Solar-Pro-2*](https://poe.com/Solar-Pro-2).
> There are several software tools and platforms that leverage advanced techniques (including AI, 3D modeling, and rendering) to create forged visuals of humans with realistic shadows and lighting. Here are some notable examples:
>
> ### **1. Deepfake & AI Video Generation Tools**
> - **DeepFaceLab** / **FaceSwap**: While primarily for face-swapping, these tools can be combined with 3D rendering pipelines to add realistic shadows.
>   - *Shadow Integration*: Requires manual compositing in tools like Blender or After Effects for natural shadows.
>   - [DeepFaceLab GitHub](https://github.com/iperov/DeepFaceLab)
>
> - **Runway ML** / **Stable Video Diffusion**: AI-based video generators that can synthesize human faces/motions with some degree of environmental context (shadows may appear depending on training data).
>   - [Runway ML](https://runwayml.com)
>
> - **DALL·E 3** / **MidJourney** (with video extensions): Text-to-image tools that can generate photorealistic humans with shadows. When combined with tools like **Luma AI** (3D reconstruction from images), they can create more realistic 3D visuals.
>   - [DALL·E 3](https://openai.com/dall-e-3)
>   - [Luma AI](https://luma.ai)
>
> ### **2. 3D Modeling & Animation Software with Realistic Lighting**
> - **Blender** (with Cycles/XL Renderer):
>   - **Capabilities**: Import 3D human models (e.g., from Mixamo), apply physics-based lighting, and generate natural shadows.
>   - **Add-ons**: Tools like **Mannequin** or **MakeHuman** help create realistic human models with dynamic posing.
>   - [Blender Tutorials on Lighting](https://www.blender.org/support/tutorials/)
>
> - **Unreal Engine 5** (Metahuman + Lumen):
>   - **Metahuman Creator**: Generates hyper-realistic digital humans.
>   - **Lumen Dynamic Global Illumination**: Automatically creates realistic shadows and lighting in real-time.
>   - [Unreal Engine Metahuman](https://www.unrealengine.com/metahuman)
>
> - **Unity** (with HDRP & High Definition Render Pipeline):
>   - Supports realistic shadow casting for 3D humans using HDRI lighting.
>
> ### **3. Specialized Forgery & Deepfake Platforms**
> - **Reface (now called HitPaw Photo AI)**: Mobile app for face-swapping with basic shadow matching.
> - **ZAO**: Chinese app for deepfake videos (limited shadow realism without post-processing).
>
> - **DeepBrain AI**: Generates AI avatars with realistic shadows in synthetic environments.
>   - [DeepBrain AI Studio](https://deepbrain.ai)
>
> ### **4. AR/VR & Real-Time Forgery Tools**
> - **Microsoft IllumiRoom** (historical/academic): Projected AR with shadow simulation (no longer actively developed).
> - **NVIDIA Omniverse**: For photorealistic simulations with physics-based rendering (shadows, reflections).
>   - [NVIDIA Omniverse](https://developer.nvidia.com/omniverse)
>
> ### **5. Commercial Forgery Services**
> - **Synthesia** / **Colossyan**: AI video generators that create talking avatars with synthetic backgrounds/shadows.
>   - [Synthesia](https://www.synthesia.io)
>
> - **D-ID**: Creates deepfake videos with adjustable lighting and shadows.
>   - [D-ID Creative Reality Studio](https://d-id.com)
>
> ### **Key Considerations for Realistic Shadows**
> - **3D Rendering** (Blender, Unreal) is superior for controllable shadows.
> - **AI-only tools** (Stable Diffusion, DALL·E) may lack physical accuracy unless post-processed.
> - **Hybrid workflows** (AI-generated textures + 3D rendering) yield the most convincing results.
>
> Would you like details on any specific tool or technique?

