Short explanation of key security measures:

Encryption of PII: AES_ENCRYPT / AES_DECRYPT used to store SSN encrypted at rest. (In production, prefer application-side authenticated encryption like AES-GCM, envelope encryption, or client-side encryption.)

Audit logging: audit_logs table + triggers + stored procedures insert audit events for visibility.

Least privilege DB users: app_user and app_admin created with restricted privileges — avoid using root for app operations.

Parameterized stored procedures: Using IN parameters prevents concatenating raw SQL in app → reduces SQL injection risk if procedures are used properly.

Public view that masks PII: v_clients_public prevents accidental exposure of plaintext SSN in normal queries.

Password hashing advice: Script reserves password_hash field; you should hash with bcrypt in the application (not with SHA256 in SQL).

Triggers log direct DML: If someone bypasses stored procedures and does direct INSERT/UPDATE/DELETE, triggers still create audit entries.
