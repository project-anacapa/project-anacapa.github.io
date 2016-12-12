
As a project manager I have a github organization.

In that github org, I have:

* List of developers
* Groups of individual developers to these repos
* Track the issues that they are working on, or should be working on.


# Phill's user stories

* As an instructor, I associate a github organization with my course.
* As an instructor, I upload a course roster to the tool.

* As an instructor, I establish a list of instructional staff (this might be done through a "group" in the organization, or by making "owners" in the organization, or something else.)

* As an instructor, I can set up starter code for assignments.

* As a student, I establish the link between my github account and my identity as part of the course. (This has the side effect of setting up whatever permissions, organization memberships, webhooks, etc. are appropriate for my participation in the course.)

* As a student, I can create a private or public repo that automatically has the right starter code, permissions, etc. for the assignment---either the manual way, or automatically.

* As an instructor, I can see a dashboard for the assignment, that shows which students have created a repo that matches the proper naming convention, permissions, etc., how many commits they have done, if we have autograding hooked up to the repo, how many submissions they have made, etc.
    * That is, it is a much more full featured version of the pie chart that is currently in submit.cs

# MVP Above this line


* As an instructor, I can establish a grading rubric for the NON-autograded parts of an assignment, complete with the rubric, and the number of points that each part is worth.  (In MVP rubric is just a single line of text plus number of points.  In later version, rubric is more full featured, similar to the kinds of features available in Gradescope.com.)


* As a grader, I can see a list of all submission for an assignment that are available for grading, and can assess each one based on the rubric.   Ideally, this will be a very small shim over the top of the existing github UI.. that is, we make use of github UI elements where possible.  For example, entering grading info might involve filling in a labxx_feedback.md file that has been pre-filled with a template, the syntax of which allows easy parsing, perhaps in yml format rather than md)

* As a grader, I can quickly see whether the template that has been entered is, or is not, accepted by the parser, and whether my intended grade did, or did not get entered properly.  (e.g. there is a dashboard, spreadhseet, etc. that highlights the non-compliant entries.)

* As a grader, I can enter feedback in a assignment level feedback repo that is the "master" copy.  That is NOT yet provided to the student.   Instead, it is available to instructional staff.  Only after the instructor clicks "approve all" or "approve specific one" or manually changes the yml to say approved, or something---does it get sent to the student, and the grade is available to the student.

* As a student, one grading for an assignment is complete and the narrative feedback has been approved by the instructor, I can see the narrative feedback in a FEEDBACK repo that I have read only access to.  

* As a student, I can see a complete view of all grades in this system that have been released to students.

* As a student, I can submit a grading issue about any item from my feedback repository in case there is
(can we do this with "github issues"?  Are issues in a private repo private?  Would this be a feasible mechanism for grading issues?")


* As a grader, I can create "issues" on an assignment, along with point values.

* As a student, I can close "issues" for an assignment in order to earn points (or earn back some fraction of points that were deducted.)

* As a grader, i can review "issues". 



# TODO

* Try setting up Jenkins workers on submit0 and submit1 as a proof of concept.

* Try setting up Jenkins master/server on Heroku as a proof of concept.

* Meet with Bryce to get the tool that allows you to set up a programming assignment by editing a file rather than by pointing and clicking.
    * Corollary: get some Python code to dump the contents of the database tables that store the programming assignments.
    * From that, develop a tool that converts those into some JSON format of our devising, perhaps based on the JSON format already in Hunter's spike of anacapa-grader.


* Make some version of some tool for manipulating submit.cs assignments available to current submit.cs users, whether that be directly Bryce's tool, or something of our construction.

    * This might be a tool where authentication is via github.
    * It might be done via convention over configuration.
  

# submit.cs assignment editing interim step

* Imagine a submit_cs_assignments organization.
* The organization contains one private repo for each submit.cs course.
* The owner of the submit_cs_assignment organization is also the administrator of submit_cs
* When you create a submit_cs course, say, CS16_w17, you find out the github ids of all of the 
    instructional staff of CS16_w17, i.e. the submit.cs administrators, and you give them
    read/write access to the github repo called CS16_w17 within submit_cs_assignments
* Inside that repo, there is a directory called assignments
* Inside the /assignments directory, this is one directory per programming assignment.
* Any time you do a git push on the repo, each of those programming assignments is parsed, and
    the corresponding assignment in submit.cs is updated if there are any changes to it, AND if
    the syntax is valid.
* There is also a /logs subdirectory.  The tool will write into that /logs subdirectory
    the result of the latest update, including any errors that occurred.



* SEE: https://github.com/carlos-jenkins/python-github-webhooks
