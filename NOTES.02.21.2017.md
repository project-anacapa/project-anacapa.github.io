
Jenkins
=======

Workers are called "nodes".

The "grade_gen" is a pipeline.  It should be called something like "Install Anacapa".

We click "Build Now" to activate a pipeline (i.e. "run" it.)

Creating a new node for csil-submit2.cs.ucsb.edu
================================================

* Choose "permanent agent"  (vs. copy existing node)
* Create a directory on the remote host for jenkins to work in
* Design decision: one jenkins node will correspond to exactly one submit-cs user (e.g.submit0, submit1,etc.) and one submit.cs worker host, e.g. csil-submit0.cs.ucsb.edu, csil-submit1.cs.ucsb.edu, etc)
* Reason: we need the processes to NOT have access to each other's stuff (difference between conventional use cases for Jenkins vs. academic use case.)

Notes for Nick's Thesis Report
===============================

* Highlight: list of differences between the "conventional use of Jenkins" and "Academic auto-grading use of Jenkins", and what that requires in the way of design decisions.

