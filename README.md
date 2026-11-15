# CampusFlow — Academic Management ERP

CampusFlow is a role-based college academic management application for Super Admin, Faculty and Student workspaces. It uses Next.js Pages Router, React, TypeScript and a local JSON data store for local demonstration.

## Main modules

### Super Admin
- Dashboard, branch, academic-year, semester and section management.
- Branch-wise subject and course management.
- Faculty and student profile management.
- Initial faculty/student login password creation and password resets.
- Subject assignments and timetable conflict checks.
- Attendance, internal marks, assignments, study materials and announcements.
- Academic reports and CSV export.
- Student account activation and deactivation.

### Faculty
- Assigned subject and class visibility.
- Student lists for assigned classes.
- Attendance marking and internal marks entry.
- Assignments, learning materials and class announcements.
- Assigned timetable and academic reports.
- Own password change from Profile.

### Student
- Own subject, attendance and internal mark records.
- Class timetable, assignments, materials and announcements.
- Own password change from Profile after signing in.

## Account and password workflow

1. Super Admin adds a faculty member or student.
2. Super Admin enters an initial login password in the same form.
3. The account is created using the entered email address as the username.
4. Super Admin securely communicates the initial credentials to the faculty member/student.
5. After signing in, the user can open Dashboard → Profile to change their password.
6. To reset a password, Super Admin edits the relevant faculty/student profile and enters a new password. Leave the password field blank to keep the current password.

Passwords are stored as salted scrypt hashes; plain-text passwords are never stored. Passwords must be at least 10 characters and include an uppercase letter, lowercase letter and number. Changing a password invalidates other active sessions for that account. No email provider, API key, SMTP or email configuration is required.

## Demo accounts

Development-only demo accounts are created automatically on the first login request when `NODE_ENV` is not `production`.

| Role | Email | Password |
|---|---|---|
| Super Admin | `admin@college.edu` | `Admin@123` |
| Faculty | `sarah.smith@college.edu` | `Faculty@123` |
| Student | `aarav.kumar@student.edu` | `Student@123` |

These credentials are for local testing only and must never be used in a public deployment.

## Run locally on Windows

Requirements: Node.js 20.9 or newer and npm.

```powershell
# Open the folder containing package.json
Copy-Item .env.example .env.local
npm install
npm run dev
```

Open `http://localhost:3000`. The `.env.local` file only needs a strong `AUTH_SECRET` for production-like deployment; no email API key is needed.

Useful checks:

```powershell
npm run validate:data
npm run typecheck
npm run lint
npm run build
```

## Project structure

```text
campusflow/
├── db.json
├── scripts/validate-data.mjs
├── src/
│   ├── components/
│   ├── lib/                 # Authentication, password hashing and JSON database
│   ├── pages/api/           # Academic resource and authentication APIs
│   ├── pages/dashboard/     # Academic modules and account settings
│   ├── pages/login.tsx
│   └── styles/globals.css
├── .env.example
├── package.json
└── tsconfig.json
```

## Data and deployment notes

`db.json` contains academic records, login accounts and audit logs. The JSON adapter is intended only for local development or a single-instance classroom demonstration. It is not safe for concurrent production writes, multiple app instances or serverless deployment. For a real college deployment, migrate the data layer to PostgreSQL/MySQL with transactions, apply database migrations, add backups and monitoring, use HTTPS, configure a unique `AUTH_SECRET` of at least 32 characters, and conduct security testing before launch.
