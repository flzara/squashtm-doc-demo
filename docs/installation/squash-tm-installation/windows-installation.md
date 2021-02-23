# Installation with Windows

!!! danger "Java support"
    From Squash TM 1.17, it is IMPERATIVE to use Java 8, Java 7 is not supported anymore.

## Installing Squash TM as a Windows service with universal package (.zip)

- Unzip the archive .zip and move the contents to the chosen location (i.e c:\<rep>).
  The Windows process associated to Squash TM must have reading and writing rights on Squash install location.
- Populate the database with SQL scripts located in: c:\<rep>\Squash-TM\databse-scripts
- Add the database connection information in startup.bat (to install a new database, see 2.05 - Install another database (recommended)):

```cmd
DB_URL="jdbc:mysql://localhost:3306/squashtm" or "jdbc:postgresql://localhost:5432/squashtm"
DB_TYPE="mysql" or "postgresql"
DB_USERNAME="squash-tm"
DB_PASSWORD="initial_pw"
```

- Install the service with:

```cmd
c:\Squash-TM\bin\squash-tm.exe install
```

!!! warning "Warning"
    Please note that the Windows installer (.jar) is for testing purpose only. It should not be used for production.
