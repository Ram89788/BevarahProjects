# Software Requirements Specification (SRS)
## Project 05: Timetable Optimizer using Constraint Logic

### 1. Project Description
A highly complex administrative tool designed for university and school administrators. It automates the notoriously difficult process of generating academic timetables. Users input courses, professors, rooms, and constraints (e.g., "Professor X cannot teach on Fridays," or "Lab Room B only holds 20 students"), and the system uses a constraint satisfaction algorithm to generate conflict-free schedules.

### 2. Core Scope & Tech Stack
- **Frontend:** ReactJS (Vite), TailwindCSS, MaterialUI (Complex data grids, drag-and-drop calendars).
- **Backend:** Java Spring Boot (Constraint programming engine, JPA relational modeling).
- **Scope:** Deep relational database schemas, genetic algorithms/constraint solvers, and high-density data visualization.

### 3. Functionalities (Minimum 25)

#### Input & Configuration (React Frontend)
1. **Resource Management Grids:** MaterialUI DataGrids to input and manage Lists of Teachers, Rooms, Subjects, and Student Groups.
2. **Room Configuration:** Define capacity, room type (e.g., Lecture Hall, Computer Lab), and building location.
3. **Teacher Constraints:** Forms to input teacher unavailability (specific days/times) and maximum hours per week.
4. **Subject Requirements:** Define if a subject requires a specific room type (e.g., Chemistry requires a Chemistry Lab) and how many lectures per week it needs.
5. **Group/Batch Configuration:** Define the number of students in a batch to ensure they aren't assigned to rooms that are too small.
6. **Hard vs. Soft Constraints Toggle:** Allow admins to define which rules *must* be followed (Hard) and which are just preferences (Soft).

#### The Optimization Engine (Spring Boot Backend)
7. **Constraint Solver Integration:** Utilize a library like OptaPlanner (Timefold) within Spring Boot to handle the heavy mathematical optimization.
8. **Conflict Detection API:** Instantly validate manual schedule changes to warn if it causes a double-booking or room capacity violation.
9. **Generation Trigger:** An asynchronous endpoint that starts the optimization process (which may take several minutes).
10. **Progress Polling:** A WebSocket or polling endpoint to update the frontend on the solver's progress and current "Score" (number of constraints broken).
11. **Stop/Save Engine:** Ability to manually halt the solver if the current schedule is "good enough".

#### Visualizing the Timetable
12. **Master Grid View:** A massive, filterable React matrix showing the entire school's schedule by day and time slots.
13. **Entity-Specific Views:** Switch views to see the timetable from the perspective of a specific Teacher, a specific Room, or a specific Student Batch.
14. **Manual Override (Drag & Drop):** Allow admins to manually drag a scheduled class to a different time slot, immediately triggering the Conflict Detection API.
15. **Color Coding:** Automatically color-code blocks by department or subject type (e.g., Labs are blue, Lectures are green).

#### Export & Distribution
16. **PDF Generation:** Generate highly formatted, printable PDFs of individual teacher or room schedules.
17. **CSV/Excel Export:** Export the raw timetable data for import into the university's main ERP system.
18. **Publish to Student Portal:** A toggle to mark a draft timetable as "Published," making it visible to a student-facing view.

#### Advanced Features & Edge Cases
19. **Consecutive Lecture Limits:** A constraint preventing a teacher from having more than 3 back-to-back classes.
20. **Travel Time Calculation:** A soft constraint preventing a teacher from having back-to-back classes in buildings that are 15 minutes apart.
21. **Lunch Break Enforcement:** Ensure every student group and teacher has at least one free slot between 11 AM and 2 PM.
22. **Multi-Term Support:** Manage separate databases/schedules for Fall, Spring, and Summer semesters.

#### Security & Architecture
23. **Admin Authentication:** Strict Spring Security implementation; only authorized academic planners can edit constraints.
24. **Database Transaction Management:** Ensure that complex updates to constraints or resource lists roll back completely if an error occurs to maintain data integrity.
25. **Audit Logging:** Track who made manual overrides to the generated schedule and when.
