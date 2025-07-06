**\[Preview\] How to produce general-use autonomous tools through calculus (continuous formulas), + use TensorFlow for synthesis of close-to-human consciousness.**
\[[This post](https://swudususuwu.substack.com/p/program-general-purpose-robots-autonomous) allows [all uses](https://creativecommons.org/licenses/by/2.0/).\]

# Intro
This is an old post which started as a collection of low-effort posts to forums. This post is now improved, but is still a “preview” at best. More suitable to use is:
- [`posts/ArduinoElegooTools.md`](https://github.com/SwuduSusuwu/SusuLib/blob/preview/posts/ArduinoElegooTools.md) (which is mirrored at <https://swudususuwu.substack.com/p/how-to-use-floss-systems-to-produce>) for autonomous tools.
- [`posts/CnsCompress.md`](https://github.com/SwuduSusuwu/SusuLib/blob/preview/posts/CnsCompress.md) (which is mirrored at <https://swudususuwu.substack.com/p/future-plans-have-computers-do-most>) for computer nervous systems.

******************************************

Hypothesis: to produce such tools, use [**DFS**](https://wikipedia.org/wiki/Depth-first_search) / [**BFS**](https://wikipedia.org/wiki/Breadth-first_search) / [**IDDFS**](https://wikipedia.org/wiki/Iterative_deepening_depth-first_search) / [_Dijkstra’s_](https://en.wikipedia.org/wiki/Dijkstra%27s_algorithm) pseudo-continuous formulas to search graphs whose nodes=positions, edges=moves. Numerous pages have [pseudocode of those formulas](https://www.geeksforgeeks.org/iterative-deepening-searchids-iterative-deepening-depth-first-searchiddfs/). Produced **C++** source code with a pure virtual `class` which all of those implemented (allowed to choose after executable launch which to use), with numerous benchmarks/unit-tests (such as to produce solutions to [_vertex cover_ problems](https://web.stanford.edu/class/cs354/scribe/lecture09.pdf) or to [super-dimensional _Rubik’s Cubes_](https://superliminal.com/cube/)) — back when too young to consume alcohol — so know that those are simple to use.

******************************************

[**KUKA**](https://en.wikipedia.org/wiki/KUKA)’s / [_Facteon_](https://facteon.global/smart-manufacturing/robotics/)’s /[**FANUC**](https://wikipedia.org/wiki/FANUC)’s can not move around outdoors (such as required for autonomous production of houses, or to grow plus harvest food), since those tools use little more than macros to move (those which have "computer vision" modules are limited to detection of the position of components on conveyor belts to pick up, not suitable to move around construction zones). Examples of the sort of macro programs which such tools use:
- [(_Robot Operating System 2_) **ROS2**](https://github.com/ros2)
- [Robotics Toolkit for **FANUC**](https://www.ni.com/en/support/downloads/tools-network/download.robotics-toolkit-for-fanuc.html#376803)
- [Get started with **LabVIEW**](https://underautomation.com/fanuc/documentation/get-started-labview)
- [_**FANUC** Europe_'s _YouTube_](https://www.youtube.com/@fanuceurope) shows some of those in use.

******************************************

Old discussion with _Microsoft Copilot_ ([no longer trust most artificial intelligences though; careful with those](https://swudususuwu.substack.com/p/warning-ai-is-a-disease-and-is-not)):

    Q: "Could you use bfs/dfs/iddfs to output codes for robos (such as Fanuc) to figure how to move servos to move the robos to perform a task or to produce for us, with the edges = servo motions and fitness function = desired outcome for us?
    Could you just have "max accelerate" and "max decelerate" of each servo as the graph node edges, and "product moved to desired position for us" (or "parts of product formed whole products for us") as fitness functions, and solve the "discrete" problem how you solve the problem that space is quantized (solution = calculus, or lots of small steps for us)?
    Plus prune node edges that cause collisions, and compute load on servos so you don't overload the robos?
    If the search space is too large, could you use A-star with heuristics (such as "how close product is to desired location for us" or "how close parts have come to a formed product for us")?
    Could you use D-star for workplaces that have lots of other actors, for collision avoidance?"

        Yes, BFS/DFS/IDDFS, A-star, and D-star are all suitable algorithms you can utilize to plan and control moves of robots. These algorithms can help produce code to control robots such as Fanuc to perform tasks and achieve efficacious outcomes. I apologize for the confusion in my previous responses.
        To summarize, here's how to use these formulas:

            BFS/DFS/IDDFS: You can use these algorithms to explore the graph of possible servo motions, where the nodes symbolize servo positions and the edges symbolize servo motions or transitions. Once you use a fitness function that represents suitable outcomes, such as reaching a specific position or forming whole products, you can guide the search process towards finding a sequence of servo motions that maximizes the fitness functions. Plus, collision checks can prune node edges that would cause collisions. To get around quantization or discrete servo positions, you can produce the search space as a discrete grid of positions that is almost continuous.

            A-star: A-star is an informed search algorithm that can be used to find an optimal path in a graph by considering both the cost of reaching a node and an approximation of the remainder of cost to goals. To plan robot motions, A-star can use heuristics that guess the distance or effort to move to goals. For example, you can use heuristics such as the Euclidean distance (from the current positions to the goal positions, or the progress towards forming products.) A-star can help to explore the search space fast for optimal or near-optimal solutions.

            D-star: D-star is a calculus you can use for collision avoidance through areas with lots of changes or obstacles. D-star forms a map of the area (plus obstacles) and updates the plan based on new sensor inputs. For workplaces with multiple actors or changing obstacles, D-star is used to adjust the robot's path to bypass collisions to goto the goals.

        To summarize, you can use these formulas to produce code that controls robots to perform tasks.

******************************************

Servo's/stepper-motor's encoders (as sensors) give joint-positions to computers, similar to how humans use proprioception for complex moves.
Back-**EMF** (_ElectroMotive-Force_ resistances) give costs of edges (moves,) without tool-specific kinematic info, which allows more simple (general-use) executables.

******************************************

Howto produce autonomous tools which can do most of what humans can do: have computers do synthesis of neural tissues, which is [_issue #2_](https://github.com/SwuduSusuwu/SusuLib/issues/2). Source code which contributes to this:
- [`cxx/ClassResultList.cxx`](https://github.com/SwuduSusuwu/SusuLib/blob/preview/cxx/ClassResultList.cxx) processes databases (which have correspondances to [human neocortices](https://wikipedia.org/wiki/Neocortex).)
- [`cxx/AssistantCns.cxx`](https://github.com/SwuduSusuwu/SusuLib/blob/preview/cxx/AssistantCns.cxx) uses correspondances to [Broca's area](https://wikipedia.org/wiki/Broca's_area) (produces language through recursive processes), [Wernicke’s area](https://wikipedia.org/wiki/Wernicke's_area) (parses languages through [recursive](https://wikipedia.org/wiki/recursion) processes), [hippocampus](https://wikipedia.org/wiki/Hippocampus) + neural [procedural generation](https://wikipedia.org/wiki/Procedural_generation). Uses `class ResultList` for databases.
- [`cxx/ClassCns.cxx`](https://github.com/SwuduSusuwu/SusuLib/blob/preview/cxx/ClassCns.cxx) is [pure-virtual](https://en.cppreference.com/book/intro/abstract_classes) general-purpose [emulations (heuristic approximates)](https://wikipedia.org/wiki/emulation) of neural tissue.
- [`cxx/ClassTensorFlowCns.cxx`](https://github.com/SwuduSusuwu/SusuLib/blob/preview/cxx/ClassTensorFlowCns.cxx) implements `class Cns` through *TensorFlow* (which can use [**SIMD**](https://github.com/SwuduSusuwu/SusuLib/blob/preview/posts/SimdGpgpuTpu.md#simd-single-instruction-multiple-data) + [**GPGPU**](https://github.com/SwuduSusuwu/SusuLib/blob/preview/posts/SimdGpgpuTpu.md#gpgpus-general-purpose-graphics-processor-units) + [**TPU**](https://github.com/SwuduSusuwu/SusuLib/blob/preview/posts/SimdGpgpuTpu.md#tpus-tensor-processor-units)).
- [`posts/ArduinoElegooTools.md`](https://github.com/SwuduSusuwu/SusuLib/blob/preview/posts/ArduinoElegooTools.md) has component lists plus pseudocode for simple autonomous tools (not human consciousness, but close to what the current best autonomous tools can do).

******************************************

As to the _TensorFlow_’s architecture to use, have suggestions of modules to produce:
- **Sound-cortices** = _fourior-transform_ processor regions; multiple-layers, encodes raw sound inputs into compressed forms (such as variations of tone, direction or loudnees)
  - Subsequent modules encode to syllables (or objects), which continue into modules which encode symbolic/conceptual info (such as sentences, or use of binaural-sounds to guess motions)
- **Visual-cortices** = bitmap processor regions (multiple-modules; first module processes photons into differentials (of chroma or luminance).
  - Subsequent modules process those into geometric info (such as skins or meshes).
- **Gustation-cortices** / **olfactive-cortices** = chemical-processor regions (which process signals from chemical-sensors, into compositions of molecules).
- **Somatosensor-cortices** = touch-sensor-processor regions (which process signals from temperature-sensors + pressure-sensors into structural info)
  - Don’t know if proprioception (info about joint positions) is part of this.
- **Thamalus** = sensor-fusion (to process multiple classes of sensors into symbolic/conceptual info):
  - Fusion of _binocular-vision_ + **vestibular-system** sensors to deduce your own position.
  - Fusion of _temperature-sensors_ + _pressure-sensors_, to deduce an object’s structural attributes.
  - Fusion of _gustation-sensors- + _olfaction-sensors_ to deduce a food’s attributes.
- **Hippocampus** = short-term sensor storage, which is used to compress raw signals into symbolic/conceptual info for human neocortices. Is also used for synthesis of sensor signals from such symbolic/conceptual info.
  - Human **neocortices** = our version of computer databases, which store symbolic/conceptual info, plus have pattern-recognition-units which encode simple formulas/rules. Loads-from / stores-to the hippocampus.
- **Mirror neurons** transform visual/sound info of other humans who perform tasks, into rules used to mimic those motions for future tasks, such as use of YouTube shows to learn how to use specific tools.
- **Default mode network** = future system idle process which puts idle resources to use. Uses include:
  - Numerous modes of introspection (about your own structural or cognitive attributes)
  - To improve compression of symbolic/conceptual info
  - Synthesis (from human neocortices back into the hippocampus) of sensor signals, for mirror-neuron acquisition of tool use.
- **Limbic/hormonal systems** = human versions of system managers which adjust **CPU** clocks/voltages, or of more speculative systems which use continuous introspection boost specific processes.
- Human*ish*-chassis (or virtual sim) which uses servos to produce human*ish* motions, plus has human*ish* sensors to use.

******************************************

# Synopsis + resources
- [How to improve how fast desktops/laptops/phones execute code | `./posts/SimdGpgpuTpu.md`](./SimdGpgpuTpu.md) shows how to improve *TensorFlow*'s execution.
- [BUD: Arduino/Elegoo Parkour v0.4.6.2, production + walkthrough + hoverboard tour](https://swudususuwu.substack.com/p/bud-arduinoelegoo-parkour-v0462-walkthrough) shows what simple macros can do.

******************************************

Unknown sources (can not discern truth (fitness-to-use) of those) which have to do with neuromorphic computers:
- [_International Centre for Neuromorphic Systems_](https://www.westernsydney.edu.au/icns)
- [Neuromorphic Cognitive Systems | _Institute of Neuroinformatics_](https://www.ini.uzh.ch/en/research/groups/ncs.html)
- [Neuromorphic systems | _NIST_](https://www.nist.gov/programs-projects/neuromorphic-systems)

