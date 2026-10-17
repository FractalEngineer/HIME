# HIME Task Organizer

**High Impact, Minimum Effort** — a browser-based task prioritization tool.

This file is the single source of project documentation and agent guidance.

## Purpose

HIME helps users decide what to work on first by scoring tasks on two factors:

- **Impact** — how much value completing the task delivers (1–10)
- **Ease** — how easy the task is to accomplish (1–10)

The **HIME Score** (Impact × Ease) surfaces the highest-value, lowest-friction
tasks so users can focus on what matters most.

Key goals:

- Simplify task prioritization using quantifiable metrics
- Provide instant visual feedback on task value
- Enable quick sorting and reorganization of tasks
- Track completed tasks with historical context
- Maintain a clean, intuitive user interface

## HIME Methodology

The core concept is **Impact × Ease = HIME Score**:

- **Impact (1–10)**: value/benefit delivered. 10 = critical value, 5 = moderate,
  1 = nice-to-have.
- **Ease (1–10)**: simplicity/speed to complete. 10 = minutes, no blockers;
  5 = moderate; 1 = complex, many unknowns.
- **HIME Score (1–100)**: the product. 100 = highest priority (high impact, easy),
  50 = medium, 1 = lowest (low impact, hard).

### User Workflow

1. Add a task with descriptive text
2. Adjust Impact and Ease sliders based on assessment
3. Click "Sort by HIME Score" to reorder by priority
4. Work on highest-scoring tasks first
5. Mark a task complete (moves it to the "Completed Tasks" section)
6. Optionally restore or delete tasks

## Tech Stack

- **Frontend**: Vanilla JavaScript (ES6+)
- **Styling**: Pure CSS3 (Flexbox, gradients, custom range inputs, keyframe animations)
- **Architecture**: Single-page application in one standalone HTML file
- **Storage**: `localStorage` (keys: `hime_tasks`, `hime_doneTasks`, `hime_taskIdCounter`)
- **Build System**: None — runs directly in the browser
- **Dependencies**: None (zero npm packages, CDNs, or frameworks)
- **Target Browsers**: Modern evergreen browsers (Chrome, Firefox, Safari, Edge)

## Project Structure

```
HIME/
├── index.html      # The entire application (HTML + CSS + JS)
├── README.md       # User-facing overview
├── LICENSE         # CC BY-NC-SA 4.0
└── AGENTS.md       # This file
```

Everything (markup, styles, and logic) lives in `index.html`.

## Project Conventions

### Code Style

- **JavaScript**: camelCase for variables/functions; `const`/`let` only (no `var`);
  arrow functions for callbacks; single quotes; 4-space indentation.
- **CSS**: kebab-case class names; mobile-first responsive design; group related
  properties (layout, typography, colors).
- **HTML**: semantic elements; meaningful IDs and classes; ARIA labels where needed.

### Architecture Patterns

- **State Management**: In-memory JavaScript arrays (`tasks`, `doneTasks`) plus a
  `taskIdCounter`. Persisted to `localStorage` on every mutation via
  `saveToLocalStorage()` and restored on load via `loadFromLocalStorage()`.
- **Rendering**: Full re-render approach — `renderTasks()` / `renderDoneTasks()`
  rebuild the relevant container's innerHTML.
- **Event Handling**: Inline `onclick` / `oninput` handlers for simplicity.
- **Data Model**: Plain objects `{ id, text, impact, ease, himeScore }`.
- **Animations**: CSS keyframes for slide-in, fade-out, pulse, and confetti.

### Key Architectural Decisions

1. Single standalone HTML file for maximum portability.
2. No external dependencies or frameworks.
3. Animation-first UX for clear user feedback.
4. Client-side only — all data stays local, no analytics or external calls.

## Feature / Behavior Reference

### Task Creation

- Add via "Add Task" button or the Enter key.
- New tasks default to `impact = 5`, `ease = 5` (`himeScore = 25`).
- Empty/whitespace-only input is ignored (no task created).
- Input field is cleared after a task is created.

### Task Properties & Scoring

- Impact and Ease are adjustable 1–10 via sliders; the current numeric value
  displays next to each slider.
- HIME Score recalculates immediately on any slider change.
- Tasks are editable inline (contenteditable title); empty edits are ignored.

### Sorting

- "Sort by HIME Score" reorders tasks by descending HIME Score.
- The button reflects state: `disabled` (no tasks), `sorted` ("✓ Sorted by HIME"),
  or `needs-sort` (pulsing) when the current order is not by score.
- Sorted state is computed on demand by `checkIfSorted()`; sort button state is
  refreshed via `updateSortButton()` after mutations.

### Task Completion

- Completing a task plays a fade-out animation, then moves it to `doneTasks`.
- A confetti burst spawns at the task's location on completion.
- Completed tasks render with strikethrough text, plus a restore (↶) and delete (✕)
  button. The done-count badge updates on every change.

### Completed Tasks Section

- Collapsible via the "Completed Tasks" header (`toggleDoneSection()`).
- A **Clear** button sits in the header next to the count; it removes all completed
  tasks at once. It is disabled when there are no completed tasks and calls
  `event.stopPropagation()` so it does not toggle the section.

### Task Deletion

- Active and completed tasks can both be deleted; active deletions also refresh the
  sort button state.

### Empty State

- With no active tasks, a placeholder shows "No tasks yet. Add one to get started!".

### Layout & Visual Design

- Desktop (>768px): task controls in a single row.
- Mobile (≤768px): controls stack vertically; input and controls sections reflow.
- Purple-to-violet gradient header and accents; custom slider thumbs; hover effects
  and transitions on interactive elements.

### Accessibility

- Enter submits a task from the input field.
- Logical tab order: input → add button → sort button → tasks.

## Development Principles

- Favor straightforward, minimal implementations first; add complexity only when
  it is requested or clearly required.
- Keep changes tightly scoped to the requested outcome.
- Identify vague or ambiguous details and ask the necessary follow-up questions
  before editing files.

## Constraints

### Technical

- Pure client-side, no server and no build process.
- No external dependencies (npm, CDNs, frameworks).
- Must handle 100+ tasks without lag; keep the file lightweight.
- Tasks and completion state persist across page close/open via `localStorage`.

### Design

- Mobile-first; responsive across phone, tablet, and desktop.
- Accessibility goal: WCAG 2.1 AA.
- No authentication; single-user, stateless, data stays local.

## Git Workflow

- **Main branch**: `main` (production-ready code).
- **Commit messages**: Conventional Commits — `feat:`, `fix:`, `docs:`, `style:`,
  `refactor:`, `test:`.
- **Branches**: Feature branches for significant changes.

## Testing

Currently manual testing in the browser. If automation is added later, target:

- Unit tests for core logic (HIME scoring, sorting, sort-state detection).
- Integration tests for workflows (add → adjust sliders → sort → complete → restore).
- Cross-browser and accessibility (keyboard, screen reader) checks.
- Performance with large task lists (100+ tasks).
