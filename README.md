# Hiring-Assistant-for-HR-Recruiters

An innovative intelligent automation system specifically designed to help Human Resources (HR) professionals and companies overcome the traditional challenges of manually reviewing hundreds of resumes (CVs). The system handles application submissions, evaluates and filters candidates accurately based on specific job requirements and criteria, and sends detailed reports to the manager containing the top-qualified candidates to streamline the decision-making process for acceptance and scheduling interviews in the fastest and simplest way possible

## Business Overview

Reviewing hundreds of CVs manually is slow, inconsistent, and prone to human error. Strong candidates can be lost due to delayed responses, while candidate data becomes scattered across emails and files.

This project addresses these challenges by:

- **Cutting time-to-hire:** Every application is automatically analyzed, scored, and summarized.
- **Consistent evaluation:** Each CV is evaluated against the actual requirements of the targeted job, helping reduce inconsistency and unconscious bias.
- **Faster decisions:** The HR manager receives a candidate summary with **Accept / Schedule Interview** actions directly in the email.
- **One source of truth:** Candidate data and evaluation results are stored in a centralized database and organized by job.
- **Team collaboration:** ClickUp tasks allow multiple recruiters to track candidates and ensure that applications do not stall when one recruiter is unavailable.


---
![Job Application Flexible JD](image/Job-Application-Flexible-JD.png)
![New Qualified Candidate](image/New-Qualified-Candidate.png)

## How It Works

1. **Intake:** the candidate selects a job from a dropdown and uploads a CV through an n8n form.
2. **Parsing:** the PDF is converted to text.
3. **Job lookup:** the requirements of the selected job are fetched from Supabase, so nothing is hardcoded in the prompt.
4. **AI analysis:** the AI Agent (Cohere) extracts skills, education, experience, courses, languages, and links, then produces a numeric score and a short summary.
5. **Storage:** the result is saved in Supabase and linked to the job through `job_id`.
6. **Routing:** a Switch node applies the company criteria.
   - **Qualified:** a ClickUp task is created and an interactive email goes to the HR manager.
   - **Not qualified:** an automated rejection email is sent and the candidate's status is updated.

## Tech Stack

| Component | Role |
|---|---|
| n8n | Workflow orchestration and the application form |
| Cohere (`command-r-plus-08-2024`) | Language model behind the AI Agent |
| Supabase (PostgreSQL) | Job requirements and candidate applications |
| ClickUp | Recruitment task tracking for the HR team |
| Gmail | HR notifications and candidate rejection emails |

## Data Model

**`job_requirements`**: `id` (PK), `title`, `description`

**`User_job_applications`**: `id` (PK), `fname`, `email`, `score`, `summary`, `status`, `links`, `language`, `education`, `skills`, `courses`, `experience`, `job_id` (FK → `job_requirements.id`)

## Key Design Decisions

- **Dynamic job requirements:** requirements live in a database table and are injected into the prompt, so the same workflow serves any vacancy without editing the AI prompt.
- **Relational integrity:** every application carries a `job_id`, so candidates are always evaluated and reported against the right position.
- **Send vs. Send-and-Wait:** HR emails wait for a response (accept / reject buttons); candidate rejection emails send directly, so the workflow never hangs waiting on a candidate.

**Author:** Esraa Mahmoud
