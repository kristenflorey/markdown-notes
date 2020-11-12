# SQL
#### Structured Query Language
  - SQL is a *declarative* programming language that works on *sets* of records.
  - Primary way to interact with databases.    
- A **Relational Database Management System** is a software application used to store, modify, and retrieve data for programs.
- A single running RDBMS can have hundreds of databases that it manages.

#### <lightblue> PostgreSQL </lightblue>
- **PostgreSQL is an open-source RDBMS that allows for interactive querying.**
- PostgreSQL can be interacted with directly from the command line using `psql` or from a GUI like **Postbird**

##### Connect to PostgreSQL from the Command Line using `psql`

---
### SQL Commands
#### User Management
  - Usernames should not contain spaces or dashes
  - They should only contain lower case letters, numbers, and underscores.
    - Good: `kristen_florey123`
    - Bad: `kristen-florey.user`
##### Creating Users
```
CREATE USER «name» WITH «option»;
```
  - define a new database role
  - A role is an entity that can own database objects and have database priveleges:
    - a role can be considered a 'user', a 'group', or both.
  - same command as `CREATE ROLE`, but with `CREATE USER` login is assumed by default

- **name**: the name of the new role
- **options**:
```
  SUPERUSER | NOSUPERUSER
  INHERIT | NOINHERIT
  LOGIN | NOLOGIN
  PASSWORD 'password' | PASSWORD NULL
  VALID UNTIL 'timestamp'
  IN ROLE role_name [, ...]
  IN GROUP role_name [, ...]
```
[Detailed List of Options](https://www.postgresql.org/docs/13/sql-createrole.html)

---
##### Deleting Users
```
DROP ROLE [IF EXISTS] «name»;
```
- removes the specified role(s).
-  `IF EXISTS` will prevent error if role does not exist.
- a role cannot be removed if it is still referenced in any database of the cluster; an error will be thrown.
- Before dropping the role, you must drop all objects it owns (or reassign their ownership)
  - see [`DROP OWNED`](https://www.postgresql.org/docs/13/sql-drop-owned.html) or [`REASSIGN OWNED`](https://www.postgresql.org/docs/13/sql-reassign-owned.html)

---
##### Setting Roles
```
SET [SESSION | LOCAL] ROLE «role_name»
```
```
RESET ROLE
```
- sets the current user indentifier to the current SQL session to be **«role_name»**
  - the specified **«role_name»** must be a role that the current session user is a member of
- `RESET ROLE` resets the current user identifier to be the current session user identifier.

#### Database Management

##### Creating a Database
```
CREATE DATABASE
```
