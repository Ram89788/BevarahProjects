# Software Requirements Specification (SRS)
## Project 08: Lecture-to-Notes AI Converter + Tagging System

### 1. Project Description
An AI-powered educational tool that transforms long, unorganized audio recordings or video files of university lectures into structured, highly readable study notes. The system automatically transcribes the audio, generates summaries, highlights key terms, and applies a smart tagging system to help students organize their materials by topic and course.

### 2. Core Scope & Tech Stack
- **Frontend:** ReactJS (Vite), TailwindCSS, MaterialUI (Audio player, rich text editor).
- **Backend:** Java Spring Boot (File handling, Async processing, External AI API integration).
- **Scope:** Large file uploads, asynchronous job tracking, NLP summarization, and document organization.

### 3. Functionalities (Minimum 25)

#### Frontend (React + MaterialUI)
1. **Drag-and-Drop Uploader:** A UI component allowing students to upload large `.mp3` or `.mp4` lecture files with a clear progress bar.
2. **Interactive Audio/Video Player:** A custom player embedded next to the generated notes, allowing users to listen while reading.
3. **Timestamped Notes Viewer:** The generated notes feature clickable timestamps that instantly jump the audio player to that exact moment in the lecture.
4. **Rich Text Editing:** Users can manually edit the AI-generated notes, highlight text, and add their own bold/italic formatting.
5. **Smart Tagging UI:** MaterialUI Autocomplete chips allowing users to assign course codes (e.g., BIO101) and topics (e.g., Mitosis) to the document.
6. **Global Search Dashboard:** A central hub to search through all generated notes using keywords, filtering by specific tags.
7. **Flashcard Generator Toggle:** A button that takes key terms from the notes and flips them into a flashcard UI for studying.
8. **Dark Mode:** System-wide dark theme to reduce eye strain.

#### Backend (Spring Boot Core Features)
9. **Multipart File Upload API:** Spring MVC configuration to handle large file uploads securely, storing them temporarily on the server or pushing to AWS S3.
10. **Asynchronous Processing:** Use Spring's `@Async` and a thread pool to handle the transcription process in the background without blocking the HTTP request.
11. **Job Status Polling:** An endpoint the frontend can poll to get the current status of the conversion (e.g., "Uploading", "Transcribing", "Summarizing", "Done").
12. **Speech-to-Text Integration:** Backend service that sends the audio file to an external API (like OpenAI Whisper or Google Cloud Speech) and parses the returned transcript.
13. **NLP Summarization Service:** Integration with an LLM API to convert the raw, messy transcript into structured bullet points with headings.
14. **Keyword Extraction Logic:** An algorithm that identifies proper nouns and highly repeated technical terms to automatically suggest tags.

#### Note Organization & Export
15. **Folder Hierarchy:** Standard CRUD APIs to organize notes into Folders (Semesters) and Subfolders (Courses).
16. **Export to PDF/Markdown:** Convert the final, edited notes into a styled PDF or raw Markdown file for download.
17. **Shareable Links:** Generate a public URL to share the lecture notes with classmates.
18. **Merge Notes:** Ability to merge notes from "Lecture 1" and "Lecture 2" into a single master study guide.

#### Advanced AI Features
19. **"Generate Quiz" Feature:** Send the final notes back to the AI to generate a 5-question multiple-choice quiz testing the user's comprehension.
20. **Speaker Diarization (Optional):** Visually separate the text if the AI detects the professor speaking versus a student asking a question.
21. **Action Item Extraction:** Highlight any dates mentioned (e.g., "The midterm is on the 15th") and flag them as "Important Tasks".

#### Security & Infrastructure
22. **File Cleanup Cron Job:** A scheduled task that automatically deletes the massive raw audio files from the server after 7 days to save storage space.
23. **User Authentication:** Spring Security JWT to ensure students only see their own uploaded lectures.
24. **API Rate Limiting & Quotas:** Limit users to a specific number of audio minutes per month to control external AI API costs.
25. **Admin Cost Dashboard:** An interface for admins to monitor total API costs, user upload volume, and system errors.
