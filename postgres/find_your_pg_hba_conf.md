# Find your pg_hba.conf file location

Enter psql and type `SHOW hba_file;`

Useful when you need to update permissions for local dev scenarios -- like not having to enter a password for your default user.
Specifically, used to set the permissions to `trust` instead of peer on local machine for development work.
Maybe this is a bad thing to do, though?
