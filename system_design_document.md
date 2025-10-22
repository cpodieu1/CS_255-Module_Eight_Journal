# CS 255 System Design Document Template

This template lays out all the different sections that you need to complete for Project Two. Each section has guidance to prompt your thinking. You will need to continually reference the interview transcript as you work to make sure that you are addressing your client’s needs. There is no required length for the final document. Instead the goal is to complete each section based on what your client’s needs are. Remove this note when you are finished, and replace all bracketed text with the relevant information.

## UML Diagrams

### UML Use Case Diagram
[ (DriverPass)
Actors
•	Student (primary)
•	Instructor
•	Admin
•	Payment Processor (external system)
•	Email and SMS Service (notifications)
Main use cases
•	Student: Create account and Sign in, View packages, Purchase package, Take practice tests, View progress, Schedule, Reschedule and Cancel driving lesson, View lesson calendar, Reset password.
•	Instructor: Set availability, Accept and decline lesson requests, Record lesson notes and attendance.
•	Admin: Manage users, Manage packages and test content, Manage instructors & schedules, View reports.
•	External: Process payment, Send confirmations and reminders.
.]


### UML Activity Diagrams
1.	[Student logs in
2.	Open Lesson Calendar → pick location/instructor/date
3.	System checks package hours and schedule conflicts
4.	[Has hours available?]
o	No → prompt to purchase/upgrade package → return
o	Yes → create Lesson reservation
5.	Send email/SMS to student and instructor
6.	Status = Confirmed (or Pending instructor approval if policy requires)
7.	Show updated calendar to student
Alternate flows: reschedule (cancel old, create new), cancel (hours credited back).]


### UML Sequence Diagram
[Lifelines: Student UI → Web App/API → Scheduler Service → Instructor Calendar → Notification Service (Email/SMS)
1.	Student UI → API: request available slots (filters)
2.	API → Scheduler: get availability
3.	Scheduler → Instructor Calendar: read openings → return list
4.	Student UI: selects slot → API: book(slotId)
5.	API → Scheduler: validate (hours, conflicts)
6.	Scheduler → Instructor Calendar: place hold / create event
7.	Scheduler → API: booking OK
8.	API → Notification Service: send confirmations
9.	API → Student UI: booking details (status, time, instructor)
If validation fails: API returns message (insufficient hours or slot taken).
.]

### UML Class Diagram
•	[User(userId, name, email, phone, role, status)
o	Student: licensePermit#, packageBalanceHours
o	Instructor: license#, rating, serviceArea
•	Package(packageId, name, hoursIncluded, price, testAccess)
•	Order(orderId, studentId, total, status, createdAt)
•	Payment(paymentId, orderId, amount, method, status, timestamp)
•	Lesson(lessonId, studentId, instructorId, startTime, endTime, location, status, notes)
•	AvailabilitySlot(slotId, instructorId, startTime, endTime, isBooked)
•	PracticeTest(testId, title, category, passScore)
•	Question(questionId, testId, text, options[4], correctIndex)
•	TestAttempt(attemptId, testId, studentId, score, startedAt, finishedAt)
Associations
•	Student places 0..* Orders; Order has 1..* Payments
•	Student books 0..* Lessons; Instructor conducts 0..* Lessons
•	Instructor owns 0..* AvailabilitySlots
•	PracticeTest contains 1..* Questions
•	Student takes 0..* TestAttempts (each for one PracticeTest)
.]

## Technical Requirements
[Architecture
•	Web app (responsive) + REST API + relational DB; stateless services behind a load balancer.
Software stack
•	Front end: React (or Angular), HTML/CSS.
•	Back end: Python (FastAPI/Flask) or Node.js (Express).
•	Database: PostgreSQL with ORM and constraints; Redis (optional) for sessions/caching.
•	Payments: Stripe (card + wallet).
•	Notifications: SendGrid (email), Twilio (SMS).
•	AuthN/AuthZ: OAuth2/OIDC (Okta/Azure AD), JWT; roles: Admin/Instructor/Student.
•	CI/CD: GitHub Actions/Azure DevOps; containerized with Docker; IaC (Terraform) optional.
### Infrastructure
•	Cloud: AWS or Azure.
•	2+ API instances behind ALB/ALB; managed Postgres (RDS/Azure DB); Object storage for assets; VPC, subnets, WAF/CDN.
•	Backups: automated daily full + 15-min PITR; RPO ≤ 15 min, RTO ≤ 1 hr.
•	Monitoring/Logs: CloudWatch/App Insights, structured logs, alerts.
### Security
•	HTTPS/TLS 1.2+, HSTS; secrets in a vault; row-level access by user role.
•	Password hashing (Argon2/bcrypt), MFA optional; input validation; rate limiting; audit logs.
•	Data at rest encryption (KMS); least-privilege IAM; regular vulnerability scans.
### Nonfunctional targets
•	Availability 99.9%; p95 API latency < 300 ms; page load < 2 s on broadband.
•	Scalability to 10k monthly active students.
•	Accessibility WCAG AA; GDPR-style privacy practices.
.]

 
