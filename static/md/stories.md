# Github Organization Setup

First priority: creation of a minimum viable product tool to help instructors manage the signup for a github organization.

The user stories:

* As an instructor:
  * I can identify a github organization as the github organization for my course.
  * I can upload a course roster (in CSV format), and I can identify which of the various columns contains the first name, surname, and email address of the student.
  * I can see a list of my current course roster, and beside each name, I can see whether each student *has* or *has not* enrolled as part of the github organization.
  * I can access a text area containing the email addresses of all students that either did, or did not register yet, that I can "copy from" and then paste into the "bcc: " field of an email. Formatted as:
```
"Joe Schmoe" <jschmoe@umail.ucsb.edu>,
"Matt Damon" <mdamon@umail.ucsb.edu>,
"Jennifer Aniston" <jennifera@umail.ucsb.edu>,
```
* As a student:
  * I can login with my github id to a web app, and then one of two things happens: (a) if my email is in the course, I get added into the github organization and I get told that I was added into the github organization.  (b) if my email is NOT in the course, I get told: please check that your official school email is associated with your github id, and is a verified email.
