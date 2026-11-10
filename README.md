# Stock
### A OneDrive, ICloud, GoogleDrive clone. Personal file cloud.

My attempt at making a complete clone of onedrive, obviously without the slop, and also without AI including Google search AI because its ass and I'm not paying for AI to make me trash.

**Architecture:**

---
**APP PROCESS:** - app's overall logic
> START
1. GET Database (if fail: don't continue, wait for connection)
    - contains hashes of all files in monitored directories
2. compare database to files on pc
3. upload new or edited files
    - POST edited files for backup and version control 
4. archive requested or old files (archived files are defined in hash database)
    - archived files on the pc are replaced with empty dummy files as shortcuts to download real file from server
5. update hashes and POST database to server (PUT if no database version control)
> QUIT
1. GET Database (if fail: just stop process)
2. if success continue normal start process then stop process

---
**BACKGROUND SERVICE:** - watches selected directories for changes
> DETECTED CHANGE
==I don't really know how to do this yet==
1. Run START process

---
**FRONTEND APP:** - exposes process settings
> GUI
- server selection
- server version control
    - database versions
    - file versions
- update intervals
- archive preferences
    - age based archiving (age is stored until the file is archived then it is disregarded)
    - specific file archiving

---
**SERVER API:**
> GET
1. database of hashes (requested version)
    - keeps user defined amount of versions
2. specified file
> POST
1. new file
2. edited files
    - previous versions are kept in the same directory just marked with a prefix of its version (.#)
3. updated database (with version control)
> PUT
1. edited file (no version control)
2. updated database (no version control)
> DELETE
1. archive file (.archive)
2. revert database 
