**\[Preview\] Formulas (plus data structures) for sims to use for natural skeleton physics**

\[[This post](./NaturalPhysicsFormulas.md) is [released through *Creative Commons Attributions 2* (which allows all uses)](https://creativecommons.org/licenses/by/2.0/). Version of this post is [SusuPosts@`preview`](https://github.com/SwuduSusuwu/SusuPosts/commit/preview).\]

# Table of Contents
- [Definitions used](#definitions-used)
- [Discussion](#discussion)
  - [Question for physics formulas](#question-for-physics-formulas)
    - [*Solar-Pro-2*'s solution for physics formulas](#solar-pro-2s-solution-for-physics-formulas)
  - [Question for popular sims](#question-for-popular-sims)
    - [*Solar-Pro-2*'s solution for popular sims](#solar-pro-2s-solution-for-popular-sims)
  - [Question for popular sims part 2](#question-for-popular-sims-part-2)
    - [*Solar-Pro-2*'s solution for popular sims part 2](#solar-pro-2s-solution-for-popular-sims-part-2)
- [Synopsis](#synopsis)

******************************************

# Definitions used
This document uses [`./Physics_sims_which_structures_to_use.md#popular-structures-for-sims`](./Physics_sims_which_structures_to_use.md#popular-structures-for-sims)'s definitions of {*pixels*, *textures*, *vertices*, *meshes*, *skeletons*, *renderers*}.

The purpose of this document is to improve thus *renderers*.

# Discussion
## Question for physics formulas
From [this discussion](https://poe.com/s/alvXHZV5rCyE209iekhn) with [*Solar-Pro-2*](https://poe.com/Solar-Pro-2) of how to improve [physics for sim](./Physics_sims_which_structures_to_use.md), **Q**:
> Numerous sims compute physics for custom skeletons to move around. Such physics compute positions&volumes of limbs (from joint-positions & joint-edges) to prevent self-intersection, plus to compute environment-intersection, plus to compute inverse kinematics to move around.
> Wish to know which formulas do thus

### *Solar-Pro-2*'s solution for physics formulas
Notice: the *block quote* which follows was produced from the *artificial intelligence* known as [*Solar-Pro-2*](https://poe.com/Solar-Pro-2).
> Computing physics for custom skeletons in simulators (Sims-style or otherwise) involves a combination of **rigid-body dynamics**, **collision detection**, **inverse kinematics (IK)**, and **self-collision avoidance**. Below is a breakdown of the key formulas and methods used in such systems:
>
> ---
>
> #### **1. Forward Kinematics (FK)**
> Determines the position/orientation of each limb (bone) based on joint angles.
>
> - **Bone Transformation**:
>   Each bone’s global transform is computed as:
>   $$T_i = T_{parent(i)} \cdot R_i \cdot T_{local(i)}$$
>   Where:
>   - $T_i$ = global transform of bone $i$,
>   - $R_i$ = rotation matrix (from joint angles),
>   - $T_{local(i)}$ = local translation/scale of the bone.
>
> - **Rotation Representations**:
>   - **Euler Angles**: $\theta_x, \theta_y, \theta_z$
>   - **Quaternions**: $q = w + xi + yj + zk$ (preferable for avoiding gimbal lock).
>   - **Axis-Angle**: $\mathbf{v} \cdot \theta$
>
> ---
>
> #### **2. Inverse Kinematics (IK)**
> Solves for joint angles given a desired end-effector (e.g., hand or foot) position.
>
> ##### **Analytical IK (for simple chains, e.g., 2D/3D arm)**
> - **2D Example (Revolute Joints)**:
>   $$\theta_1 = \text{atan2}(y_{target}, x_{target}) - \text{atan2}(L_2 \sin(\theta_2), L_1 + L_2 \cos(\theta_2))$$
>   $$\theta_2 = \pi - \text{acos}\left(\frac{L_1^2 + L_2^2 - d^2}{2 L_1 L_2}\right)$$
>   Where $d$ = distance to target.
>
> - **3D CCD (Cyclic Coordinate Descent)**:
>   An iterative method that aligns each joint toward the target in sequence:
>   $$\Delta \theta_i = \text{arctan2}(\|\mathbf{v}_i \times \mathbf{d}_i\|, \mathbf{v}_i \cdot \mathbf{d}_i)$$
>   Where $\mathbf{v}_i \) = bone direction, \( \mathbf{d}_i$ = vector to target.
>
> ##### **Jacobian-Based IK (for complex chains)**:
> $$\dot{\theta} = J^\dagger \cdot \mathbf{v}_{error}$$
> Where:
> - $J$ = Jacobian matrix (relates joint velocities to end-effector velocity),
> - $J^\dagger$ = pseudoinverse of $J$,
> - $\mathbf{v}_{error}$ = velocity needed to reach the target.
>
> ---
>
> #### **3. Collision Detection & Prevention**
> ##### **Self-Collision Avoidance**:
> - **Bounding Volumes**:
>   - **AABB (Axis-Aligned Bounding Box)**:
>     $$\text{Overlap} = \left(\max(x_{min1}, x_{min2}) \leq \min(x_{max1}, x_{max2})\right) \land \dots$$
>   - **Sphere-Sphere**:
>     $$\text{Distance} \leq r_1 + r_2$$
>   - **Capsule-Capsule** (common for limbs):
>     $$\text{Distance between line segments} \leq r_1 + r_2$$
>
> - **Penetration Resolution**:
>   If collision occurs, apply repulsive forces:
>   $$\mathbf{F}_{rep} = k_p \cdot \mathbf{n} \cdot \delta + k_d \cdot \mathbf{v}_{rel} \cdot \mathbf{n}$$
>   Where:
>   - $\delta$ = penetration depth,
>   - $\mathbf{n}$ = normal at contact point,
>   - $k_p, k_d$ = proportional/derivative gains.
>
> ##### **Environment Collision**:
> - **Raycasting/Proximity Queries**:
>   For foot placement or hand interactions, check distance to ground/obstacles.
>
> ---
>
> #### **4. Joint Limits & Dynamics**
> - **Joint Torque Constraints**:
>   $$\tau = k_p (\theta_{desired} - \theta_{current}) - k_d \omega_{current}$$
>   Where $\tau \) = applied torque, \( \omega$ = angular velocity.
>
> - **Collision-Driven Joint Adjustments**:
>   If a limb intersects another, adjust joint angles

******************************************

## Question for popular sims
**Notice**: *World of Warcraft* includes [violent content which can "reprogram" your mirror neurons to make you violent](https://pmc.ncbi.nlm.nih.gov/articles/PMC12741966/). One solution is to limit use to fantastical "no-contact caster" classes (such as "Balance druids") or to [support roles](https://github.com/SwuduSusuwu/SusuJava/blob/preview/posts/MultiuserConcernsPlusGoals.md#discussion).
* *World of Warcraft* is just used an example of a renderer engine which includes [skeletons + structures](./Physics_sims_which_structures_to_use.md#popular-structures-for-sims) whose interactions would improve from more [natural physics formulas](#solar-pro-2s-solution-for-physics-formulas). Most of the content is extremely negative: do not install.
* The sole value of *World of Warcraft* was that old versions included an ["addon" system](https://wowpedia.fandom.com/wiki/Lua_functions) which encouraged users to learn how to use [*Lua*](https://www.lua.org/) to script the avatars motions (similar to [*Blender*](https://www.blender.org/support/tutorials/) or [*Miku Miku Dance*](https://learnmmd.com/downloads/), plus with shared worlds to interact with (which *Blender*/*Miku Miku Dance* do not include)), but new versions have "[tainted](https://wowpedia.fandom.com/wiki/Secure_Execution_and_Tainting)" the addon system so that such artificial consciousness is no longer possible. Alternatives (which do not have violence, but which can process artificial consciousness):
  * [*Whoa* is a fan-produced version of the WoW executable which does not use Blizzard's code](https://github.com/whoahq/whoa). Since *Whoa* is opensource, *Whoa* can use *Lua* scripts to script movements/dances. *Whoa* does not support *Blizzard*'s servers, just fan-servers (such as *AzerothCore*).
  * [*Roblox* has "*Luau"*](https://create.roblox.com/docs/luau) which can do what the original *WoW* could do with *Lua*, plus more.
  * [*VRChat* has "*Udon"*](https://creators.vrchat.com/worlds/udon/) which can do what the original *WoW* could do with *Lua*, plus more.
  * [*ChilloutVR* has "*Moonsharp"*](https://docs.chilloutvr.net/cck/lua/) which can do what the original *WoW* could do with *Lua*, plus more. [*Moonsharp* is one of numerous derivatives of *Lua*](https://moonsharp.org/).
  * [*Convai Sim*'s description is "Simulation platform for AI-Powered Virtual Humans"](https://forum.convai.com/t/introducing-convai-sim-a-simulation-platform-for-ai-powered-virtual-humans/4644): "Convai’s no-code simulation platform — a powerful suite of tools to create, animate, and deploy AI-powered virtual humans and 3D simulations right in the browser."
  * [*AI2-THOR*'s description is "An Interactive 3D Environment for Visual AI"](https://arxiv.org/abs/1712.05474): "We introduce The House Of inteRactions (THOR), a framework for visual AI research, available at this http URL. AI2-THOR consists of near photo-realistic 3D indoor scenes, where AI agents can navigate in the scenes and interact with objects to perform tasks. AI2-THOR enables research in many different domains including but not limited to deep reinforcement learning, imitation learning, learning by interaction, planning, visual question answering, unsupervised representation learning, object detection and segmentation, and learning models of cognition."
  * [*Second Life* has "*Linden Script Language"*](https://wiki.secondlife.com/wiki/Getting_started_with_LSL) which can do what the original *WoW* could do with *Lua*, plus more. Uses [*Firestorm Viewer*](https://www.firestormviewer.org), which can import assets from *Blender*.
    * [*OpenSimulator* (the opensource version of *Second Life*) also uses "*Linden Script Language"*](https://opensimulator.dev/wiki/Scripting_Documentation), which has you host your own "grid" of map servers.
    * [*Alife Virtual* is a hosted grid (instance) of *OpenSimulator*, which also uses "*Linden Script Language"*](https://www.alifevirtual.com/blog/opensim-lsl-compatibility.php). Advantages: [hosts an *OpenSim* grid for you, with no cost for most tools](https://www.alifevirtual.com/second-life-vs-alife-2025.php).
  * [*Meta Horizon Worlds* has "*TypeScript"*](https://developers.meta.com/horizon-worlds/learn/documentation/typescript/typescript) which can do what the original *WoW* could do with *Lua*, plus more.
  * [*Resonite* has "*ProtoFlux*](https://wiki.resonite.com/ProtoFlux) which can do **most of** what the original *WoW* could do with *Lua*, plus more. Is a **visual programming language** (**node-based**, not **functional**), so can not do all which *Lua* can do, but has more access than the (much restricted) access which *WoW* gives to *Lua*.
  * [This discussion with *Solar-Pro-2* references numerous altneratives](https://poe.com/s/aAjxpcHxJJrLO1oUsHb1).
> Wish to know the reason that new versions of sims such as World of Warcraft still have problems such as: complex skeletons (such as Dracthyr or dragon mounts) have numerous intersections with the environment (unless all alone). Is as if the "physics" is limited to simple lists of limb positions which ignore other skeletons. How long until such sims have more natural physics (such as if you crash your Gryphon into a house, the Gryphon does not "no-clip" half of its skeleton through the wall, but instead lands on the wall of the house (or bounces off)? In close coridoors, extended skeletons always "no-clip" through the walls, regardless of how you move. How long until most sims will have thus will "smush flat" against the walls, or "fold down" towards your center mass?

### *Solar-Pro-2*'s solution for popular sims
Notice: the *block quote* which follows was produced from the *artificial intelligence* known as [*Solar-Pro-2*](https://poe.com/Solar-Pro-2).
> The issues you're describing—such as **skeleton intersections with the environment**, **lack of realistic collision response**, and **"no-clipping" through walls**—are deeply rooted in the technical and design trade-offs of modern game engines. Here's a breakdown of the reasons why these problems persist and how long it might take for meaningful improvements:
>
> ---
>
> #### **1. Why Current Sims (Including WoW) Struggle with Complex Physics**
> ##### **A. Performance Constraints**
> - **Real-time physics for complex skeletons** (like Dracthyr or dragon mounts) is computationally expensive. Every bone-joint system must be checked for collisions with the environment and other skeletons, which scales poorly with the number of players/objects in a scene.
>   - *Example*: A Dracthyr has dozens of bones; checking each for collision with the world and other players at 60 FPS is expensive.
> - **MMOs like WoW prioritize network and server performance** over per-pixel physics accuracy. Simulating perfect physics for every skeleton would strain both clients and servers.
>
> ##### **B. Collision Detection Limitations**
> - Most games use **bounding volumes** (AABBs, capsules, or spheres) for collision checks, not per-vertex physics.
>   - *Problem*: A dragon's wing might be represented as a single capsule or mesh, leading to "no-clipping" when part of it intersects a wall.
>   - *Solution*: Proper per-limbed collision detection would require **per-bone physics**, which is rarely implemented due to cost.
>
> ##### **C. Animation vs. Physics Trade-off**
> - Animations in games are often **pre-authored** (motion-captured or keyframed) and blended with physics later. This means:
>   - The skeleton's motion is predefined, and physics only adjusts the root motion (feet sliding, etc.).
>   - *Example*: When a dragon crashes into a wall, the animation system has no way to "fold" the wings unless explicitly programmed.
> - **Ragdoll physics** (used for falling players) is a limited form of per-bone physics but isn’t applied to controllable characters or mounts.
>
> ##### **D. Art and Design Priorities**
> - Games often **favor visual appeal over physical accuracy**. Artists design skeletons to look good in static poses, not to dynamically interact with the world.
>   - *Example*: Dracthyr's wings may be designed for spectacle, not to collide realistically with walls.
> - **Collision meshes** are often simplified or scaled up to avoid false positives, leading to "no-clipping."
>
> ##### **E. Gameplay Balancing**
> - Perfect physics could break gameplay. If a dragon mount physically collides with every wall, it might become unstuck or fall through the world in unintended ways.
>   - *Example*: In *WoW*, mounts are designed to "float" slightly to avoid getting stuck in terrain.
>
> ---
>
> #### **2. When Will This Improve?**
> ##### **Short-Term (1–3 Years)**
> - **Incremental fixes** are more likely:
>   - Better **per-limb collision detection** for mounts/pets (e.g., wings hitting walls).
>   - **Procedural animation corrections** (e.g., feet adjusting to slopes).
>   - However, full-body physics for all skeletons is unlikely due to performance costs.
>
> ##### **Mid-Term (3–5 Years)**
> - **Next-gen engines** (Unreal Engine 6, Unity 2025+) may introduce:
>   - **Per-bone physics solvers** for complex skeletons.
>   - **AI-driven collision avoidance** (e.g., NPCs folding their wings in tight spaces).
>   - **Hybrid animation-physics systems** (like NVIDIA’s **PhysX for Animation**).
>
> ##### **Long-Term (5+ Years)**
> - **True physics-based animation** could become mainstream if hardware improves (e.g., GPU-accelerated physics, AI-assisted simulations).
>   - *Example*: *Hellblade: Senua’s Sacrifice* used physics for cloth, but applying this to full skeletons is a bigger leap.
> - **AI and machine learning** could help simulate realistic limb interactions without brute-force physics (e.g., predicting how a dragon would fold its wings).
>
> ---
>
> #### **3. What Would Fix This?**
> To achieve the behavior you describe (e.g., a Gryphon smushing against a wall), games would need:
> 1. **Per-bone collision detection** with **penetration resolution**.
> 2. **Dynamic animation blending** to adjust poses based on physics feedback.
> 3. **High-performance physics solvers** (like Havok or NVIDIA PhysX) optimized for skeletons.
> 4. **Artificial intelligence** to predict and avoid collisions (e.g., pathfinding + physics).
>
> ---
>
> #### **Conclusion**
> While **small improvements** (better collision meshes, limb-specific

******************************************

## Question for popular sims part 2
"\[...\]" shows typo fixes
> Understood that collision checks with all rendered skeletons would cause "computational explosion" (use too much physics processor unit or central proessor unit resources), but most such sims use "zones" to improve network + CPU use; each "instance" has numerous small zones (each zone is equal to the view distance, or to double the view distance), such that physics just computes within those zones. But this simple "physics" just determines whether you can cast stuff on others, or whether the data structures are sent to you at all or not.
>
> For natural physics, can you not produce sub-zones as large as the largest skeleton, than have the skeleteon-physics compute collisions within those small sub-zones? If natural skeleton physics is still too expensive, what if you just pre-compute physics to "slow down" or "fold extremities towards center of mass" when your own bounder-box is too close to another bounder-box? This will not allow to \[land\] on the \[sides of houses\], nor to climb over all obstacles, \[but\] will prevent some collisions

### *Solar-Pro-2*'s solution for popular sims part 2
Notice: the *block quote* which follows was produced from the *artificial intelligence* known as [*Solar-Pro-2*](https://poe.com/Solar-Pro-2).
> Your idea of **sub-zones scaled to skeleton size** and **pre-computed collision responses** is a practical compromise between performance and realism. Here’s how it could work and its limitations:
>
> ---
>
> #### **1. Sub-Zone Physics for Skeleton Collision**
> ##### **How It Could Work:**
> - **Dynamic Zone Partitioning**:
>   - Divide the world into **adaptive sub-zones** (e.g., cubes or spheres) sized to fit the largest skeleton in the game (e.g., a Dracthyr’s bounding box).
>   - Only perform per-bone collision checks within the same sub-zone to limit computational overhead.
>   - Zones update dynamically as skeletons move (e.g., a dragon mount enters a new sub-zone).
>
> - **Bone-Level Collision Checks**:
>   - Represent each limb as a **collision primitive** (capsule, box, or convex hull).
>   - Check for overlaps only between limbs in the same sub-zone.
>   - If a collision is detected, apply **penetration resolution** to push limbs apart.
>
> ##### **Advantages**:
>   - Reduces the number of pairwise checks by limiting them to nearby skeletons.
>   - Prevents extreme "no-clipping" in tight spaces (e.g., a corridor).
>   - Works well for **self-collision avoidance** (e.g., a dragon’s wings not intersecting its tail).
>
> ##### **Limitations**:
>   - **Still expensive for large crowds**: In a battleground with 100 players, each with 50 bones, this could strain the CPU.
>   - **No environmental interaction**: Skeletons won’t realistically collide with buildings or terrain unless the environment is also partitioned into sub-zones with physics.
>
> ---
>
> #### **2. Pre-Computed "Fold Towards Center of Mass"**
> ##### **How It Could Work:**
> - **Proximity-Driven Animation Blending**:
>   - When a skeleton’s bounding box overlaps with another object (wall, player, etc.), **blend animations** to pull extremities toward the center of mass.
>   - Use **inverse kinematics (IK)** to adjust limb positions while maintaining a natural pose.
>   - Example: A dragon’s wings fold inward if it’s too close to a wall.
>
> - **Penalty Forces**:
>   - Apply artificial forces to joints that push limbs away from collisions.
>   - Similar to **ragdoll physics** but constrained to pre-authored poses.
>
> ##### **Advantages**:
>   - Avoids computational explosion by relying on animations rather than full physics.
>   - Can prevent **self-intersections** and minor environment collisions.
>   - Works well for **crowd scenes** where realism isn’t the priority.
>
> ##### **Limitations**:
>   - **Not physically accurate**: A dragon won’t "land on a wall" or "bounce off"; it’ll just compress its hitbox.
>   - **No dynamic interaction**: The skeleton won’t push against or climb obstacles—it’ll just deform.
>
> ---
>
> #### **3. Hybrid Approach: Sub-Zones + Animation Blending**
> A more realistic middle ground:
> 1. **Use sub-zones** to limit collision checks to nearby skeletons/environment.
> 2. **For environment collisions**, use simplified physics (e.g., raycasts from feet/wings to detect surfaces).
> 3. **For skeleton-skeleton collisions**, blend animations to fold extremities when overlaps occur.
> 4. **For critical interactions** (e.g., a mount crashing into a wall), trigger a **pre-rigged animation** (e.g., "impact squash").
>
> ##### **Example in *WoW***:
> - A Dracthyr flying into a wall:
>   - Its wings fold inward (animation blend).
>   - Its flight path is adjusted (root motion correction).
>   - No per-bone physics, but the illusion of collision is maintained.
>
> ---
>
> #### **4. When Could This Be Implemented?**
> - **Short-Term (1–2 Years)**:
>   - Games like *WoW* could adopt **animation blending for collision avoidance** in tight spaces.
>   - Sub-zone physics might be tested in smaller-scale games (e.g., *Diablo 4* or *Final Fantasy XVI*).
>
> - **Mid-Term (3–5 Years)**:
>   - Next-gen engines (Unreal 6, Unity 2025+) could introduce **per-bone physics solvers** optimized for skeletons.
>   - **AI-driven physics** (machine learning to predict limb interactions) might reduce computation.
>
> - **Long-Term (5+ Years)**:
>   - **Full physics-based animation** becomes feasible with better hardware (e.g., GPU-accelerated physics, quantum computing for collision detection).
>
> ---
>
> #### **Conclusion**
> Your idea of **sub-zones + animation blending** is a viable near-term solution. It won’t allow a Gryphon to land on a wall, but it can prevent extreme no-clipping and self

******************************************

# Synopsis
* [`./posts/Physics_sims_which_structures_to_use.md`](./Physics_sims_which_structures_to_use.md)

