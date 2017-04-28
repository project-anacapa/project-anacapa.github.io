
# project 709

repo should have this.

NOTE: Missing from the /p/{project_id}/info json seem to be the following things:
* The lists of build, execution and expected files
* The point values for each test case

COMPLICATIONS:
* Filenames in the unix commands might need to be altered to have path names that reflect the new structure of the anacapa repo.


```
.anacapa/assignment_spec.json
.anacapa/build_data/.keep
.anacapa/test_data/.keep
.anacapa/test_data/interpreter-tests.zip
.anacapa/test_data/build-tests.xml
.anacapa/test_data/ant-redacted.sh
.anacapa/expected_outputs/.keep
```


```json
{
  // the assignment name, i.e. lab00 or lab01 -- should match up to repo name
  "assignment_name": "cs56_f16_lab06",
  // maximum number of students per group
  "maximum_group_size": 2,
  // whether the assignment is available for students to start/submit
  "ready": false,
  // due date for assignment (any submissions after this time will be flagged)
  "deadline": null,
  // what the students will submit/what will be in their repo
  "expected_files": [
    "lab06.zip"
  ], // [] for any deliverable
  // files that will remain read-only to students, but available in their repo
  "uneditables": [
  
  ],
  // test cases and grading information
  "testables": [{
      "test_name": "JUnit Tests",
      "build_command": "",
      "test_cases": [{
          "command": "./hello",
          "points": 100,
          "kind": "diff",
          "hide_expected": true,
          "diff_source": "stdout",
          "expected": "generate", // or ".anacapa/expected_outputs/my_file.txt",
          "timeout": 4
      },
      {
      
      diff-test-01: {
stdin: null,
args: "sh ant-redacted.sh -f build-tests.xml diff-test-01",
output_filename: null,
source: "stdout",
expected: "5df6ed3ed7c51f1a92f2595789e537ed073dfcd3",
output_type: "diff",
id: 9117
},
      
      
      
          "command": "sh .anacapa/test_data/ant-redacted.sh -f .anacapa/test_data/build-tests.xml diff-test-01",
          "points": 100,
          "kind": "diff",
          "hide_expected": true,
          "diff_source": "stdout",
          "expected": "generate", // or ".anacapa/expected_outputs/my_file.txt",
          "timeout": 4
      }
      
      
      
      ]
  }],
  "artifacts": [{
    "name": "TODO?"
  }]
}
```
