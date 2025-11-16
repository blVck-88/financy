# Loan Manager

A professional loan management system for managing borrowers, loan applications, and loan repayments.
Built with **React + Vite + TypeScript** on the frontend and **Supabase** (Postgres, Auth, RLS) on the backend.

---

## Features

### Dashboard

* Total borrowers
* Active loans
* Total disbursed
* Total collected

### Authentication

* Secure user sign-up/sign-in using Supabase Auth

### Borrowers

* Register borrowers
* Searchable borrower list

### Loans

* Create loans (principal, rate, term, frequency)
* Searchable loan list
* Loan detail view with full repayment schedule

### Repayments

* Record repayments on active loans

### Role-Based Security

* Supabase RLS ensures actions match assigned user roles

---

## Tech Stack

### Frontend

* React
* Vite
* TypeScript
* Tailwind CSS
* Shadcn/UI
* React Router
* TanStack Query

### Backend

* Supabase Postgres
* Supabase Auth
* Row Level Security (RLS)

### Other Tools

* Sonner (notifications)

---

## Local Setup

### 1. Requirements

* Node.js v18+
* npm or bun
* Supabase account

### 2. Clone

```bash
git clone <YOUR_GIT_REPOSITORY_URL>
cd financy-loan
```

### 3. Install

```bash
npm install
```

---

## Supabase Configuration

### Step 1: Create Supabase Project

Make a new project in the Supabase dashboard.

### Step 2: Retrieve API Keys

In the dashboard:
**Project Settings → API**
Copy:

* Project URL
* anon key

### Step 3: Apply Database Migration

1. Open **SQL Editor**
2. Open migration file:
   `supabase/migrations/20251114071132_dd21dc72-db6b-4405-80d8-73a604af5e85.sql`
3. Use the **corrected SQL** (not the original)
4. Run it

This sets up:

* Tables
* Functions
* Roles
* Triggers
* RLS policies

---

## Environment Variables

Create `.env` in the root:

```env
VITE_SUPABASE_URL=YOUR_PROJECT_URL
VITE_SUPABASE_PUBLISHABLE_KEY=YOUR_ANON_KEY
```

---

## Run Locally

```bash
npm run dev
```

Open the URL printed (default: `http://localhost:8080`).

---

## User Roles and RLS

Supabase RLS is enabled on all tables.

When a user signs up:

* A row is added to `public.profiles`
* No role is assigned automatically

A user cannot create borrowers/loans/repayments until assigned a role.

### Assign a Role

1. Log in to create the user
2. In Table Editor, open `profiles` and copy the ID
3. Open `user_roles` table
4. Insert:

   * `user_id`: copied ID
   * `role`: one of:

| Role           | Permission               |
| -------------- | ------------------------ |
| `admin`        | Full access              |
| `loan_officer` | Create borrowers & loans |
| `accountant`   | Record repayments        |
| `collector`    | Record repayments        |

---

## Deployment

### Lovable

* Open the project
* Share → Publish

### Vercel / Netlify

1. Push code to GitHub/GitLab
2. Create a project
3. Configuration:

   * Build: `npm run build`
   * Output: `dist`
4. Add environment variables:

   * `VITE_SUPABASE_URL`
   * `VITE_SUPABASE_PUBLISHABLE_KEY`

---

## Summary

This project provides:

* A modern, secure loan management workflow
* Full borrower → loan → repayment lifecycle
* Strong role-based access via Supabase RLS
* A clean development and deployment process

---
