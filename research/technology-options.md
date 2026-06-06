# Technology Options for Browser Pong

Research Mode output. This note compares technology and deployment options for a browser-based Pong game before requirements are written. It does not recommend a final choice or record a project decision.

## Sources Checked

- MDN Canvas API documentation: Canvas is a browser API for drawing graphics with JavaScript and the `canvas` element, including animation and game graphics. It is widely available across browsers.
- MDN `requestAnimationFrame()` documentation: animation callbacks are synchronized with browser repaint; timing should use the callback timestamp to avoid speed changes on high-refresh-rate displays.
- MDN JavaScript modules and same-origin policy documentation: local `file://` testing can trigger CORS issues, especially with modules or resource loading.
- Phaser official download pages: Phaser v4.1.0 "Salusa" was released on April 30, 2026 and is available from npm, jsDelivr, and cdnjs. Phaser v3.90.0 remains visible in official docs and CDN listings, so version choice may matter.
- jsDelivr CDN file listings: current Phaser and p5.js CDN file sizes were checked from CDN listings.
- p5.js official getting-started documentation: p5 projects commonly use `index.html`, `style.css`, and `sketch.js`; `setup()` runs once and `draw()` loops by default.
- GitHub Pages documentation: GitHub Pages hosts static HTML, CSS, and JavaScript from a repository and may optionally run a build process.
- Netlify documentation: Netlify can deploy static site files by Git, CLI, or drag-and-drop.
- Vercel documentation: static HTML/CSS/client-side JavaScript projects do not require a build step when configured as a static site.

## 1. Technology Stack Options

### A. Vanilla JavaScript with HTML5 Canvas API

What it provides out of the box:

- A built-in browser drawing surface through `<canvas>` and the 2D rendering context.
- Primitive drawing operations for rectangles, lines, text, colors, clearing, transforms, and pixel/image operations.
- Browser-native input events through JavaScript, such as keyboard and pointer events.
- Browser-native animation timing through `requestAnimationFrame()`.

What it does not provide out of the box:

- No game object model.
- No built-in collision system.
- No physics engine.
- No scene/state manager.
- No asset loader beyond normal browser APIs.
- No score or UI framework.

Dependencies required:

- No third-party dependency.
- File size overhead is effectively 0 KB beyond the game files.
- No CDN dependency is required.

Complexity for basic JavaScript knowledge:

- Conceptually direct for Pong because the game entities are simple: two paddles, one ball, score text, boundaries, and input state.
- Requires the developer to write the game loop, collision checks, score updates, reset behavior, and rendering order.
- The main learning points are canvas coordinates, frame timing, input state, and separating update logic from draw logic.

Suitability for a small, self-contained browser game:

- Strong fit when the goal is a compact, transparent, self-contained implementation.
- Best when the game stays close to classic Pong and does not need a general-purpose game framework.
- Becomes more work if the project later wants menus, animation systems, audio management, mobile scaling, particles, scenes, or asset-heavy features.

Build step or plain HTML:

- Can run as a plain HTML file with inline JavaScript or classic `<script src="">` files.
- A build step is not required.
- If JavaScript modules are used, local `file://` testing may hit browser security restrictions; a small local static server may be needed for development.

Priority-dependent areas:

- If "single file and no dependency" is a major project priority, vanilla Canvas has the fewest external moving parts.
- If "learn game engine patterns" or "expand beyond Pong later" is a priority, vanilla Canvas provides less structure.
- If deterministic frame-rate behavior matters, update logic should account for `requestAnimationFrame()` timestamps rather than assuming 60 FPS.

### B. Phaser.js

What it provides out of the box:

- A browser game framework for 2D games using Canvas/WebGL rendering.
- Game configuration, scenes, game objects, input handling, asset loading, animation support, tweens, sound, timing, scaling, and physics systems.
- Arcade Physics can handle simple collision-style behavior that maps well to a Pong ball and paddles.
- A larger ecosystem of examples, tutorials, launcher tooling, and docs.

What still needs to be implemented for Pong:

- Game rules, scoring, paddle behavior, ball reset behavior, win condition, and visual design.
- Decisions about whether to use physics objects or simpler manual movement.

Dependencies required:

- Phaser is a third-party JavaScript dependency.
- Current official Phaser release checked: v4.1.0, released April 30, 2026.
- CDN availability: official Phaser download pages list jsDelivr and cdnjs URLs.
- jsDelivr file size checked for Phaser 4.1.0:
  - `phaser.min.js`: about 1.29 MB.
  - `phaser-arcade-physics.min.js`: about 1.18 MB.
- Phaser 3.90.0 is also present in official docs and CDN listings:
  - `phaser.min.js`: about 1.14 MB.
  - `phaser-arcade-physics.min.js`: about 1.04 MB.
- Gzip transfer size may be smaller than raw CDN listing size depending on host/server compression.

Complexity for basic JavaScript knowledge:

- Higher initial conceptual overhead than vanilla Canvas because the developer must learn Phaser's lifecycle, scene structure, game object APIs, preload/create/update patterns, and physics/input conventions.
- Potentially lower implementation burden once the framework concepts are understood.
- For a very small Pong game, some framework features may feel larger than the game itself.

Suitability for a small, self-contained browser game:

- Suitable if the project values framework structure, built-in systems, or likely expansion.
- May be heavier than necessary for a minimal classic Pong.
- Useful if future requirements may include menus, sound, multiple screens, effects, game states, mobile scaling, or more complex collision behavior.

Build step or plain HTML:

- Can run from a script tag using CDN-hosted Phaser; a build step is not inherently required.
- Phaser's create-game tooling can set up npm and bundlers such as Vite, but that is optional.
- If assets are loaded from separate files, local development is usually more reliable through a local server than `file://`.

Priority-dependent areas:

- Version choice matters: Phaser 4.1.0 is current as of this research, but Phaser 3 has extensive established tutorials and examples. The answer depends on whether the project prioritizes newest release or older learning material.
- The dependency cost may matter if the game must be tiny, fully inspectable, or embedded in one HTML file.
- Framework structure may be valuable if the project is a learning exercise in browser game architecture, not only Pong mechanics.

### C. p5.js

What it provides out of the box:

- A creative-coding library centered on drawing, animation, and interaction.
- A friendly sketch structure with `setup()` and `draw()`.
- Helpers for canvas creation, drawing shapes/text, color, input, random values, math utilities, and animation loops.
- A beginner-friendly programming model influenced by Processing.

What it does not provide out of the box:

- No full game framework structure like scenes, loaders, or built-in game object lifecycle.
- No built-in Pong-specific collision or physics engine in the core library.
- Game rules, collision, scoring, and state management still need to be written.

Dependencies required:

- p5.js is a third-party JavaScript dependency.
- CDN availability: jsDelivr and cdnjs provide p5.js files.
- Current jsDelivr listing checked: p5 v2.3.0.
- jsDelivr file size checked for p5 v2.3.0:
  - `p5.min.js`: about 959.27 KB.
  - `p5.esm.min.js`: about 1.04 MB.
- The p5 Web Editor default may lag behind npm/latest release lines, so version choice should be pinned rather than left implicit.

Complexity for basic JavaScript knowledge:

- Low barrier for drawing and animation because the sketch model is compact.
- Easier than raw Canvas for common drawing operations.
- Less game-specific than Phaser, so the developer still needs to structure game state, collision, input, and scoring.
- Some p5 conventions abstract the underlying browser APIs, which can be helpful for learning creative coding but may hide plain JavaScript/browser mechanics.

Suitability for a small, self-contained browser game:

- Good fit for a small visual sketch-like Pong implementation.
- Less appropriate if the project wants engine-like structure, multiple scenes, asset management, or game-specific systems.
- More dependency weight than vanilla Canvas for a game whose graphics are simple rectangles and text.

Build step or plain HTML:

- Can run from a plain HTML file using a script tag and CDN or local copy.
- The common p5 project shape uses separate `index.html`, `style.css`, and `sketch.js`, but it can be adapted.
- A build step is not required.

Priority-dependent areas:

- If beginner friendliness and quick visual iteration are high priorities, p5's sketch model matters.
- If staying close to standard browser APIs is a priority, p5 adds a layer of abstraction.
- If file size or dependency count is important, p5's library payload may be hard to justify for classic Pong.

## 2. Deployment Options

### A. Single Self-Contained HTML File

Requirements:

- One `.html` file containing markup, styles, and JavaScript.
- No external assets or dependencies unless they are embedded directly or loaded from a CDN.
- Browser access only; no server needed for classic scripts and inline code.

Tradeoffs:

- Simplest artifact to move, archive, email, or open locally.
- Lowest operational complexity.
- Harder to maintain as code grows because HTML, CSS, and JavaScript share one file.
- If a third-party library is embedded into the file, file size can become large and noisy.
- If a third-party library is loaded by CDN, the file is no longer fully offline/self-contained.

Development workflow:

- Edit one file and refresh the browser.
- Works well for minimal prototypes and small finished artifacts.
- Manual organization discipline becomes important because there is no file separation.

Priority-dependent areas:

- Strongest fit if portability and no setup matter most.
- Less attractive if maintainability, separation of concerns, or future expansion matter more.

### B. Multiple Files Opened Locally

Requirements:

- At minimum, an HTML file plus separate CSS and/or JavaScript files.
- Relative paths must be correct.
- Classic non-module scripts are more likely to work directly from `file://`.
- JavaScript modules, fetched assets, some media loading, and other cross-file operations can trigger local browser security/CORS issues.

Tradeoffs:

- Better organization than a single file.
- Still has no hosting requirement.
- Local `file://` behavior can differ from real hosted behavior.
- Some browser features expect HTTP(S), which may require a local static server during development.

Development workflow:

- Edit separate files and refresh browser.
- If using modules or assets, use a small local server to mirror real deployment behavior.
- Easier to transition to GitHub Pages, Netlify, or Vercel than a single embedded file.

Priority-dependent areas:

- Good fit if source readability matters but public deployment is not required yet.
- The answer depends on whether the chosen stack uses modules, asset loading, or CDN files.

### C. Hosted on GitHub Pages

Requirements:

- A GitHub repository.
- Static HTML, CSS, and JavaScript files.
- GitHub Pages configured for the repository or branch/folder.
- Optional custom domain.
- No backend server code.

Tradeoffs:

- Public web URL suitable for sharing and testing.
- Integrates naturally with Git workflow.
- GitHub Pages can publish static files directly from a repository and can optionally run a build process.
- Project sites are commonly served under `https://<owner>.github.io/<repositoryname>`, so relative asset paths should be handled carefully.
- Public repository visibility and Pages limits should be considered depending on account and repo settings.

Development workflow:

- Work locally, commit changes, push to GitHub, then wait for Pages deployment.
- Encourages versioned changes and reviewable history.
- For a no-build static Pong game, deployment can be straightforward once Pages is configured.

Priority-dependent areas:

- Stronger fit if the project wants a public URL tied to the repository.
- Less useful if the game should remain private, offline-only, or independent of GitHub.

### D. Hosted on a Simple Static File Host

Examples considered:

- Netlify.
- Vercel.

Requirements:

- Static site files: HTML, CSS, JavaScript, and assets.
- Account/project setup on the host.
- Deployment path can be Git integration, CLI deployment, dashboard upload, or drag-and-drop depending on provider.
- Build command can be blank for static HTML/CSS/client-side JavaScript projects.

Tradeoffs:

- Public preview and production URLs.
- More deployment features than local files or basic Pages: preview deploys, custom domains, dashboards, rollbacks, environment settings, and logs.
- More service/platform surface area than a tiny Pong game may need.
- Git-connected workflows add convenience but also more account/project setup.

Development workflow:

- With Git integration: edit locally, commit, push, and the host deploys.
- With manual upload or CLI: edit locally, then explicitly deploy the folder.
- Vercel documentation says static HTML/CSS/client-side JavaScript sites can skip a build step by using the "Other" framework preset and leaving the build command blank.
- Netlify supports Git-based deploys, CLI deploys, and drag-and-drop folders containing `.html` files.

Priority-dependent areas:

- Stronger fit if preview URLs, easy sharing, custom domains, or deploy history matter.
- Less attractive if the project wants the fewest accounts, services, and deployment concepts.
- Netlify vs Vercel depends on preferred workflow, dashboard, CLI, preview behavior, and any future framework plans.

## Cross-Cutting Research Notes

- For a classic Pong game, the core implementation is small enough that all three technology options are technically viable.
- The main tradeoff is not whether Pong is possible; it is dependency weight, learning goal, future expansion, and desired workflow.
- Plain local files are useful for early exploration, but hosted HTTP(S) better matches real browser behavior.
- CDN dependencies should be pinned to explicit versions for repeatability.
- If the final game includes separate image/audio files, module scripts, or fetch-based loading, local `file://` testing becomes less representative and may require a local server.
- No final technology or deployment choice is recommended in this note.
