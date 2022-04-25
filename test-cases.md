# Use case: Teacher views detailed results of surveys he made

## Test case 1: Request is invalid.
#### Setup:
  - You are logged in as teacher user with username: test-teacher.
  - Teacher you are signed in as is able to request detailed results of a survey.
#### Steps:
  - Request results of a survey which does not exists.
  - Open the response.
    - [Assertion]: Status code should be 400 (invalid request).
    - [Assertion]: There are no data in the response body.

## Test case 2: Teachers does no have permissons.
#### Setup:
  - You are logged in as teacher user with username: test-teacher.
  - test-teacher you are signed in as is able to request detailed results of a survey.
  - There is a active survey to some subject, which was created by another teacher (your teacher lacks permissons to open it)
#### Steps:
  - Request results of a survey from setup.
    - [Assertion]: Status code should be 401 (unauthorized).
    - [Assertion]: There are no data in the response body.

## Test case 3: Success scenario
#### Setup:
  - You are logged in as teacher user with username: test-teacher.
  - test-teacher you are signed in as is able to request detailed results of a survey.
  - test-teacher has active survey to test-subject.
#### Steps:
  - Request results of a survey from setup.
    - [Assertion]: Status code should be 200 (success).
  - You should see a page with results of the survey.
    - [Assertion]: Name of subject this survey belongs to is test-subject.
    - [Assertion]: You can see calculated statistical indicators.

