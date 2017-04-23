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


## Feature: Assignments + Repos

__*INCOMPLETE FEATURE*__

This feature enables the instructor to manage assignment repositories in the connected organization.

Functionality includes:

- A new page to list all assignment and student repositories
- A page visible to students for each assignment repo (Repos with names that look like `assignment-<name>`)
  - For each assignment, a button that students can click that creates a repo for them in the organization called `<name>-<githubid>`,
    where `<name>` is the corresponding assignment name, and `<githubid>` is their github username. The characters `<` and `>` are not
    included.
- The option to specify a "starter code" repository that will be copied into students' generated assignment repositories.
    
## Feature: Student Group Assignments

__*INCOMPLETE FEATURE*__

Note that if this feature is enabled, the `Assignments + Repos` feature is required (and automatically enabled as well).

Functionality includes:

- The ability for students to select other students to create a group for a certain assignment.
  - In this case, the generated repo name for the assignment is `<name>-githubid1-githubid2`. The github usernames of the students in the
    group are joined by the `-` character in lexicographic order.


## Feature: Crash lists

__*INCOMPLETE FEATURE*__

TODO


## Autograding with Jenkins

__*INCOMPLETE FEATURE*__

Note that if this feature is enabled, the `Assignments + Repos` feature is required (and automatically enabled as well).
