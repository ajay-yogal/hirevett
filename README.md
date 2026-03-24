# Project Definition Document

## 1. Project Overview

**Project Name:** HireVett   
**Category:** Talent Evaluation as a Service (TEaaS)  
**Tech Stack:** PHP Laravel, MySQL, NGINX, Blade/Livewire (or Vue.js)  
**Platform Type:** Web-based SaaS Application   

### One-Liner
A structured hiring evaluation platform that enables recruitment teams to screen, interview, and score candidates through configurable pipelines, then curates qualified talent into a marketplace for registered companies.

### Problem Statement
- Hiring processes across organizations are inconsistent, subjective, and lack standardized evaluation criteria.
- Recruiters spend excessive time on unstructured screening with no reusable outcome data.
- Companies struggle to find pre-evaluated, interview-ready candidates without repeating the full hiring cycle.
- There is no centralized marketplace where candidates are evaluated once and matched many times.

### Solution
A platform that combines structured talent evaluation workflows with a B2B talent marketplace, enabling:
- Recruitment teams to run standardized, scorecard-based hiring pipelines.
- Evaluated candidates to be curated into a centralized, searchable talent pool.
- Registered companies to browse pre-vetted profiles, review interview outcomes, and hire with confidence.

---

## 2. Target Users

| User Role | Description |
|---|---|
| **Super Admin** | Platform owner. Manages system configuration, companies, subscriptions, and global settings. |
| **Company Admin** | Registered company administrator. Manages team members, job postings, and hiring settings. |
| **Recruiter / Hiring Manager** | Creates job openings, defines pipelines, schedules interviews, and evaluates candidates. |
| **Interviewer / Panelist** | Conducts interviews and submits scorecard evaluations for assigned candidates. |
| **Candidate** | Applies to jobs, completes assessments, progresses through the hiring pipeline. |
| **Talent Pool Browser (Company)** | A registered company user who browses the curated talent marketplace to find pre-evaluated candidates. |

---

## 3. Core Modules

### 3.1 Authentication & User Management
- Registration and login (Email/Password, Social OAuth)
- Role-based access control (RBAC) — Super Admin, Company Admin, Recruiter, Interviewer, Candidate
- Multi-company support with team invitations
- Profile management for all user types

### 3.2 Company Management
- Company registration and verification
- Company profile (logo, industry, size, description)
- Subscription/plan management
- Team member management with role assignments

### 3.3 Job Management
- Create, edit, publish, and archive job postings
- Job details: title, description, requirements, location, type (remote/onsite/hybrid), salary range
- Assign hiring pipeline template to each job
- Application form builder (custom fields per job)
- Job visibility settings (public, internal, talent pool only)

### 3.4 Hiring Pipeline Engine
- Configurable multi-stage pipeline per job (e.g., Applied → Screening → Phone Interview → Technical Round → HR Round → Offer → Hired)
- Drag-and-drop pipeline builder for custom stages
- Candidate movement between stages (manual + automated rules)
- Stage-level actions: assign interviewer, schedule interview, attach scorecard, send notification
- Pipeline templates (save and reuse across jobs)
- Stage-level SLA/deadline tracking

### 3.5 Candidate Management
- Candidate profile: resume, contact info, skills, experience, education, portfolio links
- Application tracking across multiple jobs
- Candidate timeline/activity log (all actions, evaluations, communications)
- Candidate status tracking (Active, On Hold, Rejected, Hired, Pooled)
- Resume parsing (optional, future scope)
- Candidate self-service portal (view application status, upload documents, respond to requests)

### 3.6 Interview Scheduling & Management
- Schedule interviews with date, time, location/link
- Assign single or panel interviewers
- Calendar integration (Google Calendar / Outlook — future scope)
- Automated email/notification reminders to candidates and interviewers
- Interview types: Phone Screen, Video, In-Person, Technical Assessment, Group
- Reschedule and cancellation workflows

### 3.7 Scorecard & Evaluation System
- Scorecard template builder (per stage or per job)
- Configurable evaluation criteria (e.g., Communication, Technical Skills, Cultural Fit, Problem Solving)
- Rating scales (1–5 stars, 1–10 numeric, Pass/Fail, custom)
- Weighted scoring (assign weight to each criterion)
- Free-text feedback/comments per criterion
- Multi-interviewer scoring (each panelist submits independently)
- Aggregated score view with consensus/discrepancy highlighting
- Evaluation submission with approval workflow (optional)
- Historical scorecard data retained for talent pool profiles

### 3.8 Talent Pool (Marketplace)
- Candidates who clear defined evaluation thresholds are curated into the talent pool
- Talent pool profiles include: summary, skills, evaluation scores, interview outcomes, recruiter notes
- Searchable and filterable by: skills, experience level, location, evaluation score, industry, availability
- Registered companies can browse, shortlist, and express interest in candidates
- Candidate consent management (opt-in/opt-out of talent pool visibility)
- Talent pool categories/tags (e.g., "Senior Frontend Developer", "Product Manager", "Data Analyst")
- Company-specific shortlists and watchlists
- Contact/request-to-interview workflow between browsing companies and candidates

### 3.9 Communication & Notifications
- In-app notification center
- Email notifications (application received, interview scheduled, evaluation completed, status change)
- Email templates (customizable per company)
- Candidate messaging (in-platform messaging between recruiter and candidate)
- Bulk communication (notify multiple candidates)

### 3.10 Reports & Analytics Dashboard
- **Recruiter Dashboard:** Open jobs, pipeline stage distribution, pending evaluations, upcoming interviews
- **Company Dashboard:** Hiring funnel metrics, time-to-hire, offer acceptance rate, team activity
- **Talent Pool Analytics:** Pool size by skill/category, most-viewed profiles, company engagement
- **Super Admin Dashboard:** Platform-wide metrics, active companies, registered candidates, revenue
- Exportable reports (CSV, PDF)

### 3.11 Admin Panel (Super Admin)
- Company management (approve, suspend, delete)
- Platform-wide settings (default pipeline templates, scorecard templates, email templates)
- Subscription and billing management
- User management and access control
- Content management (landing page, FAQs, terms)
- System logs and audit trail

---

## 4. Non-Functional Requirements

| Area | Requirement |
|---|---|
| **Performance** | Page load < 2 seconds; support for 10,000+ concurrent users at scale |
| **Security** | HTTPS, password hashing (bcrypt), CSRF protection, input validation, role-based access, data encryption at rest |
| **Authentication** | Laravel Sanctum or Passport for API auth; session-based for web |
| **Scalability** | Modular architecture; queue-based processing (Laravel Queues) for emails, notifications, and heavy tasks |
| **Data Privacy** | GDPR-aware candidate consent management; data retention policies; right to deletion |
| **Availability** | 99.9% uptime target; automated backups |
| **Responsiveness** | Mobile-friendly responsive design |
| **SEO** | Public job listings optimized for search engines |

---

## 5. Tech Stack

| Layer | Technology |
|---|---|
| **Backend** | PHP 8.x, Laravel 11.x |
| **Frontend** | Blade + Livewire (or Vue.js/Inertia.js) |
| **Database** | MySQL 8.x |
| **Web Server** | NGINX |
| **Queue/Jobs** | Laravel Queues (Redis or database driver) |
| **File Storage** | Local / AWS S3 (resumes, documents) |
| **Email** | SMTP (Mailgun / SendGrid / SES) |
| **Search** | Laravel Scout + Meilisearch (for talent pool search) |
| **Caching** | Redis |
| **Deployment** | VPS (DigitalOcean / AWS EC2) or Laravel Forge |

---

## 6. MVP Scope (Phase 1)

The Minimum Viable Product focuses on delivering the core evaluation loop and talent pool:

1. **Auth & RBAC** — Registration, login, roles (Admin, Recruiter, Interviewer, Candidate)
2. **Company Setup** — Company registration, team invites
3. **Job Management** — Create/publish jobs with custom application forms
4. **Pipeline Engine** — Configurable multi-stage pipeline with candidate movement
5. **Interview Scheduling** — Basic scheduling with email notifications
6. **Scorecard System** — Template builder, multi-interviewer scoring, aggregated results
7. **Talent Pool** — Auto-curation of qualified candidates, searchable marketplace for registered companies
8. **Notifications** — Email + in-app for key events
9. **Dashboards** — Basic recruiter and company dashboards

### Phase 2 (Post-MVP)
- Advanced analytics and reporting
- Calendar integrations (Google/Outlook)
- Resume parsing
- AI-assisted candidate matching/ranking
- API access for third-party integrations
- Subscription billing (Stripe)
- Mobile app (candidate-facing)
- Video interview integration

---

## 7. Revenue Model 

| Model | Description |
|---|---|
| **Freemium** | Free tier for small teams (limited jobs, limited pipeline stages) |
| **Subscription (SaaS)** | Monthly/annual plans tiered by: number of active jobs, team size, access to talent pool |
| **Talent Pool Access Fee** | Companies pay a premium to browse and contact pre-evaluated candidates |
| **Pay-per-Hire** | Commission or flat fee when a company hires through the talent pool marketplace |
| **Enterprise** | Custom pricing for large organizations with dedicated support |

---

## 8. Key Differentiators

- **Evaluation-First Approach:** Unlike job boards or ATS tools, the platform's core is structured, scorecard-based evaluation — not just tracking.
- **Reusable Candidate Data:** A candidate evaluated once can be matched to multiple companies, reducing redundant screening.
- **Talent Marketplace:** Bridges the gap between recruitment agencies and job boards by offering a pool of pre-vetted, interview-ready candidates.
- **Configurable Pipelines:** Every company can tailor its hiring workflow without developer involvement.
- **Transparent Hiring:** Standardized scorecards reduce bias and create auditable, data-driven hiring decisions.
