**Physics sims: which structures to use (primitives versus vectors, `double` versus `long`, `volatile` versus `synchronized` versus `Atomic*`)**

\[[This post](./Physics_sims_structures.md) allows [all uses](https://creativecommons.org/licenses/by/2.0/).\]

# Table of Contents
- [Intro](#intro)
  - [Popular structures for sims](#popular-structures-for-sims)
  - [Separate variables versus dim lists](#separate-variables-versus-dim-lists)
  - [`double` versus `long`](#double-versus-long)
  - [`volatile` versus `synchronized` versus `Atomic*`](#volatile-versus-synchronized-versus-atomic-versus)
- [Synopsis](#synopsis)

# Intro
This document uses [`java`](https://github.com/topics/java) syntax for [data structures](https://docs.oracle.com/javase/8/docs/technotes/guides/jni/spec/types.html) plus [simple physics functions](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/lang/Math.html#field-detail) (which all have close-to-similar versions in most languages).

Most software engines (both for games, or physics sims) stick to `float` (or `double`) for position structures, but not much discussion exists on which structure to use.

Unless the sim is supposed to allow simple future changes of the structures used, the chore is often difficult:
* to switch from [separate variables](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/datatypes.html) (such as `double xPos, yPos;`) to [dim lists](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/util/Arrays.html) (such as `double[] pos`),
* to switch all positions + distances from `double` to `long`, or `long` to `double`.

******************************************
## Popular structures for sims
- *types* are *primitives* (such as [`double`](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/datatypes.html#:~:text=double)) or `class`es (such as [`java.lang.Integer`](https://docs.oracle.com/javase/8/docs/api/java/lang/Integer.html)).
  - *Inheritance* ("to *inherit*") is for one `class` to have all which some (different) `class` has. Non-primitive *types* in `java` all *inherit* from [`java.lang.Object`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html): `class Node : extends Object { double value; };` *extend*s `Object` to include `double value;`.
- *Nodes* (also known as *elements*) are *types* stored in *lists* (such as `double[] arrayList` or [`java.util.List<Integer> list`](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/util/List.html)), or stored in *graphs*.
  - *Structures* are *nodes* with some definition of usage (such as *coordinates*, *vertices*, *meshes* or *textures*).
  - *Tensors* are the superset of *vectors* (contiguous *lists* such as `double[]`) which can include numerous dimensions (`Color[][] bitmap` is an example of 2-dimensional *tensor*).
    - *Resolution* is most known to consumers as the `.size()` of *tensors*: `Color[1000][2000] bitmap;` gives `1000*2000` *resolution* to the *tensor* known as `bitmap` (*resolution* of *monitors* is the `.size()` of the `bitmap` of thus *monitors*).
      - *Resolution* has an overloaded definition: *resolution* also refers to the minimum step size (for `Integer` this is `1`, for `Double` this changes with magnitude, but epsilon values (such as [`Double.MIN_NORMAL`](https://stackoverflow.com/questions/3728309/difference-between-javas-double-min-normal-and-double-min-value) are popular minimum step sizes for `Double`, or [you can use `Math.nextAfter()`](https://stackoverflow.com/questions/28112500/how-to-get-the-smallest-next-or-previous-possible-double-value-supported-by-the))). Most physics documents use the "minimum step size" definition of *resolution* (which the section [`double` versus `long`](#double-versus-long) uses).
- *Indices* are offsets from the first *node* of *lists*: `class PrimitiveIndices { int[] index; }; class Index { Integer value; }; class Indices {List<Index> index; };` `Indices` stores a simple *list* of `Index`es. With `PrimitiveIndices`, performance improves, but `java`'s [*Generics*](https://docs.oracle.com/javase/tutorial/java/generics/types.html) can not use thus.
  - *Edges* are *tuples* of *indices* into *lists*, for adjacent *nodes*: `class Edge { Index source, dest; /* indices */} List<Edge> edges;`, which stores unsorted `Edge`s. The `source, dest` format supports *directed edges* (some *graphs* require *directed edges*), but also allows undirected *edges* (*meshes* use *undirected edges*).
    - *Graphs* are similar to *lists* but store connections (`Edge`s).
      - *Dense graphs* are 2-dimensional lists of nodes (in meshes, thus nodes are *vertices*): `Index[nTotalVertices][nMaxAdjacentVertices] adjacencyList;` is a *dense graph* of `Index`s (*indices*) to *nodes*.
      - *Sparse graphs* are the most popular *graphs*, which are similar to *dense graphs* except just edges are stored:
        - one form of *sparse graphs* is `List<Edge> edges;`, which stores unsorted `Edge`s.
        - another form of *sparse graphs* is `Map<Index, Indices> adjacencyList;`, which is an associative *list* of `Index`s (*indices*) of nodes to `List`s of adjacent *nodes*. This uses more resources to store, but less resources fetch values.
- *Pixels* are 24-bit **RGB** (or 32-bit [**RGBA**](https://en.wikipedia.org/wiki/RGBA_color_model)) components: `class Pixel { Integer value; }; Pixel[] pixels;` stores a simple *list* of `Pixel`s.
  - Most languages will use 32-bit integers for *bitmaps*, but `java` has [`java.awt.Color`](https://docs.oracle.com/javase/8/docs/api/java/awt/Color.html) for thus: `class Pixel { Color value; };`. Pros of `Color`: is standard, popular structure which stores **RGBA** values, with functions to access individual channels, plus does not require more overhead then `Integer` to implement.
  - Some architectures use other structures such as [**Y'UV**](https://en.wikipedia.org/wiki/Y%E2%80%B2UV) (to improve performance for specific tasks).
- *Bitmaps* are 2-dimensional tensors of *pixels* (most are supposed to show as *sprites* or as simple static images): `class Bitmap { Pixel[xResolution][yResolution] pixel; }; Bitmap[] bitmaps;` stores a simple *list* of `Bitmap`s with similar *resolutions*.
  - *Sprites* are maps of directions to *bitmaps* which are used for simple 2-dimensional sims: `enum Direction { North, South, East, West; }; class Sprite { Bitmap[Direction.values().length] avatar; }; Sprite[] sprites;` stores a simple list of `Sprite`s, which require [*geometric translation*](https://en.wikipedia.org/wiki/Translation_(geometry)) ([vertical bounces](./2_dimensional_forge.md#:~:text=simulateMotion)) for motion. Some sims [use `.gif`s (as opposed to `Bitmap`s) for more natural motion](https://stackoverflow.com/questions/9139386/animated-gif-vs-spritesheet-js-css).
  - *Textures* are *bitmaps* which are supposed to transform onto (do complex geometric convolutions onto) *meshes*: `class Texture { Bitmap bitmap; }; Texture[] textures;` stores a simple *list* of *textures* with similar *resolutions*.
- *Coordinates* are offsets from the origin of Euclidean spaces: `class Coord { double pos; }; Coord[] coordinates;` stores a simple *list* of *coordinates*.
  - *Positions* are N-coordinates, for N-dimensional spaces: `class Position { Coord[dim] coord; }; Position[] positions;` stores a simple *list* of `Position`s. [`package susuwu.{Immutable,}Pos{2,}`](https://github.com/SwuduSusuwu/SusuJava/tree/pos2/susuwu#purposes) improves performance for popular *position* formulas. Most of thus also have uses for *vertices*.
    - [*Voxels*](https://wikipedia.org/wiki/Voxel) \[[<sup>2</sup>](https://blog.spatial.com/the-main-benefits-and-disadvantages-of-voxel-modeling)\] are `Position`s which represent spheres (or cubes) plus `Color`, for N-dimensional spaces: `class Voxel { Position pos; Pixel pixel; }; Voxel[] voxels;` stores a simple *list* of `Voxel`s. [Old-fashioned sims use `Voxel`s](https://the-voxel-store.itch.io/).
    - *Vertices* are *positions* of corners of *ngons* (triangles are the simplest *ngons*): `class Vertex { Position pos; }; Vertex[] vertices;` stores a simple *list* of `Vertex`es. New sims replace `Voxel`s (with `Vertex`es plus `Texture`s).
      - *Adjacent vertices* are *vertices* attached with *edges* which form *skeletons* (or produce *Ngons*): `class AdjacentVertices { Map<Index, Indices> map; /* `Index`es of `Vertex`es */ };` is a simple "*adjacency list*".
    - *Surfaces* are the flat *geometric faces* of `Mesh`es: `class Surface { Vertex[] vertex; }; Surface[] surfaces;` stores a simple *list* of `Surface`s, *renderers* set `Texture`s onto thus *surfaces* (or onto *Ngons*).
      - *Ngons* are the smallest groups of adjacent *vertices* which can produce *faces*, for N-dimensional spaces: `class Ngon { Vertex[dim] vertex; }; Ngon[] ngons;` stores a simple *list* of `Ngon`s.
    - *Skeletons* are lists of *vertices* whose "joints" (*connections*) allow angular *motions*: `class Skeleton { Vertex[] vertices; AdjacentVertices connections; }; Skeleton[] skeletons;` stores a simple *list* of `Skeleton`s.
      - [*Quarternions*](https://en.wikipedia.org/wiki/Quaternion) are trigonometric *structures* used for motion of *joints* in `Skeleton`s.
    - *Point clouds* are *lists* of `Position`s of corners of processed *surfaces*: `class PointCloud { List<Position> point; }; PointCloud[] pointClouds;` stores a simple *list* of `PointCloud`s. [MiDaS (monocular depth estimation)](https://pytorch.org/hub/intelisl_midas_v2/) processes [individual `Bitmap`s into partial (just includes the surface) `PointCloud`s](https://github.com/SwuduSusuwu/SusuLib/blob/4cc0f8a1e7b8e5bca0cf69d114e81bc743fec7e9/posts/ArduinoElegooTools.md#tensorflow-static-image-to-point-clouds) (but is not accurate). [`cv2.calcOpticalFlowFarneback`](https://docs.opencv.org/4.x/d4/dee/tutorial_optical_flow.html#autotoc_md1162) allows to [produce whole (volumetric) `Pointcloud`s, but requires motion images (*lists* of connected `Bitmap`s)](https://github.com/SwuduSusuwu/SusuLib/blob/4cc0f8a1e7b8e5bca0cf69d114e81bc743fec7e9/posts/ArduinoElegooTools.md#optical-flow-processing-of-visuals-into-point-cloud-computes-z-axis).
      - *Textured point clouds* are `PointCloud` which store `Voxel`s (not just `Position`s): `class PointCloud { List<Voxel> point; }; TexturedPointCloud[] texturedPointClouds;` stores a simple *list* of `TexturedPointCloud`s. Different formulas are used to produce thus, since the `point`s are not infinitisimal corners of *surfaces* but are *spheres* (which all have similar circumfurence but different `Color`s)
      - [Depth imagers (such as *Microsoft Kinect 2*)](https://kinect.github.io/tutorial/lab04/index.html) can produce whole *connected point clouds* (`PointCloud`s which include `Edge`s for adjacent `Position`s, which improves conversion into *meshes*): `class ConnectedPointCloud { List<Position> point; List<Edge> edge}; ConnectedPointCloud[] connectedPointClouds;` stores a simple *list* of `ConnectedPointCloud`s.
- *Meshes* are *graphs* of *vertices*: `class Mesh { Vertex[] vertices; AdjacentVertices adjacentVertices; }; Mesh[] meshes;` stores a simple *list* of *meshes* (assumes `vertices.size() > Index.intValue()`).
- *Motions* are sequences of *motion vectors* (of *derivatives of position*), which are produced for specific *meshes* ("skeletons") to move: one popular form of *motions* is [`.fbx` *Filmbox* motions](https://www.sidefx.com/docs/houdini/nodes/out/filmboxfbx.html).
- *Avatars* (also known as *models*) are `Mesh`es plus `Texture`es plus `Skeleton`s: `class Avatar { Skeleton skeleton; Mesh mesh; Texture texture; }; Avatar[] avatars;` stores a simple *list* of `Avatar`s.
  - Old-fashioned *avatars* use `Voxel`s (not `Mesh`es plus `Texture`es): `class OldFashionedAvatar { Skeleton skeleton; Voxel[] voxels; }; OldFashionedAvatar[] oldFashionedAvatars;` stores a simple *list* of `OldFashionedAvatar`s. Old-fashioned *avatars* are just used in old sims (such as *DirectX 6* sims) or [raytracers](https://dubiousconst282.github.io/2024/10/03/voxel-ray-tracing/).
- *Renderers* load `Avatar`s, process `Mesh`es into *surfaces* attached to `Skeleton`s, plus load "skins" (*textures*) onto thus *surfaces*.
  - Most popular *renderers* also use *motions* so `Skeleton`s move, but some *renderers* just produce static images.
- [`tensorflow`](https://github.com/tensorflow/tensorflow) loads examples of `{input, output}` (which is `{question, answer}`) to produce connectomes (groups of synapses) which process future questions into new answers.
- *Descriptions* are [`char[]`](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/datatypes.html#:~:text=char)s or [`String`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html)s, which store human-language versions of *structures* (such as of *meshes*). *Descriptions* are used to document *structures* for *humans*, or for tools such as `tensorflow`.

******************************************
## Separate variables versus dim lists
Pros of `double xPos, yPos;`:
* If stuck with source-code compilers (or [script interpreters](https://ruslanspivak.com/lsbasi-part1/)) which [can not optimize static lists into constant access](https://stackoverflow.com/questions/13748872/java-is-there-a-performance-difference-between-using-n-variables-or-using-hard), this improves [**RAM** plus **CPU** use](https://stackoverflow.com/questions/47177/how-do-i-monitor-the-computers-cpu-memory-and-disk-usage-in-java).
  * If stuck with those which [can not unroll loops](https://stackoverflow.com/questions/58995731/java-manually-unrolled-loop-is-still-faster-than-the-original-loop-why) (loops such as dimension-agnostic physics functions), this improves **CPU** use.

Pros of `double[] pos;`:
* Simple to switch to more (or less) dimensions: if loops are used for the physics functions ([such as `package susuwu` does](https://github.com/SwuduSusuwu/SusuJava/blob/pos2/posts/FishSim.md)), allows to reuse [dimension-agnostic source code](https://docs.oracle.com/javase/8/docs/api/java/util/stream/Collectors.html).
* New compilers reduce those indirect accesses (the implicit pointer indirection) into constant accesses (hardcoded addresses).

******************************************
## `double` versus `long`
Some languages have `long double` (which gives nanometer *resolution* for all planets in our solar system), but:
* `long double` uses the **FPU**, so can not use vector improvements (such as [**SSE2**](https://github.com/SwuduSusuwu/SusuLib/blob/preview/posts/SimdGpgpuTpu.md#simd-single-instruction-multiple-data), nor [**GPGPU**](https://github.com/SwuduSusuwu/SusuLib/blob/preview/posts/SimdGpgpuTpu.md#gpgpus-general-purpose-graphics-processor-units)).
* `long double` uses 80 bits (`long` or `double` use 64 bits).
* `long double` uses 80 bits (`long` or `double` use 64 bits).

Pros of `double[] position;`:
* [`double` can store values in the range \[(2-2<sup>52</sup>)·2<sup>1023</sup>, 2<sup>1074</sup>\] (inclusive), store **NaN**, or store **Inf**](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/lang/Double.html#field-detail) (although *resolution* is poor with large magnitudes, plus some functions can not use [`Double.NaN`](https://docs.oracle.com/javase/8/docs/api/java/lang/Double.html#NaN) or [`Double.POSITIVE_INFINITY`](https://docs.oracle.com/javase/8/docs/api/java/lang/Double.html#POSITIVE_INFINITY) values).
* Since `double[]` includes variable exponents, `double[] position;`:
  * Is simple to use with formulas which involve squares ([`Math.pow()`](https://docs.oracle.com/cd/B40099_02/books/eScript/eScript_JSReference232.html#wp1013939)) or square roots ([`Math.sqrt()`](https://docs.oracle.com/cd/B40099_02/books/eScript/eScript_JSReference236.html#wp1014099)), such as *Euclidean distance* formulas (code which generalizes [`Math.hypot()`](https://docs.oracle.com/cd/E17904_01/apirefs.1111/e12048/functmath.htm#CQLLR191) to use more dimensions), which are common to physics sims.
  * `double[] position = {0, 0, 0}` with *Sol* (our sun)'s center-of-mass as the origin, can store positions as far as *Pluto* (but just with millimeter *resolution*).

Pros of `long[] position;`:
* [`long` can store values in the range \[-2<sup>63</sup>, 2<sup>63</sup>-1\] (inclusive)](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/lang/Long.html#field-detail) (with similar *resolution* for all of those values).
* Since `long[]` has fixed *resolution*:
  * The hardware (**CPU**s, **GPGPU**s, **TPU**s) plus software (the physics sim functions) is more simple.
  * All systems allow `long` bitshift (`<<=`, `>>=`) use (with `java`, `double` does not allow `<<=` nor `>>=`, but requires intrinsic functions such as [`Math.scalb`](https://docs.oracle.com/javase/8/docs/api/java/lang/Math.html#scalb-double-int-)). Versus division (also versus multiplication), bitshifts improve **CPU** use.
  * All positions have similar *resolution* (instead of femtometer *resolution* for *Sol*'s core (millimeter *resolution* for *Pluto*'s surface), the whole planet can have nanometer *resolution*).
  * `long[]` stores sufficient quantized positions to give nanometer *resolution* for the whole surface of the largest planet in our solar system (but with this *resolution*, the distance is limited to a single planet, such as *Jupiter*, with the planet's center-of-mass as origin).

******************************************
# `volatile` versus `synchronized` versus `Atomic*` versus
Those are the most popular structures to ensure that multiple [`Thread`](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/lang/Thread.html)s (or other *units of execution* such as [`java.util.concurrent.ExecutorService`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ExecutorService.html)) follow the *spatiotemporal structure* of the source code. More "*explicit*" (*granular*) structures exist, which do not introduce as much *blocks* (as much "*pauses*"), but which are more difficult to use.

## `synchronized`
If interpretation of so is true (am new to `java`, [so asked *Solar-Pro-2*, which says is true](https://poe.com/s/dTovhHsKEoQ6inFLCpWn)),  <https://johanley.github.io/java-practices-snapshot/topic/TopicAction5ade.html?Id=35> says:
* `class Foo { synchronized anInstanceFunction( { ... } })` causes such `synchronized` instance functions of `class Foo` to use an exclusive "instance lock" (not possible to choose which functions use which locks, except `static` versus not `static`).
* `class Foo { synchronized static someStaticFunction( { ... } })` causes such `synchronized` static functions of `class Foo` to use an exclusive "static lock" (not possible to choose which functions use which locks, except `static` versus not `static`).
* `synchronized(this)` causes the current execution to *block* (to pause) unti no *contexts of execution* use the *instance lock*, irrespective of if the current function is set to `synchronized`.
* `synchronized(this.getClass())` (which does what `synchronized(Foo.class)` does, if `this.getClass() == Foo`) causes the current execution to *block* (to pause) unti no *contexts of execution* use the *static lock*, irrespective of if the current function is set to `synchronized`.

## `java.util.concurrent.locks.ReentrantLock`
If interpretation of [this discussion with *Solar-Pro-2*](https://poe.com/s/dTovhHsKEoQ6inFLCpWn) is true:
* [`java.util.concurrent.locks.ReentrantLock`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/locks/ReentrantLock.html) is the *granular* version of `synchronized`.
* The code must setup (plus store, plus acquire, plus release) separate `ReentrantLock` instances with *explicit* instructions, thus more difficult to use.
* Due to separate `ReentrantLock` instances, numerous *units of execution* can use 1 `this`, if those *units of execution* contest for separate `ReentrantLock`s. Thus more *units of execution* (versus `synchronized`, which limits all `synchronized` blocks of `this` to 1 *unit of execution*).

## `volatile primitive` or `AtomicPrimitive`
If interpretation of so is true, [this discussion with *Solar-Pro-2*](https://poe.com/s/oKlj2EkZqBPioQ1Qgvlf) says:
* both ensure that `java` follows the explicit temporal precedence of the source code (without `volatile` or `Atomic`, `java` optimizes the execution such that *race conditions* are possible in executables which use multiple executors (such as *thread pools* or **SMP**).
* both ensure that stores whose size is more than the **CPU** architecture's word size (thus, *64-bit* primitives such as `double` or `long`) are stored whole. With no `volatile` or `Atomic` suffix, stores from one *unit of execution* can cause separate *contexts of execution* which access those addresses to process *spliced* versions ("*tearing*": versions whose first *32-bits* stores the new value but whose second *32-bits* stores the old value).
  * Just `AtomicPrimitive` suits *64-bit* **CAS** (`volatile long foo = 42; if(42 < ++foo)` is undefined, `AtomicLong foo = 42; if(42 < foo.incrementAndGet())` is true).

[*Solar-Pro-2* says this is true, plus suggests the alternative `java.util.concurrent.atomic`](https://poe.com/s/1rAVvmwTyh2kYFQE22PJ).

******************************************
# Synopsis
[This simple `java` fish sim](https://github.com/SwuduSusuwu/SusuJava/blob/pos2/posts/FishSim.md) still has much [code churn](https://github.com/SwuduSusuwu/SusuJava/commits/pos2/susuwu/FishSim.java) around which `position` data structures to use.

[`./posts/GoogleStore_MicrosoftStore_Ubuntu_scripted_tool_sims.md`](./GoogleStore_MicrosoftStore_Ubuntu_scripted_tool_sims.md) lists numerous physics sims for school use.

Most [search results](https://duckduckgo.com/?q=Do+static+arrays+in+Java+have+similar+performance+as+individual+variables%3F+%60double%5B%5D+position+%3D+%7B1%2C+2%7D%60+versus+%60double+x+%3D+2%2C+y+%3D+2%60) for such discussions just show physics engines' documents of `float` versus `double`:
* <https://docs.godotengine.org/en/stable/tutorials/physics/large_world_coordinates.html>
* <https://godotengine.org/article/emulating-double-precision-gpu-render-large-worlds/>
* <https://developer.unigine.com/en/docs/future/code/double_precision/usage>

