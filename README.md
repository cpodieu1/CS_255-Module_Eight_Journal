# CS_255-Module_Eight_Journal

# Project Reflection — DriverPass

## Brief summary.
DriverPass is a web app for a local driving school. The client needed a system for students to create accounts, purchase lesson packages, view availability, book/cancel sessions, and receive notifications; instructors and admins manage schedules, students, and payments.

## What I did well.
I scoped clear functional and non-functional requirements, kept a traceability link from user stories → “system shall” statements → UML (use-case, sequence, activity) → acceptance tests, and documented SLAs, security, and audit needs. My diagrams made ownership and error paths explicit.

## What I’d revise.
I’d expand alternate/error flows (e.g., payment failures, double bookings) in the sequence diagrams and add a simple data model/ERD with RBAC rules. I’d also include monitoring hooks and a rollback plan in the maintenance workflow.

## Interpreting user needs.
I translated interviews into personas (Student, Instructor, Admin), wrote user stories with MoSCoW priorities, and turned them into testable requirements with acceptance criteria. This ensured the design matched real tasks and let stakeholders validate scope early, reducing rework later.

## My design approach (now and future).
Start with problem framing and context diagram → personas and stories → prioritize → API-first contracts → domain model → sequence/activity diagrams → wireframes → iterate. I’ll continue using TDD for core logic, add usability checks, and plan for operability (logging, metrics, alerts, runbooks) so maintenance is built in, not bolted on.