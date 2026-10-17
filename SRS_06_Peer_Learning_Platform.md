# Software Requirements Specification (SRS)
## Project 06: Peer Learning Platform with Reputation Scoring

### 1. Project Description
A collaborative, StackOverflow-style Q&A and tutoring platform exclusively for university students. Students can ask course-specific questions, share resources, and provide answers. The platform uses a dynamic reputation scoring system to incentivize high-quality contributions, granting moderation privileges and "Top Peer" badges to highly rated users.

### 2. Core Scope & Tech Stack
- **Frontend:** ReactJS (Vite), TailwindCSS, MaterialUI (for structured cards, avatars, and badges).
- **Backend:** Java Spring Boot (REST APIs, Reputation Algorithm, JPA relationships).
- **Scope:** Threaded Q&A, upvote/downvote mechanics, user leveling, and real-time notifications.

### 3. Functionalities (Minimum 25)

#### Frontend (React + MaterialUI)
1. **Global Feed Dashboard:** A feed of the latest questions styled with MaterialUI Cards, displaying the author, tags, and upvote count.
2. **Rich Text Q&A Editor:** Integrate a Markdown editor allowing users to post code blocks, math equations (LaTeX), and images in their questions/answers.
3. **Course-Specific Tagging:** Autocomplete inputs allowing users to tag a question with a specific course code (e.g., CS101) using MaterialUI Chips.
4. **Upvote/Downvote UI:** Interactive arrows on answers and questions that instantly update the score UI (optimistic UI rendering).
5. **Accepted Answer Toggle:** The original poster can click a green checkmark to "Accept" the best answer, pinning it to the top.
6. **Reputation Badge Display:** A visual badge next to the user's avatar showing their current level (e.g., Bronze, Silver, Gold).
7. **User Profile Page:** Display the user's total reputation, a list of their top-rated answers, and subjects they are most active in.
8. **Real-Time Notification Dropdown:** A bell icon that lights up when someone answers a user's question or upvotes their post.

#### Backend (Spring Boot Core Features)
9. **Authentication & Authorization:** Spring Security JWT. Certain API endpoints (like deleting comments) check the user's reputation score before allowing access.
10. **Post & Comment CRUD:** REST endpoints managing the creation, reading, and soft-deletion of questions and answers.
11. **Reputation Calculation Engine:** A Spring service that listens for vote events and updates the user's total score (+10 for an upvote, -2 for a downvote, +15 for an accepted answer).
12. **Search API:** An endpoint allowing full-text search across question titles and bodies, prioritizing results with higher upvotes.
13. **Tagging Logic:** A many-to-many JPA mapping between Questions and Tags to efficiently query "All questions for CS101".
14. **Activity Stream:** Endpoint that returns a chronological history of a user's interactions for their profile page.

#### Gamification & Community Moderation
15. **Privilege Thresholds:** Business logic that unlocks features based on score (e.g., 50 rep to comment, 500 rep to retag questions, 1000 rep to access moderator queues).
16. **Bounty System:** A user can sacrifice some of their own reputation points to place a "Bounty" on a difficult question to attract answers.
17. **Flagging System:** Users can report inappropriate content; highly flagged posts are automatically hidden pending admin review.
18. **Review Queue:** High-reputation users get access to a special dashboard to vote on keeping or deleting flagged posts.

#### Advanced Features & Engagement
19. **"Trending Topics" Algorithm:** Backend logic to calculate which course tags have the most activity in the last 24 hours.
20. **Weekly Newsletter:** Spring Mail integration that sends users a summary of the top questions in their subscribed tags.
21. **Code Snippet Execution:** (Optional/Advanced) Integration with an external API (like JDoodle) to run code snippets directly within a question.
22. **Similar Questions Suggestion:** Before a user posts a new question, suggest existing similar questions to prevent duplicates.

#### Security & Administration
23. **Rate Limiting:** Prevent users from spamming upvotes or questions using Bucket4j or custom Spring Interceptors.
24. **SQL Injection Protection:** Utilize Spring Data JPA parameterized queries to ensure all search inputs are sanitized.
25. **Admin Dashboard:** A secured area for university staff to manually adjust reputation scores, ban malicious accounts, or broadcast global announcements.
