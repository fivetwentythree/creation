# Task Breakdown: Spaced Repetition TUI Application

## Phase 1: Project Setup & Architecture

### Task 1.1: Technology Stack Selection
- **Objective:** Finalize tech stack and project structure
- **Details:**
  - Choose TUI framework (Python Textual, Rust Ratatui, or Go Bubble Tea)
  - Choose database driver for SQLite
  - Select FSRS library or implementation approach
  - Set up project repository structure
- **Deliverable:** Project scaffolding with dependencies configured

### Task 1.2: Database Schema Design & Setup
- **Objective:** Create SQLite schema and initialization script
- **Details:**
  - Implement all tables: `decks`, `cards`, `code_snippets`, `images`, `card_stats`
  - Create migrations or schema initialization script
  - Define data types, constraints, relationships
  - Test schema with sample data
- **Deliverable:** Initialized SQLite database with all tables, migration files

### Task 1.3: Project Structure & Architecture Planning
- **Objective:** Define module organization and component boundaries
- **Details:**
  - Plan module structure (UI, Database, FSRS, File Handlers)
  - Define interfaces between modules
  - Plan error handling strategy
  - Create project architecture documentation
- **Deliverable:** Clear module structure, architectural diagrams

---

## Phase 2: Core Database Layer

### Task 2.1: Database Access Layer (DAL)
- **Objective:** Build abstraction layer for database operations
- **Details:**
  - Implement CRUD operations for decks
  - Implement CRUD operations for cards
  - Implement database connection pooling/management
  - Add error handling and logging
- **Deliverable:** Working DAL with tested deck and card operations

### Task 2.2: Card Statistics & FSRS Metadata Management
- **Objective:** Create DAL functions for managing card stats
- **Details:**
  - Implement save/update card stats (difficulty, interval, due_date, etc.)
  - Implement retrieve card stats for review
  - Add functions to query cards due for review
  - Implement batch updates for multiple cards
- **Deliverable:** Fully functional card stats management layer

### Task 2.3: Code Snippet & Image Storage Management
- **Objective:** Handle nested data structures for attachments
- **Details:**
  - Implement save/retrieve code snippets associated with cards
  - Implement save/retrieve image file paths associated with cards
  - Handle file path validation for images
  - Implement cascade delete when cards are deleted
- **Deliverable:** Working attachment management system

---

## Phase 3: FSRS Algorithm Integration

### Task 3.1: FSRS Algorithm Implementation/Integration
- **Objective:** Integrate FSRS scheduling logic
- **Details:**
  - If using external library: set up and wrap it
  - If implementing: translate FSRS algorithm to chosen language
  - Initialize card parameters (difficulty=0.5, interval=0, due_date=today, etc.)
  - Implement parameter update logic based on user ratings
- **Deliverable:** Working FSRS module with scheduling calculations

### Task 3.2: Card Scheduling & Due Date Management
- **Objective:** Track and retrieve cards for review
- **Details:**
  - Implement function to get all cards due for review (today or earlier)
  - Implement function to calculate next review date after rating
  - Track review history (what was rated, when, rating value)
  - Generate statistics (total reviewed today, average rating, etc.)
- **Deliverable:** Complete review scheduling system

---

## Phase 4: Core TUI Framework & Navigation

### Task 4.1: TUI Framework Setup & Base Components
- **Objective:** Initialize TUI framework and basic layout
- **Details:**
  - Set up main application window/container
  - Create base widget/component classes
  - Implement keyboard event handling system
  - Implement theme/color system (light & dark mode)
- **Deliverable:** Working TUI framework with basic navigation

### Task 4.2: Main Menu & Navigation System
- **Objective:** Build main navigation hub
- **Details:**
  - Create main menu screen with options: Create, Review, Manage Decks, Statistics, Settings
  - Implement screen routing/switching
  - Add keyboard shortcut system
  - Implement back/exit functionality
- **Deliverable:** Functional main menu with navigation to all sections

### Task 4.3: Deck Browser Screen
- **Objective:** Display available decks and deck-level operations
- **Details:**
  - Create table/list view of all decks
  - Display deck statistics (total cards, due count, last reviewed)
  - Implement deck selection
  - Add "Create New Deck" option
  - Implement deck deletion with confirmation
- **Deliverable:** Full deck management interface

---

## Phase 5: Card Creation Module

### Task 5.1: Card Creation Form/Modal Interface
- **Objective:** Build intuitive card creation UI
- **Details:**
  - Create modal dialog for new card entry
  - Add input fields: Prompt, Answer, Card Type selector
  - Implement focus management and tab navigation
  - Add visual feedback for input validation
  - Cancel and Submit buttons with confirmations
- **Deliverable:** Working card creation modal for Q/A and Cloze cards

### Task 5.2: Code Snippet Attachment in Card Creation
- **Objective:** Allow code insertion into cards
- **Details:**
  - Create sub-interface to add code snippets
  - Language selection dropdown (Python, JavaScript, SQL, Bash, etc.)
  - Code content input (multi-line editor)
  - Position selection (in prompt or answer)
  - Preview of formatted code
  - Delete code snippet option
- **Deliverable:** Code snippet attachment system in card creation

### Task 5.3: Image Attachment in Card Creation
- **Objective:** Allow image attachment to cards
- **Details:**
  - Create file browser/path input for images
  - Validate image file exists and is readable
  - Store relative file path in database
  - Position selection (in prompt or answer)
  - Preview thumbnail or filename
  - Delete image attachment option
- **Deliverable:** Image attachment system in card creation

### Task 5.4: Card Validation & Persistence
- **Objective:** Validate and save new cards
- **Details:**
  - Implement validation rules (non-empty prompt/answer, valid attachments)
  - Generate card ID and metadata (created_at, updated_at)
  - Initialize FSRS stats for new card (difficulty, interval, due_date)
  - Save to database via DAL
  - Show success message and return to menu
  - Handle errors and display user-friendly messages
- **Deliverable:** Complete card creation pipeline

---

## Phase 6: Review & Study Module

### Task 6.1: Review Screen Foundation
- **Objective:** Build core review interface
- **Details:**
  - Create review screen layout
  - Display deck name and review stats (X of Y cards due, today's progress)
  - Fetch cards due for review from database
  - Implement card navigation (next/previous)
  - Handle end-of-session scenarios
- **Deliverable:** Basic review screen structure

### Task 6.2: Prompt & Answer Display
- **Objective:** Render card content appropriately
- **Details:**
  - Display prompt (question or cloze text with hidden portions)
  - Implement answer reveal mechanism (initially hidden)
  - Render code snippets with syntax highlighting
  - Render images (ASCII art, Unicode, or file path fallback)
  - Handle long content with scrolling/pagination
- **Deliverable:** Rich content rendering for prompts and answers

### Task 6.3: Cloze Card Rendering
- **Objective:** Properly display cloze deletion cards
- **Details:**
  - Parse cloze format: `[hidden text]` in prompt
  - Display hidden portions as blanks or placeholders (e.g., "___")
  - Show answer with all blanks filled
  - Highlight hidden portions in answer for clarity
- **Deliverable:** Working cloze card display and reveal

### Task 6.4: User Rating & Performance Input
- **Objective:** Capture user self-assessment
- **Details:**
  - Display rating scale: 1 (Again), 2 (Hard), 3 (Good), 4 (Easy)
  - Keyboard shortcuts for each rating
  - Visual feedback when rating is selected
  - Submit rating and move to next card
  - Show rating confirmation
- **Deliverable:** Rating input system with visual feedback

### Task 6.5: FSRS Update & Scheduling
- **Objective:** Calculate next review date based on rating
- **Details:**
  - Call FSRS algorithm with current card stats and user rating
  - Calculate new interval, difficulty, due_date
  - Update card stats in database
  - Track review history (timestamp, rating, old/new interval)
  - Display updated scheduling info to user
- **Deliverable:** Dynamic schedule updates after each rating

### Task 6.6: Review Summary & Statistics
- **Objective:** Show session results
- **Details:**
  - Display cards reviewed today count
  - Show average rating
  - Display next card due time
  - Breakdown by rating (1/2/3/4 distributions)
  - Option to continue reviewing or return to menu
- **Deliverable:** Informative review session summary

---

## Phase 7: Card Management & Editing

### Task 7.1: Card Browser/List View
- **Objective:** Display all cards in a deck with filtering
- **Details:**
  - Create table view of cards (Deck → Prompt preview, Card type, Due date, Stats)
  - Sorting options (by due date, creation date, difficulty, etc.)
  - Search functionality (filter by prompt text)
  - Tag filtering (if tags are implemented)
  - Select card for action (edit, delete, view details)
- **Deliverable:** Full card management interface

### Task 7.2: Card Editing
- **Objective:** Allow modification of card content
- **Details:**
  - Reuse card creation form as edit form
  - Pre-populate with existing card data
  - Allow editing prompt, answer, attachments
  - Preserve FSRS stats during edit
  - Update updated_at timestamp
  - Show confirmation of changes
- **Deliverable:** Full card editing capability

### Task 7.3: Card Deletion with Confirmation
- **Objective:** Safe card removal
- **Details:**
  - Show confirmation dialog before deletion
  - Display card preview in confirmation
  - Cascade delete attachments and stats
  - Option to undo (archive instead of delete) - optional MVP
  - Update statistics after deletion
- **Deliverable:** Safe deletion mechanism

---

## Phase 8: Statistics & Dashboard

### Task 8.1: Statistics Dashboard Screen
- **Objective:** Visualize learning progress
- **Details:**
  - Create dashboard layout
  - Display total cards in deck
  - Show cards due today
  - Display total cards reviewed (all-time)
  - Show review streak (consecutive days reviewed)
  - Average card difficulty
  - Cards mastered (interval > X days)
- **Deliverable:** Comprehensive statistics view

### Task 8.2: Detailed Statistics & Analytics
- **Objective:** Provide deeper insights
- **Details:**
  - Review history graph (reviews per day over time)
  - Rating distribution (% of Again/Hard/Good/Easy)
  - Card difficulty heatmap (cards by difficulty level)
  - Time spent studying (estimated)
  - Retention rate (cards reviewed multiple times, retained)
- **Deliverable:** Advanced analytics view (optional, nice-to-have)

---

## Phase 9: Settings & Preferences

### Task 9.1: Settings Menu & Storage
- **Objective:** Manage application preferences
- **Details:**
  - Create settings screen with options:
    - Theme selection (light/dark)
    - Default deck
    - Review preferences (cards per session, etc.)
    - Database location
    - Keyboard shortcuts customization (optional)
  - Load/save settings to config file (JSON or TOML)
  - Apply theme changes immediately
- **Deliverable:** Full settings management system

---

## Phase 10: Data Export & Import

### Task 10.1: Deck Export (CSV/JSON)
- **Objective:** Allow backup and migration
- **Details:**
  - Implement export to CSV format (columns: Prompt, Answer, Type, Code, Image, Tags)
  - Implement export to JSON format (preserve full structure)
  - Include metadata (created_at, updated_at, deck_name)
  - Optionally include FSRS stats
  - File chooser for export location
  - Success notification
- **Deliverable:** Working export system

### Task 10.2: Deck Import (CSV/JSON)
- **Objective:** Allow data import and migration
- **Details:**
  - Implement CSV import parser
  - Implement JSON import parser
  - Validate imported data
  - Handle duplicates (skip, overwrite, or merge options)
  - Create new deck from import or merge into existing
  - Initialize FSRS stats for imported cards
  - Show import summary and any errors
- **Deliverable:** Complete import system

---

## Phase 11: Polish & Error Handling

### Task 11.1: Terminal Responsiveness & Resizing
- **Objective:** Handle various terminal sizes
- **Details:**
  - Test on different terminal widths/heights
  - Implement responsive layout (reflow on resize)
  - Handle minimum terminal size requirements
  - Graceful degradation for very small terminals
  - Update UI on resize events
- **Deliverable:** Responsive TUI across terminal sizes

### Task 11.2: Error Handling & Recovery
- **Objective:** Robust error management
- **Details:**
  - Add try-catch/error handling throughout
  - Implement user-friendly error messages
  - Log errors to file for debugging
  - Graceful handling of corrupted database
  - Recovery options (reset, repair, rollback)
  - Prevent crashes on edge cases
- **Deliverable:** Robust error handling system

### Task 11.3: Input Validation & Sanitization
- **Objective:** Prevent invalid data entry
- **Details:**
  - Validate all user inputs (text length, special characters, etc.)
  - Sanitize file paths to prevent injection
  - Handle Unicode and emoji in card text
  - Prevent SQL injection via DAL
  - Show clear validation error messages
- **Deliverable:** Input validation throughout app

### Task 11.4: Performance Optimization
- **Objective:** Ensure smooth operation
- **Details:**
  - Optimize database queries (indexing, lazy loading)
  - Cache frequently accessed data (deck stats, due cards)
  - Handle large decks (1000+ cards) efficiently
  - Test response times, optimize if needed
  - Lazy load images
- **Deliverable:** Performant application

---

## Phase 12: Testing & QA

### Task 12.1: Unit Tests
- **Objective:** Test individual components
- **Details:**
  - Write tests for FSRS calculations
  - Test DAL CRUD operations
  - Test card validation logic
  - Test import/export functions
  - Aim for 70%+ code coverage
- **Deliverable:** Comprehensive unit test suite

### Task 12.2: Integration Tests
- **Objective:** Test workflows end-to-end
- **Details:**
  - Test complete card creation workflow
  - Test complete review workflow
  - Test import/export workflows
  - Test deck management workflows
- **Deliverable:** Integration test suite

### Task 12.3: Manual QA & Edge Cases
- **Objective:** Test real-world usage scenarios
- **Details:**
  - Test with empty decks
  - Test with large decks (1000+ cards)
  - Test with special characters in prompts/answers
  - Test with corrupt images/files
  - Test keyboard navigation thoroughly
  - Test theme switching
  - Cross-platform testing (macOS, Linux, Windows if possible)
- **Deliverable:** QA checklist, bug reports, fixes

---

## Phase 13: Documentation & Release

### Task 13.1: User Documentation
- **Objective:** Create user guide
- **Details:**
  - Write README with installation instructions
  - Create keyboard shortcut reference
  - Write getting started guide
  - Create FAQ section
  - Include screenshot examples
- **Deliverable:** Complete user documentation

### Task 13.2: Developer Documentation
- **Objective:** Enable future maintenance
- **Details:**
  - Document module architecture
  - Write code comments for complex logic
  - Document database schema
  - Document FSRS implementation details
  - Create contribution guidelines
- **Deliverable:** Complete developer documentation

### Task 13.3: Release Preparation
- **Objective:** Package for release
- **Details:**
  - Create install script or binary
  - Test installation process
  - Create changelog
  - Tag release version
  - Create release notes
- **Deliverable:** Ready-to-release application

---

## Task Dependencies & Suggested Order

**Recommended Execution Path:**

1. Phase 1 (Setup & Architecture)
2. Phase 2 (Database Layer)
3. Phase 3 (FSRS Integration)
4. Phase 4 (TUI Framework)
5. Phase 5 (Card Creation) - Can run parallel with Phase 4
6. Phase 6 (Review Module) - Depends on Phases 4 & 3
7. Phase 7 (Card Management)
8. Phase 8 (Statistics)
9. Phase 9 (Settings)
10. Phase 10 (Export/Import)
11. Phase 11 (Polish)
12. Phase 12 (Testing) - Run throughout development
13. Phase 13 (Documentation & Release)

---

## Effort Estimation (Optional)

| Phase | Est. Effort | Priority |
|-------|-------------|----------|
| 1. Setup | 1-2 days | Critical |
| 2. Database | 2-3 days | Critical |
| 3. FSRS | 1-2 days | Critical |
| 4. TUI Framework | 3-4 days | Critical |
| 5. Card Creation | 3-4 days | Critical |
| 6. Review Module | 4-5 days | Critical |
| 7. Card Management | 2-3 days | High |
| 8. Statistics | 2-3 days | High |
| 9. Settings | 1-2 days | Medium |
| 10. Export/Import | 2-3 days | High |
| 11. Polish | 2-3 days | High |
| 12. Testing | 3-4 days | High |
| 13. Documentation | 1-2 days | Medium |
| **Total** | **~35-45 days** | - |

*Note: Times can vary significantly based on tech stack choice and experience level.*
