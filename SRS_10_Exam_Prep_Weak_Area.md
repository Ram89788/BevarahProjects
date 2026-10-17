# Software Requirements Specification (SRS)
## Project 10: Smart Exam Preparation Tracker with Weak-Area Detection

### 1. Project Description
A highly focused study tool that helps students prepare for massive standardized tests or final exams. Instead of just scheduling time, it tracks the student's performance on practice questions and mock exams, uses an algorithm to detect specific "weak areas" in the syllabus, and automatically dynamically adjusts the study plan to focus on those vulnerabilities.

### 2. Core Scope & Tech Stack
- **Frontend:** ReactJS (Vite), TailwindCSS, MaterialUI (Progress bars, analytical charts, quiz interface).
- **Backend:** Java Spring Boot (Scoring logic, weakness detection algorithms, REST APIs).
- **Scope:** Quiz taking interface, detailed performance analytics, dynamic scheduling, and progress tracking.

### 3. Functionalities (Minimum 25)

#### Quiz & Practice Interface (React)
1. **Mock Exam Interface:** A clean, distraction-free UI to take timed multiple-choice practice exams.
2. **Micro-Quizzes:** Short, 5-question pop quizzes generated on the fly focused on a single topic.
3. **Save & Resume:** Ability to pause a practice exam and resume it later without losing progress.
4. **Instant Feedback Toggle:** Users can choose to see the correct answer immediately after clicking, or only at the end of the exam.
5. **Question Flagging:** A button to flag a question during the exam to review it later, regardless of whether they get it right or wrong.

#### Analytics & Weak-Area Detection
6. **Detailed Results Dashboard:** After an exam, view a breakdown of accuracy categorized by syllabus topic (e.g., "Algebra: 90%, Geometry: 40%").
7. **The "Weakness Matrix":** A visual heatmap (MaterialUI/Recharts) highlighting exactly which sub-topics the user is struggling with the most.
8. **Time-Spent Analysis:** Track how long the user spends on each question; flag topics where the user is accurate but extremely slow.
9. **Historical Progress Line:** A chart showing the overall mock exam score improving over time.
10. **Error Log:** A dedicated page compiling all questions the user has ever answered incorrectly, available for review.

#### Dynamic Study Planning
11. **Adaptive Study Recommendations:** The dashboard explicitly suggests: "You should study Geometry today. Your accuracy is 40%."
12. **Custom Study Block Creation:** Generate a study task directly from the weakness matrix.
13. **Target Score Setting:** User inputs their target exam score, and the app calculates the required accuracy improvement needed in weak areas to achieve it.
14. **Daily Goals:** Auto-generated daily tasks prioritizing the weakest topics.

#### Backend (Spring Boot Core Features)
15. **Question Bank Management APIs:** Admin endpoints to upload, categorize, and tag thousands of practice questions via CSV.
16. **Exam Scoring Service:** A Java service that grades submitted exams, calculates time-per-question, and updates the user's historical statistics.
17. **Weakness Detection Algorithm:** Logic that weighs recent mistakes heavier than older mistakes to accurately determine current weak areas.
18. **User Progress API:** Endpoints returning complex JSON aggregations of user statistics for the frontend charts.
19. **JWT Security:** Standard Spring Security implementation to protect user data.

#### Organization & Motivation
20. **Exam Countdown Timer:** A persistent, highly visible countdown to the actual exam date.
21. **Confidence Toggles:** After reviewing a topic, the user can manually increase their "Confidence Score" for that area.
22. **Streaks & Badges:** Gamification elements rewarding consecutive days of taking at least one practice quiz.
23. **Export Weaknesses:** Download a PDF summary of weak areas to share with a human tutor.

#### System Features
24. **Pagination for Error Logs:** Use Spring Data `Pageable` to efficiently load the user's potentially massive history of incorrect questions.
25. **Admin Analytics:** View global statistics on which questions are answered incorrectly most often, allowing admins to fix potentially confusing questions.
