# Project Exam App
Daml templates designed for a platform for proposing exam questions that can be revised, and the taking of such exams by students. They can be graded and be available to the parents to check.

### I. Overview 
This project was created by forking the [Daml Fundamentals Certification Sample App](https://github.com/DACH-NY/FundamentalsSampleApp) repository that was created using the `empty-skeleton` template. The project adopts and exemplifies the `proposal-accept` design pattern.  
A signatory can create a DraftExam contract. Then they or an assistant, controller party, can exercise a Revise choice to alter the exam's question.  
When the teacher chooses they can exercise the Publish choice, with the students list as parameter, to create an Exam template where the students are observers. A student can take the exam by exercising the TakeExam choice and creating an ExamInProgress template, where the teacher and student are signatories.   
The ExamInProgress student's answer can be rewritten with a Rewrite choice by the student and finally it can be graded by the teacher with the Grade choice, providing a final score, a note and the supervising parent. This creates a ExamGraded visible to the observer parent, and teacher and student as signatories.  
Additionally, a DraftExam contract can be removed by the teacher with the ScrapExam choice, and updated to a new school year with the BrandNewExam choice that increments the year on the DraftExam.  
The Exam contract can be taken back to the draft stage with the FixExam choice if there is things to change, or removed entirely with the Remove choice, with teacher as the controller.

### II. Workflow
1. A teacher creates a DraftExame contract. An assistant is invited as observer, both the manager and the assistant are authorized to exercise a Revise choice, to change the exam's question.
2. Upon the controller exercising Publish, it generates a Exam contract with the provided student list as an observer.
3. TakeExam choice can be exercised by a student in the students list, it creates a new ExamInProgress where the student can RewriteAnswer his answer to the exam's question.
4. The teacher can exercise the Grade choice on the ExamInProgress to finish the exam and create a ExamGraded contract with the student's parent as an observer. It has a decimal score from 0 to 100, a grade letter is calculated based on the score.  


### III. Challenge(s)
* The project was created by using `empty-skeleton` and the following was removed from `daml.yaml`:
```
sandbox-options:
   - --wall-clock-time
```
and replaced with the following:

```
exposed-modules:
  - Main
  - Test
navigator-options:
 - --feature-user-management=false
```

### IV. Building
To compile the project
```
$ daml build
```

### V. Testing
To test all scripts:
Either run the pre-written script in the `Test.daml` under /daml OR run:
```
$ daml test
```

### VI. Running
To load the project into the sandbox and start navigator:
```
$ daml start
```
