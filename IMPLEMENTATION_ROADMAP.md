# CampusFlow Implementation Roadmap

## Current included modules
- Super Admin, Faculty and Student dashboards with role-based API access.
- Branch, academic year, semester, section, student, faculty and subject management.
- Branch-wise course/subject assignments and timetable conflict validation.
- Attendance, internal marks, assignments, study materials and announcements.
- Academic summary reports and CSV export.
- Student and faculty login accounts with administrator-managed initial passwords.
- Profile-based password changes for signed-in users.

## Account and password workflow
- Super Admin enters the initial password while creating a student or faculty profile.
- Super Admin can reset a password by editing the profile.
- Students and faculty can change their own passwords after login.
- Passwords are stored as salted scrypt hashes; changing a password invalidates existing sessions.
- No email API key or email service is required.

## Production work still recommended
- Migrate `db.json` to PostgreSQL or MySQL with transactional operations.
- Add automated tests, backups, monitoring, HTTPS and production secret management.
- Review role permissions and conduct a security assessment before deployment.
