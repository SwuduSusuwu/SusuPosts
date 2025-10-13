**[fēl-is pisc-em cēpit "the cat caught the fish" to fēl-em pisc-is cēpit "the fish caught the cat"](https://en.wikipedia.org/wiki/Analytic_language#:~:text=fish). Human ancestors are fish.**

\[[This post](https://swudususuwu.substack.com/p/the-cat-caught-the-fish) allows [all uses](https://creativecommons.org/licenses/by/2.0/).\]

# Table of Contents
- [Intro](#intro)
- [*OpenGLES2* fish](#request-opengles2-fish)
  - [*OpenGLES2* fish released through *Apache 2* + *GPLv2*](#request-to-release-opengles2-fish-through-apache-2--gplv2)
- [*Java* fish](#request-java-fish)
  - [*Java* fish released through *Apache 2* + *GPLv2*](#request-to-release-java-fish-through-apache-2--gplv2)
- [Synopsis](#synopsis)

# Intro
It is common to correct [those who confuse](https://www.answers.com/mammals/Why_do_people_think_that_dolphins_were_fish) [_delphinida_](https://wikipedia.org/wiki/Delphinida) ([porpoises](https://duckduckgo.com/?t=h_&q=horse%20sims), [dolphins](https://www.dingogames.com/dolphin/) or orcas) with fish (such as [sharks](https://wowpedia.fandom.com/wiki/Shark)) — since _delphinida_ are mammals, evolved from cows (for taxonomists; ["_Artiodactyls_" or "_Cetartiodactyls_"](https://wikipedia.org/wiki/Artiodactyl), which is the group which includes both _Delphinida_ + cows) — but perhaps you should not; [all tetrapods (thus all mammals) evolved from the lobe-finned fish](https://wikipedia.org/wiki/Evolution_of_tetrapods).
- Most fish organs are also human organs. [Most human organs are also fish organs](https://www.mathsisfun.com/associative-commutative-distributive.html).
- Both have [mouths](https://substack-post-media.s3.amazonaws.com/public/images/91e0e319-a6b1-4dc4-8779-1f3b7895554f_1920x1080.jpeg), tongues, throats, stomachs, intestines, [bladder](https://www.deviantart.com/dacos95/art/underwater-world-A-wip6-1223583458)s, [anus](https://www.hyperphysics.phy-astr.gsu.edu/hbase/Solar/uranus.html)es.
- Both have [hearts](https://www.deviantart.com/dacos95/art/underwater-world-A-wip6-1223583458).
- Both have [eyes](https://duckduckgo.com/?t=h_&q=mice&ia=images&iax=images), [ears](https://i.etsystatic.com/41632471/r/il/94566a/4984509254/il_fullxfull.4984509254_m7lz.jpg), [skin](https://www.robloxsticker.com/skins), [peripheral nervous systems](https://poe.com/s/LcRxFfzGrHEZ01taCIyl).
- Both have adaptive [central nervous systems](https://github.com/SwuduSusuwu/SusuLib/blob/preview/posts/CnsCompress.md) with [consciousness](https://pmc.ncbi.nlm.nih.gov/articles/PMC543470/).

[Humans](https://www.youtube.com/watch?v=gg5_mlQOsUQ), [cats](https://duckduckgo.com/?t=h_&q=nekolocation&ia=web), mongoose, [cows](https://superuser.com/questions/43715/what-are-super-cow-powers-and-why-doesnt-my-aptitude-have-them), porpoises plus [dinosaurs](https://blog.en.uptodown.com/dinosaurs-pubg-mobile-details-how-they-work/) all have the [lobe-fin](https://duckduckgo.com/?t=h_&q=lotion) fish as common [ancestors](https://itsfoss.com/birth-of-unix/), so it is important that [fishers](https://wikipedia.org/wiki/Phishers) allow our [oceans](https://www.digitalocean.com/) to continue to have numerous [fish](https://bashcommands.com/fish-vs-bash)es.

Not to confuse with cat food:
![Cat catches fish](https://substack-post-media.s3.amazonaws.com/public/images/91e0e319-a6b1-4dc4-8779-1f3b7895554f_1920x1080.jpeg)

******************************************

# Request *OpenGLES2* fish
Simple [_OpenGLES2_](https://www.khronos.org/opengles/) fish sim, ([produced through _Grok-2_](https://poe.com/s/ZGtQKWGpBLkOzaTr6SkA); [released through *Apache 2* + *GPLv2*](#request-to-release-opengles2-fish-through-apache-2--gplv2)).

**Q**: "Produce *OpenGLES2* code which moves the sprites of some fish around."

## [*Grok-2*](https://poe.com/Grok-2)'s *OpenGLES2* fish
**Notice**: *Grok-2* [used *C* for the original source code](https://github.com/SwuduSusuwu/SusuPosts/blob/0e99e40befe6f982653d7b2c0b0679572f015323/posts/Human_ancestors_are_fish.md#grok-2s-opengles2-fish), what follows is manual conversion to *C++* source code.

`build.sh`
```bash
#!/bin/sh
sudo apt install clang++ libglvnd-dev
clang++ -lGLESv2 fish.c++
return $?
```

`fish.c++`
```c++
#include <GLES2/gl2.h>
#include <GLES2/gl2ext.h>
#include <math.h>
#include <stdlib.h>
#include <time.h>
#include <vector>

// Structure to represent a fish
typedef struct {
	float x, y;  // Position
	float dx, dy;  // Velocity
	float angle;  // Rotation angle
} Fish;

class Fishes {
	GLuint program;
	GLuint vbo;
	std::vector<Fish> fishes;
	int num_fishes;

	// Vertex shader source
	const char* vertex_shader_source =
		"attribute vec4 a_position;\n"
		"attribute vec2 a_texCoord;\n"
		"uniform mat4 u_mvpMatrix;\n"
		"varying vec2 v_texCoord;\n"
		"void main() {\n"
		"    gl_Position = u_mvpMatrix * a_position;\n"
		"    v_texCoord = a_texCoord;\n"
		"}\n";

	// Fragment shader source
	const char* fragment_shader_source =
		"precision mediump float;\n"
		"uniform sampler2D u_texture;\n"
		"varying vec2 v_texCoord;\n"
		"void main() {\n"
		"    gl_FragColor = texture2D(u_texture, v_texCoord);\n"
		"}\n";

	// Initialize OpenGL ES
	Fishes() {
		// Compile shaders
		GLuint vertex_shader = glCreateShader(GL_VERTEX_SHADER);
		glShaderSource(vertex_shader, 1, &vertex_shader_source, NULL);
		glCompileShader(vertex_shader);

		GLuint fragment_shader = glCreateShader(GL_FRAGMENT_SHADER);
		glShaderSource(fragment_shader, 1, &fragment_shader_source, NULL);
		glCompileShader(fragment_shader);

		// Create program
		program = glCreateProgram();
		glAttachShader(program, vertex_shader);
		glAttachShader(program, fragment_shader);
		glLinkProgram(program);

		// Create VBO for fish sprite
		GLfloat vertices[] = {
			-0.5f, -0.5f, 0.0f, 0.0f, 0.0f,
			 0.5f, -0.5f, 0.0f, 1.0f, 0.0f,
			-0.5f,  0.5f, 0.0f, 0.0f, 1.0f,
			 0.5f,  0.5f, 0.0f, 1.0f, 1.0f
		};
		glGenBuffers(1, &vbo);
		glBindBuffer(GL_ARRAY_BUFFER, vbo);
		glBufferData(GL_ARRAY_BUFFER, sizeof(vertices), vertices, GL_STATIC_DRAW);

		// Initialize fish vector
		num_fishes = 10;
		fishes.reserve(num_fishes);
		srand(time(NULL));
		for (int i = 0; i < num_fishes; i++) {
			Fish fish;
			fish.x = (float)rand() / RAND_MAX * 2 - 1;
			fish.y = (float)rand() / RAND_MAX * 2 - 1;
			fish.dx = (float)rand() / RAND_MAX * 0.02 - 0.01;
			fish.dy = (float)rand() / RAND_MAX * 0.02 - 0.01;
			fish.angle = 0.0f;
			fishes.push_back(fish);
		}
	}

	// Update fish positions
	void update(float dt) {
		for (int i = 0; i < num_fishes; i++) {
			fishes[i].x += fishes[i].dx * dt;
			fishes[i].y += fishes[i].dy * dt;

			// Bounce off edges
			if (fishes[i].x < -1.0f || fishes[i].x > 1.0f) {
				fishes[i].dx = -fishes[i].dx;
			}
			if (fishes[i].y < -1.0f || fishes[i].y > 1.0f) {
				fishes[i].dy = -fishes[i].dy;
			}

			// Update rotation angle
			fishes[i].angle += dt * 2.0f;
		}
	}

	// Render fish sprites
	void render() {
		glClear(GL_COLOR_BUFFER_BIT);

		glUseProgram(program);

		// Set up model-view-projection matrix
		float mvpMatrix[16] = {
			1.0f, 0.0f, 0.0f, 0.0f,
			0.0f, 1.0f, 0.0f, 0.0f,
			0.0f, 0.0f, 1.0f, 0.0f,
			0.0f, 0.0f, 0.0f, 1.0f
		};
		GLint mvpMatrixLocation = glGetUniformLocation(program, "u_mvpMatrix");
		glUniformMatrix4fv(mvpMatrixLocation, 1, GL_FALSE, mvpMatrix);

		// Set up vertex attributes
		GLint positionLocation = glGetAttribLocation(program, "a_position");
		glEnableVertexAttribArray(positionLocation);
		glVertexAttribPointer(positionLocation, 3, GL_FLOAT, GL_FALSE, 5 * sizeof(GLfloat), (void*)0);

		GLint texCoordLocation = glGetAttribLocation(program, "a_texCoord");
		glEnableVertexAttribArray(texCoordLocation);
		glVertexAttribPointer(texCoordLocation, 2, GL_FLOAT, GL_FALSE, 5 * sizeof(GLfloat), (void*)(3 * sizeof(GLfloat)));

		// Render each fish
		for (int i = 0; i < num_fishes; i++) {
			// Set up model matrix for this fish
			float modelMatrix[16] = {
				cosf(fishes[i].angle), -sinf(fishes[i].angle), 0.0f, 0.0f,
				sinf(fishes[i].angle), cosf(fishes[i].angle), 0.0f, 0.0f,
				0.0f, 0.0f, 1.0f, 0.0f,
				fishes[i].x, fishes[i].y, 0.0f, 1.0f
			};

			// Combine model and projection matrices
			float combinedMatrix[16];
			for (int j = 0; j < 16; j++) {
				combinedMatrix[j] = 0.0f;
				for (int k = 0; k < 4; k++) {
					combinedMatrix[j] += mvpMatrix[j / 4 * 4 + k] * modelMatrix[k * 4 + j % 4];
				}
			}

			// Update MVP matrix uniform
			glUniformMatrix4fv(mvpMatrixLocation, 1, GL_FALSE, combinedMatrix);

			// Draw the fish sprite
			glDrawArrays(GL_TRIANGLE_STRIP, 0, 4);
		}

		glDisableVertexAttribArray(positionLocation);
		glDisableVertexAttribArray(texCoordLocation);
	}

	~Fishes() { /* dtor */
		glDeleteProgram(program);
		glDeleteBuffers(1, &vbo);
	}
};
```

******************************************

## Request to release *OpenGLES2* fish through *Apache 2* / *GPLv2*
**Q**: "Wish to publish this as *Apache 2* / *GPLv2*"
### *Grok-2* allows to release *OpenGLES2* fish through *Apache 2* / *GPLv2*
> To publish your code under both the Apache License 2.0 and GPLv2, you need to be aware of the compatibility issues between these licenses. The Apache License 2.0 is generally considered compatible with GPLv2, but there are some considerations to keep in mind.
>
> Here's a step-by-step guide to properly license your code under both Apache License 2.0 and GPLv2:
>
> 1. **Choose a primary license**: Since GPLv2 is considered a "strong copyleft" license, it's typically used as the primary license when dual-licensing with Apache License 2.0. This means that any derivative works must be distributed under GPLv2.
>
> 2. **Add license headers**: Include license headers at the top of your source files. Here's an example of how you might structure the header for your `fish.c` file:
>
> ```c
> /*
>  * Copyright [Year] [Your Name or Organization]
>  *
>  * This program is free software; you can redistribute it and/or modify
>  * it under the terms of the GNU General Public License version 2 as
>  * published by the Free Software Foundation.
>  *
>  * Alternatively, this software may be distributed under the terms of Apache
>  * License Version 2.0.
>  *
>  * This program is distributed in the hope that it will be useful,
>  * but WITHOUT ANY WARRANTY; without even the implied warranty of
>  * MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the
>  * GNU General Public License for more details.
>  *
>  * You should have received a copy of the GNU General Public License along
>  * with this program; if not, write to the Free Software Foundation, Inc.,
>  * 51 Franklin Street, Fifth Floor, Boston, MA 02110-1301 USA.
>  *
>  * You should have received a copy of the Apache License Version 2.0 along
>  * with this program; if not, see <https://www.apache.org/licenses/LICENSE-2.0>.
>  */
> ```
>
> 3. **Include full license texts**: Include the full text of both licenses in your project. Create two separate files:
>    - `LICENSE-GPLv2.txt`: Copy the full text of the GPLv2 license into this file.
>    - `LICENSE-Apache-2.0.txt`: Copy the full text of the Apache License 2.0 into this file.
>
> 4. **README file**: In your project's README file, explain the dual licensing. Here's an example:
>
> ```
> # Fish Sprite Animation
>
> This project is dual-licensed under the GNU General Public License version 2 (GPLv2) and the Apache License Version 2.0.
>
> You may choose to use this software under either license.
>
> - For GPLv2: See LICENSE-GPLv2.txt
> - For Apache License 2.0: See LICENSE-Apache-2.0.txt
>
> When using this software, please ensure you comply with the terms of the chosen license.
> ```
>
> 5. **Considerations**:
>    - Be aware that if someone modifies your code and distributes it under GPLv2, they must also distribute their modifications under GPLv2.
>    - If someone uses your code under the Apache License 2.0, they can incorporate it into proprietary software, but they must include the Apache License notice and any required notices in their distribution.
>
> 6. **Year and Copyright Holder**: Replace `[Year]` with the year you're publishing the code, and `[Your Name or Organization]` with your actual name or organization.
>
> By following these steps, you'll have properly dual-licensed your code under both Apache License 2.0 and GPLv2. Remember to update the year and copyright holder information as needed in future releases.

`[Year]` above is `2025`, `[Your Name or Organization]` is `https://github.com/SwuduSusuwu/ with assistance of https://poe.com/Grok-2`.

******************************************

# Request *Java* fish
**Q**: "Wish that you produce *Java* source code for a fish sim"

Result: simple [_Java_](https://www.java.com/en/download/help/whatis_java.html) [fish sim](#solar-pro-2s-java-fish) ([produced through _Solar-Pro-2_](https://poe.com/s/ehlOJYRJNsrGJttfJ4HK); [released through *Apache 2* + *GPLv2*](#request-to-release-java-fish-through-apache-2--gplv2)).

******************************************

Notice: improved [_Solar-Pro-2_'s original source code](https://github.com/SwuduSusuwu/SusuPosts/blob/a83a3d619c560e15891b3d2d18dcadecda6f87b7/posts/Human_ancestors_are_fish.md#solar-pro-2s-java-fish) as this list shows:
* `:%s/, 0, 0, 0/, 0, 0/`: fixes "error: method rotate in class Transform cannot be applied to given types; ... actual and formal argument lists differ in length"
* [introduced `frameCount`, `lastTime`, `fps`, `fpsText`](https://github.com/SwuduSusuwu/SusuPosts/commit/a4128662b24ce177f333508250cfba66cefe7109) to show **FPS** ([produced through _Solar-Pro-2_](https://poe.com/s/OSENRaU2uCb4TznzRPas)).
  * improved `AnimationTimer::handle()`: to show true **FPS**, plus to not to redraw `fpsText` until `fps` changes.
  * refactored `Fish::applySeparation()` to reuse values.
  * refactored `Fish::applyWallAvoidance()` to reuse values, plus replace [magic constants](https://stackoverflow.com/questions/43950998/what-are-symbolic-constants-and-magic-constants) with `BOUNDS_DISTANCE`.
  * improved `Fish::update()` so if rotation is miniscule, this reuses transforms (to improve **FPS**, but **FPS** is too unstable to notice differences.)
* introduced `*_FACTOR` (`= 1` for original results), to scale `Fish::apply*()` forces.
  * increased `SEPARATION_FACTOR` (from `1`) to `2`, so schools are loose enough to view individual fish.
  * decreased `SEPARATION_DISTANCE` (from `50`) to `22`, so fish still school.
* increased `WIDTH` (from `800`) to `1280`, increased `HEIGHT` (from `600`) to `720`, since most computers (plus smartphones) can show *720p* resolution.
  * increased `FISH_COUNT` (from `50`) to `102`, since the window now has more room.
* improved `Fish::createFishShape()` to produce 2 colors of fish.
  * introduced `Fish::isSimilarTo()`: to limit schools to similar fish.
  * introduced `SEPARATION_NONSIMILAR_DISTANCE`, so `Fish::applySeparation()` can use `isSimilarTo()`.
  * improved `Fish::applyAlignment()` / `Fish::applyCohesion()`: now use `Fish::isSimilarTo()`.
  * this is now close to a fluid particle sim which has 2 types of molecules which group to similar molecules (such as [oleophilic compounds](https://thepetrosolutions.com/forums/topic/difference-between-oleophobic-and-oleophilic-impurities/#post-3508)) plus separate from nonsimilar molecules ([such as oleophobic compounds](https://poe.com/s/dYx54tOaDTaDnaBT9TRm)), except the numerous steps of *Boids* formula cause some emergent phenomenon which simple molecules do not possess.

******************************************

Notice: [Used *Solar-Pro-2* to improve codeflow](https://github.com/SwuduSusuwu/SusuPosts/commit/40aa328886832b0d7753f8b016e95d2163f898d6) (of the ancestor `git commit` --- which was "1 / 2" human-produced source code --- to thus) [so `fps` improves](https://poe.com/s/ifeHY8AcpVmVC7R5aPB7):
* moves `Fish`-specific constants from `FishSim` into `Fish`.
* uses `java.util.concurrent.Executor{s,Service}` to offload `apply*()` motions.
* introduces `GRID_SIZE`, which `updateFish()` now uses (to split `List<Fish> fishList` into `List<Fish>[][] grid` (which reduces *O(n^2)* to *O(n^2 / (WIDTH / GRID_SIZE) / (HEIGHT / GRID_SIZE))* **CPU** use)).
* replaces `javafx.scene.shape.Polygon` with {`javafx.scene.canvas.Canvas`, `javafx.scene.canvas.GraphicsContext`}.
* replaces `1.0 / 2 < random.nextDouble()` with `random.nextBoolean()`.
* replaces {`Fish::createFishShape()`, `Fish::getShape()`} with {`Fish::render()`, `FishSim::renderFish()`}.
* improves `Fish::update()` so that fish wrap around (to opposite edges) if out-of-bounds.
* increases resolution to 2600\*1600 (oops; the goal was to support larger resolutions, not default to those).
* Notice: Own improvements to those above:
  * Documents minimum `GRID_SIZE` which enforces `*_DISTANCE`s.
  * Replaces magic constants (`100`) in `applyFlockingRules()` with `GRID_SIZE` (fixes undefined behaviour if `GRID_SIZE` changes).
  * Replaces magic constants ({`2600`, `1600`}) in {`Fish::applyFlockingRules()`, `Fish::update()`} with {`WIDTH`, `HEIGHT`}.
  * Reduces `UPDATE_INTERVAL` (from `5`) to `2` (since `ExecutorService` is used, this does not lower `fps`) so physics is smooth.
  * Revert to *720p* resolution (so this is still compatible with old computers or smartphones).
  * Reintroduced `Fish::isSimilarTo()`, to allow close matches.
  * Document future `Fish::setPos()`, which will have alternatives (versus wraparound) to ensure `Fish` are in bounds.

******************************************

Notice: use `sudo apt install openjfx openjdk-25-jdk-headless` for the packages on *Ubuntu*.
* use `PATH_TO_FX=/usr/share/openjfx/lib/` to build on *Ubuntu*.

******************************************

## [*Solar-Pro-2*](https://poe.com/Solar-Pro-2)'s *Java* fish
> Below is a complete Java source code for a simple 2D fish simulation using JavaFX. This simulation will have multiple fish that move around the screen, avoid walls, and follow basic flocking behavior (separation, alignment, cohesion).
>
> ### ✅ Features of this simulation:
> - Multiple fish with simple shapes
> - Basic flocking behavior (Boids algorithm simplified)
> - Wall avoidance
> - Random initial positions and velocities
> - JavaFX for rendering and animation
>
> ---
>
> ## 📁 File: `FishSim.java`

```java
import javafx.animation.AnimationTimer;
import javafx.application.Application;
import javafx.application.Platform;
import javafx.scene.Scene;
import javafx.scene.canvas.Canvas;
import javafx.scene.canvas.GraphicsContext;
import javafx.scene.layout.Pane;
import javafx.scene.paint.Color;
import javafx.scene.text.Text;
import javafx.stage.Stage;
import java.util.ArrayList;
import java.util.List;
import java.util.Random;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class FishSim extends Application {

	private static final int WIDTH = 1280;
	private static final int HEIGHT = 720;
	private static final int FISH_COUNT = 102;
	private static final int GRID_SIZE = 100; // Notice: set this to `Colllections.max({*_DISTANCE})` (which should equal what most sims call "view distance"), so that all relevent `Fish` are processed.
	private static final int UPDATE_INTERVAL = 2; // The `frameCounter` per `Fish::applyFlockingRulesUpdate()`

	private List<Fish> fishList = new ArrayList<>();
	private Random random = new Random();
	private Pane root = new Pane();
	private Canvas canvas = new Canvas(WIDTH, HEIGHT);
	private GraphicsContext gc = canvas.getGraphicsContext2D();

	private Text fpsText = new Text("0 FPS");
	private int frameCount = 0;
	private long lastTime = System.nanoTime();
	private double fps = 0;
	private int frameCounter = 0;

	private ExecutorService executor = Executors.newSingleThreadExecutor();

	public static void main(String[] args) {
		launch(args);
	}

	@Override
	public void start(Stage primaryStage) {
		// Initialize fish
		for (int i = 0; i < FISH_COUNT; i++) {
			double x = random.nextDouble() * WIDTH;
			double y = random.nextDouble() * HEIGHT;
			double dx = (random.nextDouble() * 2 - 1) * Fish.MAX_SPEED;
			double dy = (random.nextDouble() * 2 - 1) * Fish.MAX_SPEED;
			fishList.add(new Fish(x, y, dx, dy, random.nextBoolean() ? Color.BLUE : Color.GREEN));
		}

		root.getChildren().add(canvas);
		root.getChildren().add(fpsText);

		Scene scene = new Scene(root, WIDTH, HEIGHT, Color.LIGHTBLUE);
		primaryStage.setScene(scene);
		primaryStage.setTitle("Fish Simulation (Boids)");
		primaryStage.setResizable(false);
		primaryStage.show();

		fpsText.setX(10);
		fpsText.setY(30);
		fpsText.setFill(Color.WHITE);

		// Start animation loop
		new AnimationTimer() {
			@Override
			public void handle(long now) {
				frameCounter++;
				if (frameCounter % UPDATE_INTERVAL == 0) {
					executor.submit(() -> updateFish());
				}

				renderFish();

				double elapsed = (now - lastTime) / 1_000_000_000.0;
				if (elapsed >= 1.0) {
					lastTime = now;
					fps = frameCount / elapsed;
					Platform.runLater(() -> {
						fpsText.setText(String.format("%.1f FPS", fps));
					});
					frameCount = 0;
				} else {
					frameCount++;
				}
			}
		}.start();
	}

	private void updateFish() {
		// Use spatial partitioning (simple grid system)
		List<Fish>[][] grid = new ArrayList[WIDTH / GRID_SIZE][HEIGHT / GRID_SIZE];
		for (int i = 0; i < WIDTH / GRID_SIZE; i++) {
			for (int j = 0; j < HEIGHT / GRID_SIZE; j++) {
				grid[i][j] = new ArrayList<>();
			}
		}

		// Assign fish to grid cells
		for (Fish fish : fishList) {
			int gridX = (int) (fish.x / GRID_SIZE);
			int gridY = (int) (fish.y / GRID_SIZE);
			if (gridX >= 0 && gridX < WIDTH / GRID_SIZE && gridY >= 0 && gridY < HEIGHT / GRID_SIZE) {
				grid[gridX][gridY].add(fish);
			}
		}

		// Update each fish
		for (Fish fish : fishList) {
			fish.applyFlockingRules(fishList, grid);
			fish.update();
		}
	}

	private void renderFish() {
		gc.clearRect(0, 0, WIDTH, HEIGHT);
		for (Fish fish : fishList) {
			fish.render(gc);
		}
	}

	@Override
	public void stop() {
		executor.shutdown();
	}

	private static class Fish {
		private static final double SEPARATION_DISTANCE = 22;
		private static final double SEPARATION_FACTOR = 2;
		private static final double SEPARATION_NONSIMILAR_DISTANCE = 42;
		private static final double SEPARATION_NONSIMILAR_FACTOR = 2.2;
		private static final double ALIGNMENT_DISTANCE = 100;
		private static final double ALIGNMENT_FACTOR = 1;
		private static final double COHESION_DISTANCE = 100;
		private static final double COHESION_FACTOR = 1;
		private static final double BOUNDS_DISTANCE = 20;
		private static final double BOUNDS_FACTOR = 1;
		private static final double MAX_SPEED = 3.0;
		private static final double ACCELERATION = 0.1;

		private double x, y;        // Position
		private double dx, dy;      // Velocity
		private Color color;

		public Fish(double x, double y, double dx, double dy, Color color) {
			this.x = x;
			this.y = y;
			this.dx = dx;
			this.dy = dy;
			this.color = color;
		}

		public boolean isSimilarTo(Fish other) {
			return color.equals(other.color); /* TODO: use `Math.hypot()` (Euclidean distance) of color component differences, to allow close matches. Use a function (such as `javafx.scene.shape.Polygon.getPoints()`), for comparison of vertices. */
		}

		public void applyFlockingRules(List<Fish> allFish, List<Fish>[][] grid) {
			int gridX = (int) (x / GRID_SIZE);
			int gridY = (int) (y / GRID_SIZE);
			List<Fish> nearbyFish = new ArrayList<>();

			// Check neighboring grid cells
			for (int i = Math.max(0, gridX - 1); i <= Math.min(grid.length - 1, gridX + 1); i++) {
				for (int j = Math.max(0, gridY - 1); j <= Math.min(grid[0].length - 1, gridY + 1); j++) {
					nearbyFish.addAll(grid[i][j]);
				}
			}

			applySeparation(nearbyFish);
			applyAlignment(nearbyFish);
			applyCohesion(nearbyFish);
			applyWallAvoidance(WIDTH, HEIGHT);
		}

		private void applySeparation(List<Fish> nearbyFish) {
			double sepX = 0, sepY = 0;
			double sepNonsimilarX = 0, sepNonsimilarY = 0;
			int count = 0, countNonsimilar = 0;

			for (Fish other : nearbyFish) {
				if (other != this) {
					double diffX = x - other.x;
					double diffY = y - other.y;
					double dist = Math.hypot(diffX, diffY);
					if (isSimilarTo(other)) {
						if (dist < SEPARATION_DISTANCE) {
							sepX += diffX / dist;
							sepY += diffY / dist;
							count++;
						}
					} else {
						if (dist < SEPARATION_NONSIMILAR_DISTANCE) {
							sepNonsimilarX += diffX / dist;
							sepNonsimilarY += diffY / dist;
							countNonsimilar++;
						}
					}
				}
			}

			if (count > 0) {
				sepX /= count;
				sepY /= count;
				double sepLength = Math.sqrt(sepX * sepX + sepY * sepY);
				if (sepLength > 0) {
					dx += (sepX / sepLength) * ACCELERATION * SEPARATION_FACTOR;
					dy += (sepY / sepLength) * ACCELERATION * SEPARATION_FACTOR;
				}
			}
			if (countNonsimilar > 0) {
				sepNonsimilarX /= countNonsimilar;
				sepNonsimilarY /= countNonsimilar;
				double sepLength = Math.sqrt(sepNonsimilarX * sepNonsimilarX + sepNonsimilarY * sepNonsimilarY);
				if (sepLength > 0) {
					dx += (sepNonsimilarX / sepLength) * ACCELERATION * SEPARATION_NONSIMILAR_FACTOR;
					dy += (sepNonsimilarY / sepLength) * ACCELERATION * SEPARATION_NONSIMILAR_FACTOR;
				}
			}
		}

		private void applyAlignment(List<Fish> nearbyFish) {
			double avgDX = 0, avgDY = 0;
			int count = 0;

			for (Fish other : nearbyFish) {
				if (other != this && isSimilarTo(other)) {
					double dist = Math.hypot(x - other.x, y - other.y);
					if (dist < ALIGNMENT_DISTANCE) {
						avgDX += other.dx;
						avgDY += other.dy;
						count++;
					}
				}
			}

			if (count > 0) {
				avgDX /= count;
				avgDY /= count;
				double length = Math.sqrt(avgDX * avgDX + avgDY * avgDY);
				if (length > 0) {
					avgDX = (avgDX / length) * ACCELERATION * ALIGNMENT_FACTOR;
					avgDY = (avgDY / length) * ACCELERATION * ALIGNMENT_FACTOR;
				}
				dx += avgDX;
				dy += avgDY;
			}
		}

		private void applyCohesion(List<Fish> nearbyFish) {
			double avgX = 0, avgY = 0;
			int count = 0;

			for (Fish other : nearbyFish) {
				if (other != this && isSimilarTo(other)) {
					double dist = Math.hypot(x - other.x, y - other.y);
					if (dist < COHESION_DISTANCE) {
						avgX += other.x;
						avgY += other.y;
						count++;
					}
				}
			}

			if (count > 0) {
				avgX = (avgX / count) - x;
				avgY = (avgY / count) - y;
				double length = Math.sqrt(avgX * avgX + avgY * avgY);
				if (length > 0) {
					avgX = (avgX / length) * ACCELERATION * COHESION_FACTOR;
					avgY = (avgY / length) * ACCELERATION * COHESION_FACTOR;
				}
				dx += avgX;
				dy += avgY;
			}
		}

		private void applyWallAvoidance(double width, double height) {
			double avoidanceX = 0, avoidanceY = 0;

			if (x < BOUNDS_DISTANCE) {
				avoidanceX += (BOUNDS_DISTANCE - x);
			}
			if (x > width - BOUNDS_DISTANCE) {
				avoidanceX -= (x - (width - BOUNDS_DISTANCE));
			}
			if (y < BOUNDS_DISTANCE) {
				avoidanceY += (BOUNDS_DISTANCE - y);
			}
			if (y > height - BOUNDS_DISTANCE) {
				avoidanceY -= (y - (height - BOUNDS_DISTANCE));
			}

			dx += avoidanceX / BOUNDS_DISTANCE * ACCELERATION * BOUNDS_FACTOR;
			dy += avoidanceY / BOUNDS_DISTANCE * ACCELERATION * BOUNDS_FACTOR;
		}

		public void update() {
			// Limit speed
			double speed = Math.sqrt(dx * dx + dy * dy);
			if (speed > MAX_SPEED) {
				dx = (dx / speed) * MAX_SPEED;
				dy = (dy / speed) * MAX_SPEED;
			}

			// Update position // TODO: move into future `Fish::setPos()`, which shall have the invariant `Fish.pos <= FishSim.resolution` established.
			x += dx;
			y += dy;

			// Wrap around screen // TODO: move into future `Fish::setPos()`, as one numerous (optional) solutions which ensure `Fish.pos <= FishSim.resolution` is established.
			x = (x + WIDTH) % WIDTH;
			y = (y + HEIGHT) % HEIGHT;
		}

		public void render(GraphicsContext gc) {
			gc.save();
			gc.translate(x, y);
			gc.rotate(Math.toDegrees(Math.atan2(dy, dx)) + 90);
			gc.setFill(color);
			gc.beginPath();
			gc.moveTo(0, -10);
			gc.lineTo(-5, 10);
			gc.lineTo(-2, 0);
			gc.lineTo(2, 0);
			gc.lineTo(5, 10);
			gc.closePath();
			gc.fill();
			gc.restore();
		}
	}
}
```

> This completes the Java source code for the fish simulation. Let me provide a brief explanation of how the simulation works:
>
> ### 🔍 How the Simulation Works
>
> 1. **Fish Representation**:
>    - Each fish is represented by a `Polygon` shape resembling a fish.
>    - Each fish has a position `(x, y)` and velocity `(dx, dy)`.
>
> 2. **Flocking Behavior**:
>    - **Separation**: Fish try to stay away from nearby fish to avoid crowding.
>    - **Alignment**: Fish try to align their direction with nearby fish.
>    - **Cohesion**: Fish try to move towards the average position of nearby fish.
>    - These rules are based on the Boids algorithm.
>
> 3. **Wall Avoidance**:
>    - Fish steer away from the edges of the screen to avoid going out of bounds.
>
> 4. **JavaFX Animation**:
>    - The simulation runs in an `AnimationTimer` loop, updating fish positions and behaviors every frame.
>    - The fish shapes are updated to reflect their new positions and directions.
>
> ### 🧪 How to Run the Simulation:
> 1. Save the code in a file named `FishSim.java`.
> 2. Compile it with:
>   ```bash
>   javac --module-path $PATH_TO_FX --add-modules javafx.controls,javafx.fxml FishSim.java
>   ```
>   (Make sure to replace `$PATH_TO_FX` with the actual path to your JavaFX SDK.)
> 3. Run it with:
>   ```bash
>   java --module-path $PATH_TO_FX --add-modules javafx.controls,javafx.fxml FishSim
>   ```
>
> ### 🎯 Enhancements You Could Add:
> - Add obstacles for fish to navigate around.
> - Implement predator-prey dynamics with different types of fish.
> - Add visual effects like trails or bubbles.
> - Implement steering behaviors like obstacle avoidance or path following.
>
> Let me know if you'd like any of these enhancements or further modifications!

******************************************

## Request to release *Java* fish through *Apache 2* / *GPLv2*
**Q**: "Am allowed to publish this as *Apache 2* / *GPLv2*?"
### *Solar-Pro-2* allows to release *Java* fish through *Apache 2* / *GPLv2*
> Absolutely! You are allowed to publish this Java fish simulation source code under either the **Apache License 2.0** or the **GNU General Public License v2.0 (GPLv2)**. Here’s what you need to know:
>
> ### ✅ Licensing Compatibility
> - **Apache 2.0** and **GPLv2** are both open-source licenses, but they have key differences:
>   - **Apache 2.0** is a permissive license, allowing proprietary derivatives.
>   - **GPLv2** is copyleft, requiring derivatives to also be licensed under GPLv2 (or compatible licenses).
> - The two licenses are **not directly compatible**—code under GPLv2 cannot be relicensed under Apache 2.0 without permission from all copyright holders. However, you can choose **one** of them for this code.
>
> ### ✅ Steps to Publish Under Your Chosen License
> 1. **Choose One License** (either Apache 2.0 or GPLv2—**not both** unless you’re creating a dual-licensed project, which is more complex).
> 2. **Add the License Text** to your project (typically in a file named `LICENSE` or `COPYING`).
> 3. **Add a License Header** to the source file(s) if required by the license (Apache 2.0 recommends this, GPLv2 does not strictly require it but it’s good practice).
>
> ### 📄 Example License Headers
> #### For Apache 2.0:
> ```java
> /*
>  * Licensed under the Apache License, Version 2.0 (the "License");
>  * you may not use this file except in compliance with the License.
>  * You may obtain a copy of the License at
>  *
>  *     http://www.apache.org/licenses/LICENSE-2.0
>  *
>  * Unless required by applicable law or agreed to in writing, software
>  * distributed under the License is distributed on an "AS IS" BASIS,
>  * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
>  * See the License for the specific language governing permissions and
>  * limitations under the License.
>  */
> ```
>
> #### For GPLv2:
> ```java
> /*
>  * FishSim.java
>  *
>  * This program is free software; you can redistribute it and/or modify
>  * it under the terms of the GNU General Public License as published by
>  * the Free Software Foundation; either version 2 of the License, or
>  * (at your option) any later version.
>  *
>  * This program is distributed in the hope that it will be useful,
>  * but WITHOUT ANY WARRANTY; without even the implied warranty of
>  * MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
>  * GNU General Public License for more details.
>  *
>  * You should have received a copy of the GNU General Public License along
>  * with this program; if not, write to the Free Software Foundation, Inc.,
>  * 51 Franklin Street, Fifth Floor, Boston, MA 02110-1301 USA.
>  */
> ```
>
> ### 📌 Recommendation
> - If you want **maximum permissiveness** (e.g., for reuse in commercial/proprietary projects), choose **Apache 2.0**.
> - If you want to **ensure all derivatives remain open-source**, choose **GPLv2**.
>
> Let me know if you’d like help drafting a full `LICENSE` file for either license!

******************************************

# Synopsis
* **Q**: "Produce a C++ `class fish` which does a fish sim". [*Grok-2*'s *C++* fish sim](https://poe.com/s/fPpFTNwFxeOUjXuKnSu4)
* **Q**: "Use GLFW+Vulkan to produce virtual fish which swim around". [*Solar-Pro-2*'s *GLFW* + *Vulkan* fish sim](https://poe.com/s/Ou5DxBJQKdLeaRKhvxYK)

