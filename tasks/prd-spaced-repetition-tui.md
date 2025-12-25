# Product Requirements Document: Spaced Repetition TUI Application

## Introduction/Overview

A Terminal User Interface (TUI) application for spaced repetition learning using the state-of-the-art FSRS (Free Spaced Repetition Scheduler) algorithm. The app enables users to efficiently study any type of knowledge—languages, technical topics, general knowledge—through an intuitive command-line interface. It combines powerful learning science with an easy card creation workflow and rich content support.

## Goals

1. Enable users to create flashcards (Q/A, cloze) intuitively within the TUI without switching to external tools
2. Implement FSRS algorithm for optimal review scheduling based on user performance
3. Support multimedia-rich cards (images, code snippets) alongside text
4. Provide a seamless, pleasant study experience with all-in-one functionality
5. Persist all data locally in SQLite for portability and offline access

## User Stories

- As a student, I want to quickly create Q/A cards directly in the app so I can immediately start reviewing without switching contexts
- As a programmer, I want to include code snippets with syntax highlighting in my flashcards so I can learn API documentation and language features
- As a language learner, I want to hide certain words in my prompts using cloze deletion so I can test myself on vocabulary recall
- As a visual learner, I want to attach images to both questions and answers so I can learn with visual aids
- As a regular user, I want the app to automatically schedule my reviews using FSRS so I study at the optimal time to retain information
- As a user, I want to switch between reviewing and creating cards within the same app without friction
- As a user, I want my data saved locally in a structured format so I can export/backup easily

## Functional Requirements

### Card Creation
1. The app must provide a simple, intuitive mode to create new flashcards without requiring a text editor
2. Users must be able to create three card types:
   - **Q/A Cards:** Question (prompt) and Answer format
   - **Cloze Cards:** Text with hidden portions marked as `[hidden text]`
   - Both types must support text, code snippets, and images
3. The card creation interface must support inline editing with visual feedback
4. Users must be able to attach code snippets to both prompts and answers with language selection (Python, JavaScript, etc.)
5. Users must be able to attach images to prompts and answers via file path selection
6. The app must validate card data before saving (ensure prompts and answers are not empty)
7. Users must be able to cancel and discard in-progress card creation

### Card Storage & Management
8. All cards must be stored in a SQLite database with the following schema:
   - Card ID (UUID)
   - Card type (Q/A or Cloze)
   - Prompt (text content)
   - Answer (text content)
   - Metadata: created_at, updated_at, tags, deck name
   - Nested relationships for code snippets and images
9. The app must support organizing cards into "decks" (categories/subjects)
10. Users must be able to view all cards in a deck with filtering and search capabilities
11. Users must be able to edit, delete, or archive cards from the review interface
12. The app must track revision history for each card

### Review & Spaced Repetition
13. The app must implement the FSRS (Free Spaced Repetition Scheduler) algorithm to schedule card reviews
14. During review, users must see either the prompt (Q/A) or the cloze text, and reveal the answer on demand
15. Code snippets and images must be rendered with proper formatting (syntax highlighting for code, embedded images)
16. Users must rate their recall performance on a scale (e.g., 1-5: Again, Hard, Good, Easy) after each card
17. The app must update card scheduling based on user ratings according to FSRS parameters
18. The app must display scheduling information: next review date, difficulty level, repetitions count
19. Users must see a summary dashboard showing:
    - Total cards in deck
    - Cards due for review today
    - Study progress/statistics

### TUI Features & User Experience
20. The app must support keyboard-driven navigation (no mouse required, though mouse may work)
21. The app must display a clean, organized layout with:
    - Main menu for navigation (Create, Review, Manage Decks, Settings, Statistics)
    - Clear visual hierarchy and information density
    - Progress indicators during review
22. The app must provide keyboard shortcuts for common actions (review, skip, edit, delete)
23. The app must render properly on terminals of different sizes (responsive layout)
24. The app must support syntax highlighting for code snippets (at least Python, JavaScript, SQL, Bash)
25. The app must support color theming (at least a light and dark theme, customizable)
26. The app must provide helpful error messages and confirmations for destructive actions
27. The app must handle edge cases gracefully (empty decks, corrupted data, invalid file paths)

### Data Persistence & Portability
28. The SQLite database must be stored in a user-friendly location (e.g., `~/.flashcards/` or user-specified directory)
29. Users must be able to export decks to standard formats (CSV, JSON) for backup or migration
30. Users must be able to import cards from standard formats (CSV, JSON)
31. The app must include a settings file to store user preferences (theme, default deck, etc.)

## Non-Goals (Out of Scope)

- Cloud synchronization or online backup (data remains local)
- Collaborative/multiplayer features
- Spaced repetition for other formats (videos, audio)
- Mobile companion app
- Built-in content marketplace or shared decks (in MVP)
- Advanced statistical analysis or heatmaps
- Integration with external learning platforms (Anki import is not required in MVP)
- Handwriting or drawing input
- Text-to-speech pronunciation guides (optional future enhancement)

## Design Considerations

### TUI Framework
- Framework choice is flexible; prioritize ease of implementation and responsiveness
- Candidates: Python (Textual), Rust (Ratatui), Go (Bubble Tea)
- Must support:
  - Modal dialogs for card creation/editing
  - Dynamic resizing
  - Syntax highlighting for code blocks
  - Image rendering (ASCII art or inline images depending on terminal capability)

### UI/UX Layout Structure
- **Main Menu Screen:** Navigation to key sections
- **Deck Browser:** List of decks with statistics
- **Card Creation Modal:** Form-like interface for entering prompt, answer, attachments
- **Review Screen:** Large prompt display, hidden answer, reveal button, rating buttons
- **Card Management:** Table/list view of cards with edit/delete options
- **Statistics Dashboard:** Visual summary of progress
- **Settings:** Theme, deck location, review preferences

### Image & Code Handling
- **Code:** Store as text with language metadata; render with syntax highlighting
- **Images:** Store file paths relative to database location; render in terminal (use Unicode/ANSI art or image protocol if supported)
- Fallback for limited terminals: Display file path or placeholder

## Technical Considerations

### Database Schema (SQLite)
```
decks: id (PK), name, created_at, updated_at
cards: id (PK), deck_id (FK), type (Q/A or Cloze), prompt, answer, created_at, updated_at, tags
code_snippets: id (PK), card_id (FK), content, language, position (prompt/answer)
images: id (PK), card_id (FK), file_path, position (prompt/answer)
card_stats: id (PK), card_id (FK), difficulty, due_date, repetitions, interval, ease_factor
```

### FSRS Implementation
- Use an existing FSRS library if available (e.g., `fsrs-rs` for Rust, `fsrs-py` for Python) or implement from FSRS algorithm specifications
- Store FSRS parameters per card: difficulty, interval, due_date, repetitions, ease_factor

### Code Structure
- Modular architecture: Separate concerns for UI, database, FSRS logic, and file handling
- Clear separation between card creation flow and review flow
- Logging system for debugging (optional but helpful)

## Success Metrics

1. Users can create a new card in less than 30 seconds from app launch
2. The TUI is responsive and loads cards within 100ms for typical deck sizes (500+ cards)
3. FSRS scheduling is accurate and users report effective retention when following recommendations
4. All card types (Q/A, cloze) with attachments render correctly on standard terminals
5. No data loss during normal app operation; SQLite integrity maintained
6. Keyboard navigation works smoothly across all screens without requiring mouse
7. App handles edge cases (empty input, large images, special characters) without crashing

## Open Questions

1. Should the app support multiple decks simultaneous review sessions, or one at a time?
2. What is the preferred method for image attachment: file browser within TUI or copy file path?
3. Should tags be searchable/filterable, or just display-only metadata in MVP?
4. What terminal capabilities should we assume as minimum (e.g., 256 colors, true color, image protocol support)?
5. Should users be able to undo deleted cards or is permanent deletion acceptable?
