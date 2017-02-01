# Jenkins Semantics

Workflow to get auto-grading set up

1. Install GitHub Organization Plugin and Anacapa Grader Jenkins Plugin with Jenkins
1. Set up Jenkins to point to the course github org via GitHub Organization Plugin
1. create **private** assignment spec repo called `assignment-LABNAME` containing the following:
    * assignment_spec.json (described later)
    * Jenkinsfile
        - TODO: What will this look like???
          - Maybe this will be the official Jenkinsfile that knows that this is the
            assignment spec repo (by looking at the name and recognizing that it is
            `assignment-LABNAME`) and treats it differently than the student code
          - When student submissions get graded, they pull in this Jenkinsfile?
    * test_data/ folder
        - contains information that will be copied to student repos when grading so
          that grading scripts can access them as necessary (still hidden from students)
        - Equivalent for legacy submit is the "Execution Files"
    * expected_outputs/ folder
        - TODO: Describe
    * ...completed assignment files to use as reference implementation
1. When `assignment-LABNAME` is created, a build starts that generates the output
   artifacts as necessary for grading/diffing. Verify that this build succeeds.
1. create starter code repo called `starter-LABNAME` containing the following:
    * Jenkinsfile (empty)
        - XXX: Or perhaps we can provide some sort of DSL directive like `submit 'LABNAME'`
        - This needs to be here so that Jenkins can know that it should process the repo
    * ...starter code files
1. when student checks out the assignment, they get a new repo called `LABNAME-githubid`
   where `githubid` is their GitHub username. If the student is in a group/pair, that
   repo would be named `LABNAME-githubid1-githubid2`, where `githubid1` and `githubid2`
   appear in lexicographic order.
   * This repo contains a copy of whatever was in `starter-LABNAME`
1. Whenever the student pushes code to their repo, a Jenkins build starts that goes and
   fetches the information from `assignment-LABNAME` (i.e. tests, due date, deliverables,
   and other metadata) and runs code to compute the grade.
   * If any of the commits contain changes to any of the files listed in
     `uneditables` from the assignment spec, those changes are reverted and
     the file is changed to be whatever is in `starter-LABNAME`
   * The `test_data` folder is copied over from the `assignment-LABNAME` repo
   * Code to run is determined by the `testables` field of the `assignment_spec.json`
   * When complete, grade results are output in (json|yaml) via format below
        - as Jenkins Artifact?
        - POST'd to web application?
        - placed in new repo? e.g. `results-LABNAME-githubid`
        - placed as file in global results repo? e.g. `results-LABNAME`
            - file = `LABNAME-githubid-latest.json`
            - for multiple submissions, `LABNAME-githubid-fa65bge.json`
                - where `fa65bge` is the abbreviated commit hash
            - OR `LABNAME-githubid-[1-N].json`


Questions
- What happens when a student pushes code to an overdue project?
- Should we stop building things that pass some threshold over the due date?
  - does this matter?
- Who are the users and roles within Jenkins and how do we control access to artifacts that should be private to individual {student, instructor}?
- Are the users in Jenkins individual people or "machine accounts"?

TODO: Determine permissions and access restrictions for Jenkins views/tools

### Assignment Spec Format
```javascript
{
  // the assignment name, i.e. lab00 or lab01 -- should match up to repo name
  "assignment_name": "lab00",
  // maximum number of students per group
  "maximum_group_size": 1,
  // whether the assignment is available for students to start/submit
  "ready": true,
  // due date for assignment (any submissions after this time will be flagged)
  "deadline": "2017-01-13 23:59:00-08:00",
  // what the students will submit/what will be in their repo
  "expected_files": [
    "hello.cpp"
  ], // [] for any deliverable
  // files that will remain read-only to students, but available in their repo
  "uneditables": [
    "Jenkinsfile",
    "Makefile",
    "src/main/java/edu/ucsb/cs/cs56/Parser.java",
    "**/*.h",
    "*.h"
  ],
  // test cases and grading information
  "testables": [{
      "test_name": "Hello World",
      "build_command": "g++ -o hello hello.cpp",
      "test_cases": [{
          "command": "./hello",
          "points": 100,
          "kind": "diff",
          "hide_expected": true,
          "diff_source": "stdout",
          "timeout": 4
      }]
  }],
  "artifacts": [{
    "name": "TODO?"
  }]
}
```

XXX: Should we provide an "artifacts" option in the assignment spec so that instructors
     can pre-generate materials for manual grading?
  * Use case: image generation
  * Use case: interactive UI
  * If we do this, we can write a utility to fetch all the artifacts and provide a
    link to download them all in an archive file (.zip , .tar.gz , etc)

#### Test Case Types

* Diff

  ```json
  {
    "command": "./hello",
    "points": 100,
    "kind": "diff",
    "hide_expected": true,
    "diff_source": "output.txt",
    "timeout": 5
  }
  ```
  * Either specify expected output (in new expected_outputs/ folder?) or generate from reference solution
* Script

  ```json
  {
    "command": "./test_data/grader hello",
    "points": 100,
    "kind": "script",
    "timeout": 5
  }
  ```
  * Your grading script should print to `stdout` the grade in the following json format:
  
    ```json
    {
      "score": 75.2,
      "max_score": 100,
      "comments": ""
    }
    ```
  * Don't worry if your "max_score" is different from what you entered in the
    "points" field of the test case. The percentage will be calculated given the
    output of your script and the same percentage will be applied to calculate
    the test case score in terms of the given "points" value.
* Unit Tests (Not Available Yet) - JUnit, CxxUnit, unittest, pytest, etc
  - TODO: Describe


### TestResults output format (json or yaml)

```javascript
{
   "assignment_name": "lab00",
   "repo_name": "ucsb-cs16-wi17/lab00-githubid",
   "results": [{
      "test_group": "Hello World",
      "test_name": "./hello",
      "score": 100,
      "max_score": 100,
      "output": ""
   }]
}
```
