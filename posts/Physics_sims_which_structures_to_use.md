**Physics sims: which structures to use (primitives versus vectors, `double` versus `long`)**

\[[This post](./Physics_sims_structures.md) allows [all uses](https://creativecommons.org/licenses/by/2.0/).\]

# Table of Contents
- [Intro](#intro)
  - [Separate variables versus dim lists](#separate-variables-versus-dim-lists)
  - [`double` versus `long`](#double-versus-long)
- [Synopsis](#synopsis)

# Intro
This document uses [`java`](https://github.com/topics/java) syntax for [data structures](https://docs.oracle.com/javase/8/docs/technotes/guides/jni/spec/types.html) plus [simple physics functions](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/lang/Math.html#field-detail) (which all have close-to-similar versions in most languages).

Most software engines (both for games, or physics sims) stick to `float` (or `double`) for position structures, but not much discussion exists on which structure to use.

Unless the sim is supposed to allow simple future changes of the structures used, the chore is often difficult:
* to switch from [separate variables](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/datatypes.html) (such as `double xPos, yPos;`) to [dim lists](https://docs.oracle.com/en/java/javase/21/docs/api/java.base/java/util/Arrays.html) (such as `double[] pos`),
* to switch all positions + distances from `double` to `long`, or `long` to `double`.

******************************************
## Separate variables versus dim lists
Pros of `double xPos, yPos;`:
* If stuck with source-code compilers (or [script interpreters](https://ruslanspivak.com/lsbasi-part1/)) which [can not optimize static lists into constant access](https://stackoverflow.com/questions/13748872/java-is-there-a-performance-difference-between-using-n-variables-or-using-hard), this improves [**RAM** plus **CPU** use](https://stackoverflow.com/questions/47177/how-do-i-monitor-the-computers-cpu-memory-and-disk-usage-in-java).
  * If stuck with those which [can not unroll loops](https://stackoverflow.com/questions/58995731/java-manually-unrolled-loop-is-still-faster-than-the-original-loop-why) (loops such as dimension-agnostic physics functions), this improves **CPU** use.

Pros of `double[] pos;`:
* Simple to switch to more (or less) dimensions: if loops are used for the physics functions ([such as `package susuwu` does](https://github.com/SwuduSusuwu/SusuJava/blob/pos2/posts/FishSim.md)), allows to reuse [dimension-agnostic source code](https://docs.oracle.com/javase/8/docs/api/java/util/stream/Collectors.html).
* New compilers reduce those indirect accesses (the implicit pointer indirection) into constant accesses (hardcoded addresses).

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
# Synopsis
[This simple `java` fish sim](https://github.com/SwuduSusuwu/SusuJava/blob/pos2/posts/FishSim.md) still has much [code churn](https://github.com/SwuduSusuwu/SusuJava/commits/pos2/susuwu/FishSim.java) around which `position` data structures to use.

[`./posts/GoogleStore_MicrosoftStore_Ubuntu_scripted_tool_sims.md`](./GoogleStore_MicrosoftStore_Ubuntu_scripted_tool_sims.md) lists numerous physics sims for school use.

Most [search results](https://duckduckgo.com/?q=Do+static+arrays+in+Java+have+similar+performance+as+individual+variables%3F+%60double%5B%5D+position+%3D+%7B1%2C+2%7D%60+versus+%60double+x+%3D+2%2C+y+%3D+2%60) for such discussions just show physics engines' documents of `float` versus `double`:
* <https://docs.godotengine.org/en/stable/tutorials/physics/large_world_coordinates.html>
* <https://godotengine.org/article/emulating-double-precision-gpu-render-large-worlds/>
* <https://developer.unigine.com/en/docs/future/code/double_precision/usage>

