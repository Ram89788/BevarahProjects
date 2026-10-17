# Software Requirements Specification (SRS)
## Project 02: Smart Attendance + Behavior Analytics Dashboard

### 1. Project Description
This system modernizes classroom management for schools and universities. Beyond simply logging presence or absence, it tracks student behavioral metrics (participation, focus, disruption) and visualizes this data in a comprehensive analytics dashboard. It allows educators to identify at-risk students early based on attendance drops or behavioral shifts.

### 2. Core Scope & Tech Stack
- **Frontend:** ReactJS (Vite), TailwindCSS, MaterialUI (for complex data tables and charts).
- **Backend:** Java Spring Boot (REST APIs, Spring Data JPA, Role-Based Access Control).
- **Scope:** Bulk data entry, statistical aggregations, real-time filtering, and multi-role access.

### 3. Functionalities (Minimum 25)

#### Frontend (React + MaterialUI)
1. **Teacher Dashboard:** A central hub displaying today's classes, overall attendance rate, and alerts for at-risk students.
2. **Rapid Attendance Grid:** A MaterialUI DataGrid allowing teachers to mark attendance (Present, Absent, Late) for 50+ students in under a minute via toggle switches.
3. **Behavior Logging Modal:** A quick-entry form to log behavior points (+1 for great question, -1 for disruption) during class.
4. **Student Profile View:** A detailed page for a single student showing their attendance history heatmap and a radar chart of their behavior scores.
5. **Analytics Charts:** Line charts plotting class attendance over the semester versus average grades.
6. **Class Roster Management:** UI to upload a CSV to automatically populate a class list.
7. **Filter & Search:** Advanced filtering on the dashboard to find students with < 75% attendance.
8. **Responsive Layout:** Tailwind grid/flexbox ensuring the attendance grid is usable on a teacher's iPad or mobile phone.

#### Backend (Spring Boot Core Features)
9. **Multi-Role Security:** Spring Security configuring roles for `ADMIN` (Principals), `TEACHER`, and `STUDENT/PARENT` (read-only).
10. **Attendance Logging API:** High-performance REST endpoint capable of accepting a bulk array of student attendance statuses in one payload.
11. **Behavior Scoring Engine:** Business logic that aggregates daily behavior points into a weekly "Conduct Score."
12. **At-Risk Detection Algorithm:** A Spring `@Service` that runs daily to identify students who missed 3 consecutive classes or whose behavior score dropped by 30%.
13. **Class & Subject Management:** CRUD endpoints to create academic years, semesters, subjects, and assign teachers to them.
14. **Parent Notification API:** Trigger an automated email/SMS to parents if a student is marked Absent unexcused.

#### Data Analytics & Reporting
15. **Monthly Attendance Report:** Endpoint that generates a structured JSON report aggregating attendance percentages per grade level.
16. **Behavioral Trend Analysis:** Compare a student's behavior in morning classes versus afternoon classes.
17. **Export to Excel/PDF:** Use Apache POI or iText in Spring Boot to generate downloadable official attendance reports.
18. **Custom Excuse Workflows:** API flow allowing parents to submit a sick note, which marks the absence as "Excused" pending teacher approval.

#### Collaboration & System Features
19. **Seating Chart Builder:** A drag-and-drop React interface for teachers to design a classroom layout, linking seats to student profiles.
20. **Audit Trail:** Spring Data Envers integration to track exactly which teacher altered an attendance record and when.
21. **Pagination & Sorting:** Efficient database querying using Spring Data `Pageable` for tables with thousands of attendance records.
22. **School-Wide Broadcast:** Admins can post a banner message visible on all teacher dashboards.
23. **Data Caching:** Redis or Spring `@Cacheable` applied to frequently accessed analytics (like school-wide average attendance) to reduce DB load.
24. **API Rate Limiting:** Prevent abuse of the login and data export endpoints.
25. **Swagger UI Integration:** Implement `springdoc-openapi` to automatically generate interactive API documentation for frontend developers.
