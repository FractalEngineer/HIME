## ADDED Requirements

### Requirement: Task Creation
The system SHALL allow users to create new tasks with descriptive text.

#### Scenario: Add task with valid input
- **WHEN** user enters task text and clicks "Add Task" button
- **THEN** task is added to the active tasks list with default Impact=5 and Ease=5

#### Scenario: Add task with Enter key
- **WHEN** user enters task text and presses Enter key
- **THEN** task is added to the active tasks list with default values

#### Scenario: Prevent empty task creation
- **WHEN** user attempts to add a task with empty or whitespace-only text
- **THEN** system displays alert message and does not create task

#### Scenario: Clear input after task creation
- **WHEN** task is successfully created
- **THEN** input field is cleared and ready for next task

### Requirement: Task Properties Management
The system SHALL allow users to adjust Impact and Ease values for each task using slider controls.

#### Scenario: Adjust Impact slider
- **WHEN** user moves the Impact slider for a task
- **THEN** Impact value updates (1-10 range) and HIME Score recalculates immediately

#### Scenario: Adjust Ease slider
- **WHEN** user moves the Ease slider for a task
- **THEN** Ease value updates (1-10 range) and HIME Score recalculates immediately

#### Scenario: Display current slider values
- **WHEN** sliders are adjusted
- **THEN** current numeric values are displayed below each slider in real-time

### Requirement: HIME Score Calculation
The system SHALL calculate and display the HIME Score as the product of Impact and Ease.

#### Scenario: Calculate initial HIME Score
- **WHEN** new task is created with default values (Impact=5, Ease=5)
- **THEN** HIME Score displays as 25

#### Scenario: Recalculate on slider change
- **WHEN** user adjusts either Impact or Ease slider
- **THEN** HIME Score immediately recalculates and updates display

#### Scenario: Display score range
- **WHEN** tasks have various Impact and Ease combinations
- **THEN** HIME Scores range from 1 (1×1) to 100 (10×10)

### Requirement: Task Sorting
The system SHALL provide sorting functionality to reorder tasks by HIME Score in descending order.

#### Scenario: Sort unsorted tasks
- **WHEN** user clicks "Sort by HIME Score" button with unsorted tasks
- **THEN** tasks reorder with highest HIME Score first, button shows "Already Sorted"

#### Scenario: Detect when sorting needed
- **WHEN** user modifies task sliders after sorting
- **THEN** sort button changes appearance to indicate "needs-sort" state with pulse animation

#### Scenario: Handle single task
- **WHEN** only one or zero tasks exist
- **THEN** sort button shows "Already Sorted" state and is non-interactive

#### Scenario: Maintain sort detection
- **WHEN** tasks are manually created in sorted order
- **THEN** system detects sorted state without requiring sort action

### Requirement: Task Completion
The system SHALL allow users to mark tasks as completed and move them to a separate completed section.

#### Scenario: Complete a task
- **WHEN** user clicks the checkbox circle next to a task
- **THEN** task animates out, moves to "Completed Tasks" section, and displays with strikethrough

#### Scenario: Display completion animation
- **WHEN** task is marked complete
- **THEN** fade-out and slide-left animation plays before task removal

#### Scenario: Track completion timestamp
- **WHEN** task is completed
- **THEN** completedAt timestamp is added to task object

#### Scenario: Update done counter
- **WHEN** task is completed or uncompleted
- **THEN** completed tasks counter badge updates to show current count

### Requirement: Completed Tasks Management
The system SHALL maintain a separate collapsible section for completed tasks with undo and delete capabilities.

#### Scenario: Expand completed section
- **WHEN** user clicks "Completed Tasks" header
- **THEN** section expands to show all completed tasks with slide-in animation

#### Scenario: Collapse completed section
- **WHEN** user clicks expanded "Completed Tasks" header
- **THEN** section collapses and hides completed tasks list

#### Scenario: Display completed task details
- **WHEN** completed tasks are displayed
- **THEN** each shows task text (strikethrough), HIME Score, undo button, and delete button

#### Scenario: Undo task completion
- **WHEN** user clicks "Undo" button on completed task
- **THEN** task moves back to active tasks list with original Impact and Ease values

#### Scenario: Show empty completed state
- **WHEN** no tasks have been completed
- **THEN** completed section displays "No completed tasks yet" message

### Requirement: Task Deletion
The system SHALL allow users to delete tasks from both active and completed lists.

#### Scenario: Delete active task
- **WHEN** user clicks "Delete" button on active task
- **THEN** task is immediately removed from active tasks list

#### Scenario: Delete completed task
- **WHEN** user clicks delete button (×) on completed task
- **THEN** task is permanently removed from completed tasks list

#### Scenario: Update sort state after deletion
- **WHEN** task is deleted from active list
- **THEN** system checks if remaining tasks are sorted and updates button state

### Requirement: User Interface Layout
The system SHALL provide a responsive, mobile-first interface with clear visual hierarchy.

#### Scenario: Display on desktop
- **WHEN** viewed on desktop browser (>768px width)
- **THEN** task items display in grid layout with all controls in single row

#### Scenario: Display on mobile
- **WHEN** viewed on mobile device (≤768px width)
- **THEN** task items stack vertically with controls reorganized for touch interaction

#### Scenario: Show empty state
- **WHEN** no active tasks exist
- **THEN** display placeholder with emoji and message "No tasks yet. Add your first task above to get started!"

#### Scenario: Visual feedback on hover
- **WHEN** user hovers over interactive elements (buttons, sliders, task items)
- **THEN** elements display hover effects (scale, shadow, color changes)

### Requirement: Visual Design System
The system SHALL implement a cohesive design with gradient themes, smooth animations, and modern styling.

#### Scenario: Display gradient header
- **WHEN** page loads
- **THEN** header displays purple-to-violet gradient background with white text

#### Scenario: Display HIME Score with gradient text
- **WHEN** HIME Score is shown
- **THEN** number displays with gradient text effect (purple to violet)

#### Scenario: Animate sort button
- **WHEN** sorting is needed
- **THEN** sort button pulses with blue color and animated shadow

#### Scenario: Style slider controls
- **WHEN** sliders are displayed
- **THEN** custom purple thumb with shadow effect and smooth transitions on interaction

### Requirement: State Management
The system SHALL maintain application state using in-memory JavaScript data structures.

#### Scenario: Initialize application state
- **WHEN** page loads
- **THEN** empty tasks array, empty doneTasks array, taskIdCounter=0, isSorted=true

#### Scenario: Generate unique task IDs
- **WHEN** new task is created
- **THEN** task receives unique incremental ID from taskIdCounter

#### Scenario: Update sorted state flag
- **WHEN** tasks are modified or sorted
- **THEN** isSorted flag updates to reflect current sort state

#### Scenario: Maintain done section toggle state
- **WHEN** user expands/collapses done section
- **THEN** isDoneExpanded flag persists state for session

### Requirement: Keyboard Accessibility
The system SHALL support keyboard navigation and common keyboard shortcuts.

#### Scenario: Submit with Enter key
- **WHEN** task input field is focused and user presses Enter
- **THEN** task is added same as clicking "Add Task" button

#### Scenario: Focus management
- **WHEN** user tabs through interface
- **THEN** focus order follows logical flow: input → add button → sort button → tasks
