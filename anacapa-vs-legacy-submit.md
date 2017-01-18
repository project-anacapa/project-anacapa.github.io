# Anacapa vs. Legacy Submit

# Advantages for Support

* Uses Jenkins for running grading scripts (vs. custom code)
    * Off-the shelf, yum installable/updatable, open source free commodity software
    * Professional level support, security updates
    * logrotate built in (not true of legacy submit)
    * far more features than legacy submit

# Advantages for Instructors

* Instructor (but not student) has full visibility into full logs of the testing runs
    * In legacy submit, those logs are visible to system admins only
    * Those logs could be selectively revealed (or not) to students based on assignment settings chosen by instructor
   
* Easier manipulation of assignments
    * Copying an assignment is simply copying a github repo---not a custom web app action 
    * Manipulating portions of assignments (test cases, etc.) is manipulating files and directories, not interacting with a thousand confusing mouse clicks on menus.  (easier for instructors, less code to maintain.)
   
# Advantages for Students

* Testing happens automatically as part of normal git workflow

