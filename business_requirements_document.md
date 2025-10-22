# CS 255 Business Requirements Document Template

## Complete this template by replacing the bracketed text with the relevant information.

This template lays out all the different sections that you need to complete for Project One. Each section has guiding questions to prompt your thinking. These questions are meant to guide your initial responses to each area. You are encouraged to go beyond these questions using what you have learned in your readings. You will need to continually reference the interview transcript as you work to make sure that you are addressing your client’s needs. There is no required length for the final document. Instead, the goal is to complete each section based on your client’s needs.

Tip: You should respond in a bulleted list for each section. This will make your thoughts easier to reference when you move into the design phase for Project Two. One starter bullet has been provided for you in each section, but you will need to add more.
System Components and Design
Purpose
What is the purpose of this project? Who is the client and what do they want their system to be able to do?
[ Purpose: Design a cloud, web system to deliver DMV-aligned driver training and manage DriverPass’s operations (training, scheduling, tracking, reporting). 
Client and needs: The client is DriverPass (owner Liam; IT officer Ian). They want a system that lets students take online classes and practice tests, book, modify, cancel 2-hour on-road lessons and packages, track progress and instructor notes, audit who changed what with printable activity reports, provide role-based access (incl. password resets), integrate with DMV updates, notifications, access data from any device and download reports, and capture customer info & payments.
 ]

## System Background
What does DriverPass want the system to do? What is the problem they want to fix? What are the different components needed for this system?
•	[ Offer online classes and practice tests and manage on-the-road lesson reservations (2-hour sessions), bookable online or by a secretary, and track which student–driver–car–time combination is set.
Enable anywhere web access (desktop, mobile) and let staff download reports for offline analysis.
Enforce role-based security (admin resets, block access) and audit tracking with printable activity reports.
Support student self-service (create, modify, cancel appointments, password reset).
Keep training aligned with DMV (receive rule, question updates with notifications).
Run as a cloud, web app with backups, security handled by the platform.
Capture customer and payment info and allow package management (three lesson packages; ability to disable a package).

Problem they want to fix
There’s a market gap: many students fail DMV tests; DriverPass aims to improve outcomes with better training (online + on-road).

## Components needed
Presentation, UI (pages for progress, notes, forms, contact).
Database layer (student, driver, car, schedule, packages, payments, audit logs). Link DB to interface as a project step. 
Business logic layer (security, roles, rights, scheduling rules, reporting).
Integrations: DMV update, notification service and email, report export.
Cloud, web platform for hosting, backup, and security.]

## Objectives and Goals
What should this system be able to do when it is completed? What measurable tasks need to be included in the system design to achieve this?
•	[Provide online classes and practice tests with progress details (test name, time, score, status) and access from any device.
Enable students (and the secretary) to book, modify, cancel 2-hour on-road lessons, assigning student–driver–car–time, and keep an audit trail with printable activity reports.
Enforce role-based security (admin resets, disable access) and self-service password reset.
Stay current with DMV rules, questions and notify staff when updates arrive.
Run as a cloud, web system with backups, security handled by the platform.
Support data entry and reporting: student info forms, driver notes (time windows + comments), contact pages, and downloadable reports.
Manage packages (3 predefined; admin can disable a package).
Capture customer and payment details and pickup/drop-off locations.

## Measurable design tasks / deliverables
Requirements & models completed: use cases, activity diagrams, class diagram approved by client.
Interface built (pages above) and linked to the database; both milestones closed.
Business-logic layer (RBAC, scheduling rules, audit logging) implemented.
Testing phase completed with sign-off; system delivered.

## Operational criteria met:
Book, modify, cancel lesson with conflict checks and 2-hour duration; who, when changes logged and printable report generated.
Students view practice-test progress (name, time, score, status).
Admin resets/block accounts; users self-reset passwords.
DMV update ingested and notification issued. 
Reports exportable for offline work.]

## Requirements
Nonfunctional Requirements
In this section, you will detail the different nonfunctional requirements for the DriverPass system. You will need to think about the different things that the system needs to function properly.

## Performance Requirements
What environments (web-based, application, etc.) does this system need to run in? How fast should the system run? How often should the system be updated?
•	[Web-based, cloud-hosted, accessible from any computer or mobile device; backups and security handled by the platform.
Speed (measurable targets not stated in interview, recommended NFRs)
          Page/view load ≤ 2 s (p50), ≤ 4 s (p95).
           Login/search/booking actions ≤ 3 s end-to-end; report export starts ≤ 10 s.
           Uptime ≥ 99.9% monthly; backups hourly (RPO ≤1 h), restore in ≤4 h (RTO).
Update cadence
DMV content: system receives notifications and should sync within 24 h of a DMV change (daily auto-check).
Platform, security: routine releases monthly; critical patches within 24–48 h.]

## Platform Constraints
What platforms (Windows, Unix, etc.) should the system run on? Does the back end require any tools, such as a database, to support this application?
•	[Web/cloud-hosted; access from any computer or mobile device OS-agnostic (browser based). Backups, security handled by the cloud. 
Relational database (project step: “build the database tables and link it to the interface”).
Business-logic layer for roles, rights, security and scheduling rules.]

## Accuracy and Precision
How will you distinguish between different users? Is the input case-sensitive? When should the system inform the admin of a problem?
•	[Use role-based accounts Owner (Liam), IT officer (Ian), Secretary, and Students/Customers each with defined rights (e.g., Ian can reset passwords and block access)
Case sensitivity: Not specified in the interview. Recommended: emails/usernames case-insensitive, passwords case-sensitive, and store canonical forms (e.g., lowercased emails).

## When to inform admin of a problem:
Explicit in interview: notify on DMV updates.
Recommended triggers (not explicitly stated): repeated failed logins or blocked accounts, scheduling conflicts/overbooking, payment failures, system/DB errors, or suspicious changes flagged via the required activity/audit trail (“who made/canceled/modified” with printable reports).]

## Adaptability 
Can you make changes to the user (add/remove/modify) without changing code? How will the system adapt to platform updates? What type of access does the IT admin need? 
•	[Yes, via UI: secretary enters student info in input forms; customers can self-reset passwords; IT can reset or block accounts (no code change).
Run it in the cloud, backups/security handled by the provider, minimizing technical overhead. For content/regulatory changes, ingest DMV updates with notifications.
Full account control: reset passwords and block access; enforce role-based rights]

## Security
What is required for the user to log in? How can you secure the connection or the data exchange between the client and the server? What should happen to the account if there is a “brute force” hacking attempt? What happens if the user forgets their password? 
•	[User account and password (role-based account per user); recommend email-as-username and optional 2FA
Enforce HTTPS/TLS end-to-end, HSTS, secure cookies (HttpOnly/SameSite), CSRF tokens, input validation, and hashed passwords (Argon2/bcrypt).
Encrypt at rest, use least-privilege roles, and keep an audit trail of changes]

## Functional Requirements
Using the information from the scenario, think about the different functions the system needs to provide. Each of your bullets should start with “The system shall . . .” For example, one functional requirement might be, “The system shall validate user credentials when logging in.”
•	[The system shall provide online classes and practice tests for students.
The system shall let customers book, modify, and cancel 2-hour driving lessons online or via the secretary.
The system shall assign and track each reservation’s student, driver, car, date, and time.
The system shall maintain three lesson packages and allow an admin to disable a package.
The system shall support role-based access for owner, IT officer, secretary, and customers.
The system shall offer web access from any computer or mobile device and allow downloading reports for offline work.
The system shall run as a cloud-hosted web application with backup and security handled by the platform.
The system shall capture student information, including name, address, phone, state, payment details, and pickup/drop-off locations]

## User Interface
What are the needs of the interface? Who are the different users for this interface? What will each user need to be able to do through the interface? How will the user interact with the interface (mobile, browser, etc.)? 
•	[Web, cloud-hosted UI; works on any computer or mobile device; support downloading --- reports; backups/security handled by the platform.
-- Pages/flows: online-test progress (test name, time, score, status), driver notes table (lesson time, start/end hour, comments), student info form, contact page, reservation ---- booking/modify/cancel, printable activity report, password reset.
-- Owner (Liam), IT officer (Ian), Secretary, Customer/Student.
-- Owner: access data anywhere, download reports, review activity/audit printouts.
-- IT officer: reset passwords, block access, maintain/modify system.
-- Secretary: create bookings by phone/office; fill student info form. 
Customer/Student: book/modify/cancel lessons online; view test progress; reset password; provide profile/payment info; select packages
Via a browser on desktop or mobile; the system is web/cloud based.]

## Assumptions
What things were not specifically addressed in your design above? What assumptions are you making in your design about the users or the technology they have? 
•	[Accessibility/ADA compliance, localization, and cross-browser support (only “any computer or mobile device” is stated).
Performance/SLA targets (page loads, booking latency), uptime/SLOs, and backup/RPO/RTO (only that cloud handles backups/security).
Security specifics: password rules/2FA, session timeouts, rate-limiting, data retention, log retention, breach/alerting thresholds (only roles, resets, and audit are stated).
Payments: PCI-DSS approach (they want to collect card data, but gateway/tokenization/storage rules aren’t defined)
Scheduling edge cases: time-zone handling, instructor/car capacity rules beyond “2-hour sessions,” cancellation/no-show policies.
Content ops: who authors/approves online class material; cadence for DMV sync beyond “receive updates and notify.”
Reporting scope/exports beyond “print activity report” and “download reports.”

## Assumptions I’m making

Web, cloud-hosted app usable on modern desktop/mobile browsers; no native apps.
Users have reliable internet + email/SMS for self-service password reset; IT can still reset/block accounts. 
Role-based access with at least Owner, IT, Secretary, Student; all actions are audit-logged.
DMV provides a consumable feed/API for rules/questions; system polls and sends internal notifications.
Payments processed via a PCI-compliant gateway (tokenization); the system avoids storing full card numbers despite collecting payment info.]

## Limitations
Any system you build will naturally have limitations. What limitations do you see in your system design? What limitations do you have as far as resources, time, budget, or technology?
•	[Online-only edits; offline is read-only. Modifying data while offline risks duplicates, so updates must occur online; exports (e.g., Excel) are for offline review only.
External dependency on DMV. Training/tests stay current only if DMV pushes updates; delays or format changes can stall content.
Cloud reliance. Backups/security are provider-handled, less direct control and potential vendor constraints.
Payment scope/risk. System collects card data; PCI approach is unspecified—adding compliance and storage limitations.
Package flexibility (v1). Only disabling a package is UI-supported; adding/removing packages needs a developer.
Fixed session length. Lessons are locked at 2 hours, less flexible for varied needs.
Complex scheduling. Must consistently map student–driver–car–time; conflicts remain a risk without robust rules.
Tight timeline & dependencies. Requirements took 14 days; design due by Mar 10, then interface (12 days), DB link (9), business logic (22). Slippage or rework threatens dates.
Staffing constraints. Specific people and availability (e.g., John returns Mar 1) gate class-diagram work.
Budget not specified. Feature choices (e.g., PCI tooling, DMV integration method) may be limited, an explicit risk.
Tech scope. Web/cloud only; no native apps; offline edits unsupported by design.]

Gantt Chart
Please include a screenshot of the GANTT chart that you created with Lucidchart. Be sure to check that it meets the plan described by the characters in the interview.

[Insert chart]
 

