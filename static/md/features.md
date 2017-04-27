# Feature Levels for Anacapa

Below are a series of feature descriptions for [course-github-org-tool](https://github.com/project-anacapa/course-github-org-tool). Each
section describes what functionality is included (as well as the dependencies) with each feature.

## Baseline

This level is the minimum amount of functionality of the app. 

The __*baseline*__ functionality of the project includes:

- Connection to GitHub Organization
- Flexibility to choose between Git Providers (i.e. github.com, GitHub Enterprise, GitLab)
- Instructor privileges higher than student privileges
- Roster Upload
- Automatic organization membership invitations to GitHub users (who sign in to the app) with emails that appear on uploaded roster
- Roster Download (with GitHub Usernames)


## Feature: `Anacapa Repos`

__*INCOMPLETE FEATURE*__

If this feature is enabled, then the application will track all repositories that look like they correspond to Project Anacapa (i.e. they
follow the proper naming conventions). The types of repositories that this application knows about are as follows:

- Assignment Master repos, named `/^assignment-([\w\d\-_]+)$/i`, e.g. `assignment-lab01` or `assignment-merge-sort`.
  * this repository will contain your reference solution to the assignment, and should remain PRIVATE (not visible to students)
  * In addition to the reference solution, your assignment master repo should contain a single directory called `.anacapa/`, in which
    you will add your `assignment_spec.json` file. That file lets Anacapa know about how you want your assignment to be handled.
- Student code repos, named `/^labname-([\w\d\-_]+)$/i`, where `labname` corresponds to an existing assignment master repo in the course 
  organization, and the suffix is a `-`-delimited list of student github usernames in lexicographic order. e.g. `lab01-janedoe1` or 
  `merge-sort-defunkt-joegaucho`.

This feature enables the instructor to manage assignment repositories in the connected organization.

Functionality includes:

- A new page to list all assignment and student repositories
- A page visible to students for each assignment repo (Repos with names that look like `assignment-<name>`)
  - For each assignment, a button that students can click that creates a repo for them in the organization for that assignment with the 
    proper naming conventions as described above. It would be called `<name>-<githubid>`, where `<name>` is the corresponding assignment
    name, and `<githubid>` is their github username. The characters `<` and `>` are not included.
- The option to specify (in your `.anacapa/assignment_spec.json` file) the URL to a "starter code" repository that will be copied into 
  students' generated assignment repositories.
    
## Feature: Student Group Assignments

__*INCOMPLETE FEATURE*__

Note that if this feature is enabled, the `Anacapa Repos` feature is required (and automatically enabled as well).

Functionality includes:

- The ability for students to select other students to create a group for a certain assignment.
  - In this case, the generated repo name for the assignment is `<name>-githubid1-githubid2`. The github usernames of the students in the
    group are joined by the `-` character in lexicographic order.


## Feature: Crash lists

__*INCOMPLETE FEATURE*__

TODO


## Autograding with Jenkins

__*INCOMPLETE FEATURE*__

Note that if this feature is enabled, the `Anacapa Repos` feature is required (and automatically enabled as well).

Extra required configuration variables: `JENKINS_URL`.... TODO: ask @garethgeorge for his findings in this realm
