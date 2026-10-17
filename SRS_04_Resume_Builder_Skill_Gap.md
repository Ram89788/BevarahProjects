# Software Requirements Specification (SRS)
## Project 04: Resume Builder + Skill Gap Analyzer

### 1. Project Description
A career development platform that helps job seekers build professional resumes while simultaneously analyzing their skills against live job descriptions. Users paste a target job description, and the system highlights missing keywords, suggests skill upgrades, and helps tailor the resume to pass Applicant Tracking Systems (ATS).

### 2. Core Scope & Tech Stack
- **Frontend:** ReactJS (Vite), TailwindCSS, MaterialUI (for forms, steppers, and PDF rendering preview).
- **Backend:** Java Spring Boot (REST APIs, Text Analysis, PDF Generation).
- **Scope:** Dynamic form building, Natural Language Processing (NLP) integration, ATS scoring algorithms.

### 3. Functionalities (Minimum 25)

#### Frontend (React + MaterialUI)
1. **Multi-Step Resume Builder:** Use MaterialUI Stepper to guide the user through sections: Personal Info, Experience, Education, and Skills.
2. **Live PDF Preview:** Split-screen layout where form inputs instantly update a rendered resume preview on the right side.
3. **Template Selector:** Carousel to choose between various professional, ATS-friendly resume templates.
4. **Target Job Input:** A dedicated text area to paste the description of the job the user is applying for.
5. **Skill Gap Dashboard:** Visual display (radar charts or progress bars) comparing the user's listed skills against the required skills from the job description.
6. **Action Verb Suggestions:** Tooltips or dropdowns suggesting strong action verbs (e.g., "Spearheaded", "Optimized") while typing experience bullet points.
7. **Drag & Drop Reordering:** Allow users to drag and reorder their job experiences or skill sections.
8. **Responsive Design:** Tailwind classes ensuring the builder is usable on both desktop and tablet devices.

#### Backend (Spring Boot Core Features)
9. **User Management:** Spring Security for account creation, login, and storing multiple versions of a user's resume.
10. **Resume CRUD Operations:** Endpoints to save, update, and retrieve the structured JSON data of a user's resume.
11. **Keyword Extraction Service:** A Java service that parses the target job description to extract high-frequency noun phrases and technical skills.
12. **Skill Matching Algorithm:** Compare the extracted job keywords against the user's resume text to calculate a percentage "Match Score".
13. **PDF Generation Engine:** Utilize libraries like Apache PDFBox or iText to compile the JSON resume data into a perfectly formatted, downloadable PDF.
14. **Grammar & Spell Check API:** Integration with an external API (like LanguageTool) to flag typos in the bullet points.

#### Analytics & Enhancement
15. **Missing Skills Highlighter:** Return a list of critical skills found in the job description that are entirely missing from the resume.
16. **Formatting Check:** Backend validation to ensure the resume isn't too long (e.g., warning if word count suggests it will spill onto 3 pages).
17. **Skill Upgrade Recommendations:** Suggest online courses (e.g., Coursera/Udemy links) for the specific skills identified as "missing" in the gap analysis.
18. **Version Cloning:** Allow users to duplicate an existing resume so they can tweak it for a slightly different role without starting from scratch.

#### Organization & Sharing
19. **Cover Letter Generator:** Auto-generate a basic cover letter draft by combining the user's top skills and the target company's name.
20. **Shareable Web Link:** Generate a public, read-only URL for the resume (e.g., for adding to a LinkedIn profile).
21. **Download Tracking:** Track how many times the public link has been viewed or the PDF downloaded.

#### System Features & Security
22. **Data Privacy:** Strict GDPR-compliant data deletion endpoint to completely wipe personal data and PDFs from the server.
23. **CORS Configuration:** Spring Boot configured to securely accept requests only from the deployed React frontend domain.
24. **File Storage Handling:** Use Amazon S3 (or local file storage configured via Spring) to temporarily store generated PDFs before download.
25. **Admin Dashboard:** Monitor platform usage, most popular templates, and system errors.
