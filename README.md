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

## How It Works

```text
Candidate Application
        ↓
Select Job + Upload CV
        ↓
Extract CV Text
        ↓
Fetch Job Requirements
        ↓
AI Agent: Analyze + Score + Summarize
        ↓
Save Results to Supabase
        ↓
Apply Qualification Criteria
        ↓
   ┌───────────────┴───────────────┐
   ↓                               ↓
Qualified                    Not Qualified
   ↓                               ↓
ClickUp Task                  Rejection Email
   ↓                               ↓
HR Email Notification        Update Candidate Status
   ↓
HR Decision
