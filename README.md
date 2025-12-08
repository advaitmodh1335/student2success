# Student2Success High-Fidelity Prototype

**Team:** T08 G05

**Run via localhost / a live server (e.g., VS Code “Live Server” / “livewire”).**
Opening files with `file://` can break charts, fonts, and modal behavior.


## Project Description
**Student2Success** is a multi-persona career portal prototype that demonstrates realistic end-to-end interactions for **Students**, **Employers**, and **Staff**. It balances **horizontal fidelity** (consistent navigation/components) with **vertical fidelity** (fully interactive flows, validations, modals). The stack is vanilla **HTML/CSS/JS** with **Chart.js** (CDN). Minimal state is kept in localStorage, no backend is required.


## Team Members

| Name | Email | UCID |
| :--- | :--- | :--- |
| **Advait Modh** | advaitamitkumar.modh@ucalgary.ca | 30202791 |
| **Jawad Naheen Shamim** | jawadnaheen.shamim@ucalgary.ca | 30210511 |
| **Maharsh Patel** | maharshyogeshkumar.p@ucalgary.ca | 30217402 |
| **Shashwat Tank** | shashwat.tank@ucalgary.ca | 30218865 |
| **Bryan Phan** | hoangbach.phan@ucalgary.ca | 30222218 |


## How to Run

**Use localhost or a live server (“livewire”).**
Internet connection is required for the Chart.js CDN.

### Option A - VS Code Live Server
1. Open the project root in **VS Code**.
2. Install the **Live Server** extension.
3. Right-click **`index.html`** → **Open with Live Server**.
4. Navigate to `http://127.0.0.1:5500/index.html` (or similar).

### Option B - Python 3

1. Direct to the project root
2. Run python3 -m http.server 5500 in terminal
3. Then open http://localhost:5500/index.html

### Option C - Direct Link made using FIREWALL
1. https://student2success-a235a.web.app

## What Was Implemented (Cases / Functions)

### Shared
* Consistent Topbar, Back strip, centered page headers, card/table components.
* Modal system with backdrop, Esc-to-close, focus return, and ARIA labels.
* Pill UI controls (status dropdowns and inline action pills).

### Student
* **Login page** with guidance text (“Login using your university credentials”).
* **Profile page:**
    * Save requires all fields filled (Full Name, Email, Program, Expected Graduation).
    * If anything is missing: a window pop-up appears.
    * Successful save shows a transient toast and persists to localStorage.
* **Documents:**
    * Upload modal (Document Type, File, Name).
    * Rename with illegal-character validation (`\ / : * ? " < > |` blocked).
    * Set Default (single-select across table).
    * Download uses a blue pill and blob URLs; Delete revokes blob URL and confirms.

### Employer
* **Post Job** form with segmented Job Type selector and confirmation modal.
* **Applicants table:**
    * Dynamic header/tagline from URL params (id/title/company/location).
    * Search + Filter by Status (Under Review / Interview / Approved / Rejected).
    * Status pill appearance changes with value.
    * Save changes shows a diff list; confirm/commit updates.
    * Row actions: View (details modal), Message (compose + preview), Download Resume (placeholder `.txt` + “download started” modal).

### Staff
* **Jobs Queue → Job Details:** Approve (success modal) or Decline (optional feedback; “Sending…” → “Sent ✓”).
* **Statistics:** three Chart.js graphs (Approvals by Day, Active Postings, Avg Time to Approve).


## What Data Should Be Entered

* **Student Login:** any non-empty email/password.
* **Profile:** enter all four fields before saving - Full Name, Email, Program, Expected Graduation.
    * If any field is empty, the error pop-up appears.
* **Documents:** choose a file; Name is optional (defaults to file name).
* **Post Job:** Title & Location recommended; Job Type selectable; Deadline free-form YYYY-MM-DD.
* **Applicants:** change statuses, then use Save changes to commit diffs.
* **Decline (Staff):** feedback optional; shows “Sending…” then “Sent ✓”.



## Walkthrough

Start from `index.html` and pick a role.

### 1) Student Flow

#### Login - `student/login.html`
* Email: `student@university.edu`
* Password: `password`
* Click **Login**.

#### Profile Validation - `student/profile.html`
* Click **Save changes** immediately → a pop-up says fields are missing.
* Fill all fields exactly:
    * Full Name: `Alex Student`
    * Email: `alex.student@ucalgary.ca`
    * Program: `BSc Computer Science`
    * Expected Graduation: `2027`
* Click **Save changes** → a toast “Profile saved” appears.

#### Documents - `student/documents.html`
* Click **New Upload** → Document Type: `Resume`.
* **Browse files…** select any `Resume.pdf`; Name: `Resume v2` (or leave blank).
* Click **Upload** → confirmation → **Done**.
* In the table:
    * **Rename** → type `Resume Fall` → **Save** (blocks illegal characters).
    * **Set Default** (row shows “Default ✓”, others clear).
    * **Download** (blue pill) → browser downloads the blob.
    * **Delete** → confirm; file removed and the blob URL is revoked.

### 2) Employer Flow

#### Post a Job - `employer/post-job.html`
* Title: `Software Developer Intern`
* Location: `Remote`
* Compensation: `$25/hr`
* Job Type: `Internship`
* Description/Requirements: any text
* Click **Submit** → confirmation modal appears.

#### Applicants - `employer/applicants.html`
* In **Search**, type `Maya`; in **Filter**, choose `Interview`.
* Change statuses (e.g., Alex → Interview, Ethan → Rejected).
* Click **Save changes** → confirm list → **Save**.
* Try row actions: **View**, **Message** (type `Thanks for applying!` → **Send**), **Download Resume**.

### 3) Staff Flow

#### Queue -> Details - `staff/jobs.html` → click Review
* On `staff/job-details.html?`, click **Approve** (success modal), or
* Click **Decline**, type feedback, click **Send feedback** (shows Sending… → Sent ✓).

#### Statistics - `staff/statistics.html`
* Hover the charts for tooltips (Approvals by Day, Active Postings, Avg Time to Approve).



## Known Limitations

* No real authentication/server; profile data stored in localStorage.
* Employer resume downloads are placeholder `.txt`.
* Requires internet for Chart.js CDN.


## AI Disclosure

 Some Part of this code were generated by Chat GPT