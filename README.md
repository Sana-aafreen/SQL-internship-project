# Optimized Database Design & Analytics for LMS
Report
________________________________________
## 1. Project Overview
This project involved designing and optimizing the relational database backbone of a Learning Management System (LMS). The schema supports key LMS operations: student registration, instructor management, course delivery, module tracking, enrollments, grading, and attendance. The design ensures scalability, consistency, and query performance.
________________________________________
## 2. Design Choices
Entity Modeling
•	Core Entities: Students, Instructors, Courses, Modules, Enrollments, Grades, Attendance.
•	Relationships:
o	One Instructor → Many Courses.
o	One Course → Many Modules.
o	Many Students ↔ Many Courses (via Enrollments).
o	Enrollments linked to Grades and Attendance for detailed performance tracking.
Normalization
•	Schema normalized to Third Normal Form (3NF):
o	Removed repeating groups (e.g., no multiple courses stored in a student record).
o	Eliminated redundancy (grades, attendance separated into their own tables).
o	Ensured every non-key attribute depends only on its primary key.
Primary Keys
•	UUIDs (CHAR(36)) used as primary keys for portability and uniqueness across distributed systems.
•	Alternative option considered: AUTO_INCREMENT integers (simpler but less scalable).
________________________________________
## 3. Optimization Strategies
Indexes
•	Added indexes on:
o	enrollments(student_id), enrollments(course_id) → Fast lookup of student enrollments.
o	modules(course_id, position) → Efficient retrieval of course modules in order.
o	grades(enrollment_id, module_id) → Quick grade lookups.
o	attendance(enrollment_id, module_id) → Fast attendance tracking.
Views
•	Created course_module_count view for reporting the number of modules per course.
Query Optimization
•	Used EXPLAIN to validate query execution paths.
•	Optimized joins by ensuring foreign keys are indexed.
•	Limited result sets (LIMIT, filtering with WHERE) to reduce scan cost.
________________________________________
## 4. Sample Analytical Insights
•	Most Enrolled Courses: Identifies popular courses for curriculum planning.
•	Top 5 Active Students: Measures engagement based on completed modules.
•	Completion Rates: Tracks learning outcomes per course.
•	Instructor Performance: Evaluates teaching effectiveness via average student grades.
•	Attendance Reports: Monitors student participation and compliance.
________________________________________
## 5. Challenges & Resolutions
•	UUID vs AUTO_INCREMENT: Chose UUIDs for flexibility, but noted higher storage cost.
•	PostgreSQL vs MySQL Differences: Converted PostgreSQL-only functions (uuid_generate_v4, generate_series, random()) into MySQL equivalents (UUID(), RAND(), manual number tables).
•	Data Population: Used INSERT … SELECT with helper number sets to simulate realistic datasets.
________________________________________
## 6. Conclusion
The project successfully delivered a normalized, optimized LMS database capable of handling core academic workflows and advanced reporting. Performance tuning (indexing + query analysis) ensured efficient data retrieval. The final design balances data integrity, performance, and scalability, providing a strong foundation for a production-ready LMS.
________________________________________
📌 Prepared by: Sana Aafreen
📅 Date: 27-09-2025

