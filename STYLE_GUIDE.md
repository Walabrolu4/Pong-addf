# STYLE_GUIDE.md - PongTest

## 1. Documentation Voice

1. Write in clear, testable requirements language.
2. Prefer concrete values over adjectives.
3. State what is in scope and what is deferred.
4. Use "must" for requirements, "should" for guidance, and "may" for optional future possibilities.
5. Avoid implementation speculation in Design Mode.

## 2. Game UI Voice

1. Keep in-game text short and direct.
2. Use player-facing names from `DOMAIN.md`: Two Players, Vs AI, First to 10, 3 Lives.
3. Use action prompts that match controls exactly, such as "Press Space to serve" and "Press R to restart."
4. Do not explain ADDF process inside the game UI.

## 3. Banned Words in Project Files

- just
- simply
- obviously
- easy
- smart
- magic
- maybe
- probably

Use precise wording instead.

## 4. Canonical Terminology

| Term | Use |
|---|---|
| PongTest | Project name. |
| v1.0 | First playable release scope. |
| Two Players | Mode with two human players sharing one keyboard. |
| Vs AI | Mode with the human on the left paddle and AI on the right paddle. |
| First to 10 | Match mode where the first side to reach 10 points wins. |
| 3 Lives | Vs AI high-score mode where the human starts with 3 lives. |
| Not Started | Initial menu/selection state. |
| Ready to Serve | State waiting for `Space` before ball movement starts. |
| Playing | Active gameplay state. |
| Point Reset | State after point, life loss, or AI miss. |
| Game Over | End state before restart. |
| local high score | Browser-local score storage for 3 Lives mode. |
| local static files | `index.html`, `styles.css`, and `game.js` opened without a server. |

## 5. File Naming

- Use `UPPER_SNAKE_CASE.md` for root project brain files.
- Use lowercase kebab case for documentation and research files.
- Use lowercase snake case for sprint files.
- Runtime files for v1.0 must be named `index.html`, `styles.css`, and `game.js`.
- Do not use spaces in file or folder names.

## 6. Markdown Structure

1. Start each project brain file with a single H1.
2. Use short headings and tables when they improve scanability.
3. Keep requirements and decisions separate.
4. Link durable facts to `docs/requirements.md` or `DECISIONS.md` when possible.
5. Keep unresolved questions in `QUESTIONS.md`, not hidden inside implementation notes.

## 7. Code Style Guidance for Future Develop Mode

No code is written in this Design Mode file. When Develop Mode is authorized later:

- Prefer readable vanilla JavaScript over clever abstractions.
- Keep game state names aligned with `DOMAIN.md`.
- Keep Canvas rendering and update logic understandable.
- Use constants for shared gameplay values from requirements.
- Avoid external dependencies unless a new accepted decision approves them.

## 8. Visual Style Guidance

v1.0 visual requirements are intentionally minimal:

- Black playfield background.
- White paddles and ball.
- Muted grey center divider.
- High-contrast text.
- Centered 800 by 500 game canvas.

Exact color values are still an open question in `QUESTIONS.md`.

## 9. No Emoji Rule

Do not use emoji in project files, commit messages, sprint packs, or game UI text.
