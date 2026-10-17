# Software Requirements Specification (SRS)
## Project 01: AI Study Planner with Adaptive Difficulty Tracking

### 1. Project Description
The AI Study Planner is an intelligent educational platform that generates dynamic study schedules based on a student's upcoming exams, available hours, and historical performance. The system uses an adaptive tracking algorithm to automatically allocate more study time to subjects the student finds difficult, ensuring an optimized learning path.

### 2. Core Scope & Tech Stack
- **Frontend:** ReactJS (Vite), TailwindCSS, MaterialUI (for interactive calendars and data grids).
- **Backend:** Java Spring Boot (REST APIs, scheduling logic, security).
- **Scope:** Calendar integration, difficulty assessment algorithm, task tracking, and visual analytics.

### 3. Functionalities (Minimum 25)

#### Frontend (React + MaterialUI)
1. **Interactive Dashboard:** Use MaterialUI Cards to display today's upcoming study sessions and a progress ring for daily goals.
2. **Dynamic Calendar:** Integrate a full-screen React-Big-Calendar showing all planned study blocks and exam dates.
3. **Subject Configuration Form:** Form to add subjects, syllabus topics, and initial perceived difficulty (1-5 slider).
4. **Drag-and-Drop Tasks:** React-beautiful-dnd implementation to let users manually rearrange generated study blocks.
5. **Study Timer:** A built-in Pomodoro timer component that syncs time tracked back to the server.
6. **Confidence Rating Modal:** A pop-up after every study session asking the user to rate their understanding (1-5 stars) using MaterialUI Rating components.
7. **Progress Visualizations:** Recharts/Chart.js integration to display "Knowledge Growth" over time per subject.
8. **Dark Mode Toggle:** Tailwind-driven global dark/light theme switching.

#### Backend (Spring Boot Core Features)
9. **JWT Authentication:** Spring Security implementation with JSON Web Tokens for stateless user sessions.
10. **User Registration & Profile API:** Endpoints to handle signup, login, and storing user study preferences (hours available per day).
11. **Adaptive Scheduling Algorithm:** A Spring service that calculates the required hours per topic, applying a multiplier for topics with a low confidence score.
12. **Automated Timetable Generation:** API endpoint that receives exam dates and outputs a JSON array of scheduled study blocks.
13. **CRUD Operations for Subjects/Exams:** Standard REST endpoints (`GET`, `POST`, `PUT`, `DELETE`) to manage the user's curriculum.
14. **Time Tracking API:** Endpoint to log exactly how many minutes were spent on a specific study block.

#### Intelligent & Adaptive Features
15. **Difficulty Recalculation:** A scheduled Cron job (using `@Scheduled`) that recalculates the difficulty weight of topics every night based on recent user feedback.
16. **Spaced Repetition Integration:** The scheduling algorithm automatically inserts "Review" blocks 3, 7, and 14 days after a topic is first studied.
17. **Burnout Detection:** Backend logic that flags if a user schedules more than 8 hours of intense study in a day, sending a warning via the UI.
18. **Syllabus Coverage Tracking:** Calculate the percentage of topics marked "Confident" versus total topics.

#### Notifications & Collaboration
19. **Email Reminders:** Spring Mail integration to send a daily morning summary of the day's study plan.
20. **Browser Push Notifications:** Web push integration to alert the user 10 minutes before a study block begins.
21. **Export to Google Calendar:** Generate an `.ics` file so users can import their generated plan to external calendars.
22. **Study Group Sharing:** Generate a read-only link so users can share their study timeline with friends.

#### Administration & Security
23. **Global Exception Handling:** `@ControllerAdvice` to handle API errors and return standardized JSON error messages to the React frontend.
24. **Input Validation:** Hibernate Validator (`@Valid`) on all incoming DTOs to prevent malicious or malformed data.
25. **Admin Analytics Endpoint:** An endpoint (secured for ADMIN role only) to view total active users and average study times across the platform.
