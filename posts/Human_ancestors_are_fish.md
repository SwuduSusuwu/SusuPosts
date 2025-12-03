**[fēl-is pisc-em cēpit "the cat caught the fish" to fēl-em pisc-is cēpit "the fish caught the cat"](https://en.wikipedia.org/wiki/Analytic_language#:~:text=fish). Human ancestors are fish.**

\[[This post](https://swudususuwu.substack.com/p/the-cat-caught-the-fish) allows [all uses](https://creativecommons.org/licenses/by/2.0/).\]

# Table of Contents
- [Intro](#intro)
- [*OpenGLES2* fish](#request-opengles2-fish)
  - [*OpenGLES2* fish released through *Apache 2* + *GPLv2*](#request-to-release-opengles2-fish-through-apache-2--gplv2)
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

// Structure to represent a fish
typedef struct {
	float x, y;  // Position
	float dx, dy;  // Velocity
	float angle;  // Rotation angle
} Fish;

// Global variables
GLuint program;
GLuint vbo;
Fish *fishes;
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
void init() {
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

	// Initialize fish array
	num_fishes = 10;
	fishes = malloc(num_fishes);
	srand(time(NULL));
	for (int i = 0; i < num_fishes; i++) {
		fishes[i].x = (float)rand() / RAND_MAX * 2 - 1;
		fishes[i].y = (float)rand() / RAND_MAX * 2 - 1;
		fishes[i].dx = (float)rand() / RAND_MAX * 0.02 - 0.01;
		fishes[i].dy = (float)rand() / RAND_MAX * 0.02 - 0.01;
		fishes[i].angle = 0.0f;
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

// Clean up resources
void cleanup() {
	glDeleteProgram(program);
	glDeleteBuffers(1, &vbo);
	free(fishes);
}
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

# Synopsis
* **Q**: "Produce a C++ `class fish` which does a fish sim". [*Grok-2*'s *C++* fish sim](https://poe.com/s/fPpFTNwFxeOUjXuKnSu4)
* **Q**: "Use GLFW+Vulkan to produce virtual fish which swim around". [*Solar-Pro-2*'s *GLFW* + *Vulkan* fish sim](https://poe.com/s/Ou5DxBJQKdLeaRKhvxYK)

