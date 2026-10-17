# Software Requirements Specification (SRS)
## Project 07: Internship Tracker + Predictive Recommendation

### 1. Project Description
A centralized platform for university students to track their internship applications across multiple companies. Beyond a simple Kanban board, the system analyzes the student's profile (skills, major, past applications) and uses a predictive recommendation engine to suggest new internship postings where the student has the highest statistical probability of getting an interview.

### 2. Core Scope & Tech Stack
- **Frontend:** ReactJS (Vite), TailwindCSS, MaterialUI (Kanban board, statistics charts).
- **Backend:** Java Spring Boot (REST APIs, Web Scraping/API ingestion, Recommendation Logic).
- **Scope:** Application lifecycle tracking, data visualization, basic ML/Rule-based recommendations.

### 3. Functionalities (Minimum 25)

#### Frontend (React + MaterialUI)
1. **Application Kanban Board:** A drag-and-drop interface (using `react-beautiful-dnd`) to move applications through stages: Wishlist, Applied, Interviewing, Offer, Rejected.
2. **Add Application Modal:** A comprehensive form to log company name, role, applied date, link to posting, and notes.
3. **Chrome Extension Integration (Optional Prep):** A UI endpoint designed to easily accept data pushed from a browser extension (to quick-save jobs).
4. **"Smart Match" Dashboard:** A dedicated tab displaying AI-recommended internships, sorted by "Match Percentage".
5. **Analytics Charts:** Recharts/Chart.js showing a funnel chart of the user's conversion rate (Applied -> Interview -> Offer).
6. **Timeline View:** A chronological history of all updates made to an application (e.g., "Moved to Interview on Oct 12").
7. **Task Reminders:** A specialized to-do list for action items (e.g., "Send Thank You Email to Recruiter").
8. **Dark Mode & Responsive UI:** Ensure the tracker is highly usable on mobile for quick updates after a phone screen.

#### Backend (Spring Boot Core Features)
9. **User Authentication:** Spring Security handling student accounts and encrypting personal data.
10. **Application CRUD:** High-performance REST endpoints to manage the lifecycle of an internship application.
11. **Recommendation Engine:** A Spring service that compares the user's "Skills" array against a database of open internships, assigning a match score based on keyword overlap and historical success of similar students.
12. **Job Ingestion API:** A scheduled task (`@Scheduled`) that pulls new internship postings from external APIs (like GitHub Jobs, or an internal university career portal).
13. **Email Parsing (Advanced):** Integration with an email API (like SendGrid/Gmail) to detect "Interview Invitation" emails and automatically update the Kanban status.
14. **Due Date Reminders:** Backend logic that checks application deadlines and sends a notification if a "Wishlist" job is about to expire.

#### Analytics & Insights
15. **Global Company Stats:** Show users aggregated, anonymized data (e.g., "It takes an average of 14 days to hear back from Google").
16. **Skill Gap Analysis:** If a user is rejected frequently, the system highlights common skills required by those roles that the user lacks.
17. **Interview Prep Notes:** A dedicated rich-text area within an application card to save LeetCode links or behavioral stories specific to that company.
18. **Salary/Stipend Tracker:** Allow users to input offer details and compare them visually across multiple offers.

#### Networking & Sharing
19. **Referral Request System:** Identify if an alumni from the university works at the target company and suggest reaching out.
20. **Shareable "Hired" Graphic:** Generate a customized "I got the offer!" image for the student to post on LinkedIn.
21. **Export Data:** Allow users to download their entire application history as a CSV spreadsheet.

#### System Maintenance & Admin
22. **Database Migration:** Use Flyway or Liquibase in Spring Boot to manage schema changes as the recommendation engine evolves.
23. **Global Job Board Management:** Admins can manually add, edit, or remove scraped job postings to ensure data quality.
24. **Exception Handling:** Custom `@ControllerAdvice` to handle duplicate job entries gracefully.
25. **Data Purge:** Allow users to permanently delete their account and all associated application data to comply with privacy laws.
