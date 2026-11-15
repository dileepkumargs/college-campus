# CampusFlow — Current Project Package

This package includes the CampusFlow academic management modules and the current account/password workflow.

## Account workflow
- Super Admin creates a student or faculty profile and sets its initial login password in the same form.
- The registered email address is the login username.
- Super Admin can reset the password by editing the profile and entering a new password.
- Students and faculty can change their own passwords after signing in from Dashboard → Profile.
- No email service or API key is required. Super Admin securely provides the initial credentials to the user.

Passwords are stored as salted scrypt hashes. Password changes increment the session version so existing sessions are invalidated. Administrative password changes are recorded in audit logs.

This is a local demonstration using `db.json`, not a production-ready college deployment. Configure a strong `AUTH_SECRET` and migrate to a transactional SQL database before production.
