# Project Context

## Purpose
HIME (High Impact Minimum Effort) is a task prioritization and organization tool that helps users maximize productivity by focusing on tasks with the highest impact-to-effort ratio. The core methodology multiplies Impact (1-10) by Ease (1-10) to generate a HIME Score, enabling users to quickly identify which tasks deliver the most value for the least effort.

**Key Goals:**
- Simplify task prioritization using quantifiable metrics
- Provide instant visual feedback on task value
- Enable quick sorting and reorganization of tasks
- Track completed tasks with historical context
- Maintain a clean, intuitive user interface

## Tech Stack
- **Frontend**: Vanilla JavaScript (ES6+)
- **Styling**: Pure CSS3 with modern features (Grid, Flexbox, CSS Variables, Gradients)
- **Architecture**: Single-page application (SPA) - standalone HTML file
- **Storage**: Client-side only (localStorage for persistence - to be implemented)
- **Build System**: None - runs directly in browser
- **Target Browsers**: Modern evergreen browsers (Chrome, Firefox, Safari, Edge)

## Project Conventions

### Code Style
- **JavaScript**:
  - camelCase for variables and functions
  - PascalCase for class names (if/when added)
  - const/let only (no var)
  - Arrow functions preferred for callbacks
  - Single quotes for strings
  - 4-space indentation

- **CSS**:
  - kebab-case for class names
  - BEM methodology for complex components (if needed)
  - Mobile-first responsive design approach
  - Use CSS custom properties for theming
  - Group related properties (layout, typography, colors)

- **HTML**:
  - Semantic HTML5 elements
  - Meaningful IDs and classes
  - Accessibility: ARIA labels where needed

### Architecture Patterns
- **State Management**: In-memory JavaScript arrays (`tasks`, `doneTasks`)
- **Rendering**: Full re-render approach (simple DOM replacement)
- **Event Handling**: Inline onclick handlers for simplicity
- **Data Model**: Plain JavaScript objects with id, text, impact, ease properties
- **Modularity**: Single file for simplicity; future: split into modules if complexity grows

**Key Architectural Decisions:**
1. Standalone HTML file for maximum portability
2. No external dependencies/frameworks (zero npm packages)
3. Progressive enhancement approach
4. Animation-first UX for better user feedback

### Testing Strategy
Currently: Manual testing in browser

**Future Testing Approach:**
- Unit tests for core logic (task sorting, HIME score calculation)
- Integration tests for user workflows (add task → modify sliders → sort → complete)
- Browser compatibility testing
- Accessibility testing (keyboard navigation, screen readers)
- Performance testing for large task lists (100+ tasks)

### Git Workflow
- **Main Branch**: `main` (production-ready code)
- **Commit Messages**: Conventional commits format
  - `feat:` for new features
  - `fix:` for bug fixes
  - `docs:` for documentation
  - `style:` for formatting changes
  - `refactor:` for code restructuring
  - `test:` for adding tests
- **Branch Strategy**: Feature branches for significant changes
- **PR Requirements**: TBD (self-review for now)

## Domain Context

### HIME Methodology
The core concept is **Impact × Ease = HIME Score**:

- **Impact (1-10)**: How much value/benefit this task delivers
  - 10 = Critical business value, major user benefit
  - 5 = Moderate value, noticeable improvement
  - 1 = Minimal value, nice-to-have

- **Ease (1-10)**: How simple/quick the task is to complete
  - 10 = Takes minutes, no blockers, trivial
  - 5 = Moderate complexity, few dependencies
  - 1 = Very complex, many unknowns, time-consuming

- **HIME Score**: The product (1-100)
  - 100 = Maximum priority (high impact, easy to do)
  - 50 = Medium priority
  - 1 = Lowest priority (low impact, hard to do)

### User Workflow
1. Add task with descriptive text
2. Adjust Impact and Ease sliders based on assessment
3. Click "Sort by HIME Score" to reorder by priority
4. Work on highest-scoring tasks first
5. Click checkbox to mark complete (moves to "Completed Tasks" section)
6. Optionally undo completion or delete tasks

## Important Constraints

### Technical Constraints
- **No Server**: Pure client-side application
- **No Build Process**: Must work by opening HTML file directly
- **No External Dependencies**: Zero npm packages, CDNs, or frameworks
- **Browser Support**: Modern browsers only (ES6+ required)
- **File Size**: Keep under 50KB for fast loading
- **Performance**: Must handle 100+ tasks without lag
- **Persistence**: Tasks and status must persist between page close/open

### Design Constraints
- **Mobile-First**: Must work on phones, tablets, and desktop
- **Accessibility**: WCAG 2.1 AA compliance (goal)
- **No Authentication**: Stateless, single-user focused
- **Data Privacy**: All data stays local (no analytics, tracking, or external calls)

### Business Constraints
- **Open Source**: Free to use, modify, distribute
- **Self-Hosted**: Users must manage their own data
- **No Cloud Sync**: Each device maintains independent state

## External Dependencies

**Current**: None

**Potential Future Dependencies** (if needed):
- LocalStorage API (browser built-in) for data persistence
- IndexedDB for advanced data management
- Web Storage API for cross-tab synchronization
- Service Workers for offline support
- File System Access API for import/export

**No External Services**: No APIs, databases, or cloud services are used or planned.
