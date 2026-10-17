# Software Requirements Specification (SRS)
## Project 03: Collaborative Notes with Version Diff + Rollback

### 1. Project Description
A workspace productivity tool designed for engineering and academic teams. It allows users to write notes collaboratively in Markdown. The standout feature is a robust version control system (similar to Git/Wikipedia) that tracks every save, shows a visual diff of changes between versions, and allows users to roll back the document to any previous state.

### 2. Core Scope & Tech Stack
- **Frontend:** ReactJS (Vite), TailwindCSS, MaterialUI, Monaco Editor (or similar Markdown editor).
- **Backend:** Java Spring Boot (WebSockets for collaboration, JPA for version history).
- **Scope:** Markdown rendering, diff calculation, real-time syncing, and hierarchical folder organization.

### 3. Functionalities (Minimum 25)

#### Frontend (React + UI Components)
1. **Markdown Editor:** Integrate a robust editor (like React-Markdown or Monaco) supporting live preview split-screen.
2. **Workspace Navigation:** A sidebar tree-view (MaterialUI TreeView) to organize notes into nested folders and subfolders.
3. **Real-Time Collaboration Indicators:** Show avatars of other users currently viewing or editing the same note.
4. **Visual Diff Viewer:** A specialized UI view highlighting added text in green and removed text in red, comparing two document versions.
5. **Version History Panel:** A sidebar listing all saved versions with timestamps and the author's name.
6. **One-Click Rollback:** A button to restore the editor's content to a selected historical version.
7. **Tagging System:** Add colored chips (MaterialUI Chips) to notes for quick filtering and categorization.
8. **Dark Mode & Typography Controls:** Tailwind configuration to let users adjust font sizes and switch to dark mode for comfortable reading.

#### Backend (Spring Boot Core Features)
9. **WebSocket Configuration:** Implement Spring WebSockets (STOMP) to handle real-time broadcasting of cursor positions and text locks.
10. **Document CRUD APIs:** Standard REST endpoints to create, rename, move, and delete markdown notes.
11. **Versioning Engine:** Every time a note is saved (or auto-saved every 5 mins), the backend creates a new `NoteVersion` entity linked to the main note, preserving the raw text.
12. **Diff Calculation Service:** A Java service utilizing a diff-match-patch library to compute the exact differences between two text payloads on the server.
13. **Optimistic Locking:** JPA `@Version` annotation to prevent two users from overwriting each other's saves simultaneously if offline.
14. **Folder Hierarchy Logic:** Self-referential database table to handle infinitely nested folder structures.

#### Collaboration & Sharing
15. **Share via Link:** Generate a unique URL (UUID-based) to share a note publicly (read-only) or privately.
16. **Access Permissions:** Define roles per document (Owner, Editor, Viewer).
17. **Comment Threads:** Allow users to highlight a specific block of text and leave a threaded comment.
18. **Activity Feed:** A dashboard widget showing recent edits made by teammates across the workspace.

#### Search & Export
19. **Full-Text Search:** API endpoint utilizing Spring Data to search for keywords within the contents of all accessible notes.
20. **Export to PDF/HTML:** Backend service using a library like Flexmark to convert the Markdown payload into a styled PDF or HTML file for download.
21. **Import Markdown:** Allow users to drag and drop existing `.md` files into the web app to create new notes.

#### Security & System Features
22. **OAuth2 Login:** Support login via Google or GitHub alongside standard JWT email/password authentication.
23. **Trash/Recycle Bin:** Deleted notes are moved to a soft-delete "Trash" state for 30 days before permanent purging via a Spring `@Scheduled` task.
24. **Payload Compression:** GZIP compression enabled in Spring Boot application properties to handle large markdown files efficiently over the network.
25. **Rate Limiting:** Protect the version rollback and save endpoints from spam to conserve database storage.
