## Use case: Teacher views detailed results of surveys he made

### Test case 1: Request is invalid.
---
**Setup**:
  - You are logged in as teacher user with username: test-teacher.
  - Teacher you are signed in as is able to request detailed results of a survey.
**Steps**:
  - Request results of a survey which does not exists.
  - Open the response.
    - [Assertion]: Status code should be 400 (invalid request).
    - [Assertion]: There are no data in the response body.

### Test case 2: Teachers does no have permissons.
---
**Setup**:
  - You are logged in as teacher user with username: test-teacher.
  - test-teacher you are signed in as is able to request detailed results of a survey.
  - There is a active survey to some subject, which was created by another teacher (your teacher lacks permissons to open it)
**Steps**:
  - Request results of a survey from setup.
    - [Assertion]: Status code should be 401 (unauthorized).
    - [Assertion]: There are no data in the response body.

### Test case 3: Success scenario
---
**Setup**:
  - You are logged in as teacher user with username: test-teacher.
  - test-teacher you are signed in as is able to request detailed results of a survey.
  - test-teacher has active survey to test-subject.
**Steps**:
  - Request results of a survey from setup.
    - [Assertion]: Status code should be 200 (success).
  - You should see a page with results of the survey.
    - [Assertion]: Name of subject this survey belongs to is test-subject.
    - [Assertion]: You can see calculated statistical indicators.

## Use case: Teacher creates a survey for his subject

### Test case 1: Non-existing subject
---

**Setup**

You are logged in and authenticated as `Teacher` user with username `test-teacher`

**Steps**

- Open a form for creating new survey by pressing `New survey` button.
- Fills in metadata for a non-existing subject identified by unique `id` and time span. Example of malformed triple is `Teacher, XXXX, 12:00:00 12:45:00`, where the subject identifier does not follow naming convention.
- Request a new survey by pushing the button `Confirm`.
- [Assertion]: You should see, that data are accepted and send to the service.
- [Assertion]: After a negligible time span, you are informed about unsuccessful attempt via popup window with the reason of the refusal.

### Test case 2:  Missing permissions
---

**Setup**

- Permission to create surveys is removed from the `test-teacher` user before the test.
- You are logged in and authenticated as a teacher with username `test-teacher`.

**Steps**

- Search for existing subject identity in the `Search module`.
- Request creation of the new survey with `New survey` and identity.
- [Assertion]: You should be informed about unsuccessful attempt via popup with the reason.

### Test case 3: Missing survey data
---

**Setup**

- You are logged in as teacher with username `test-teacher`, authenticated and `test-teacher` has permissions to create surveys. Permissions are checked in the specific module.

**Steps**

- Request new survey with existing subject identity.
- [Assertion]: You are redirected to the new survey form.
- Fill in survey parameters, such as purpose, time span, etc., but do not fill in title parameter.
- Confirm that the survey parameters are finalized by pressing the button `Confirm`.
- [Assertion]: You are notified about missing title via popup.

### Test case 4: Teacher creates new survey
---

**Setup**

- You are logged in as teacher with username `test-teacher`, authenticated and `test-teacher` has permissions to create surveys.

**Steps**

- Fills in valid subject identity (a triple) and presses the button `New survey`.
- [Assertion]: New survey form opens.
- Fill in valid survey parameters (title, etc.).
- Confirm that survey is finalized by pressing `Confirm` button.
- [Assertion]: You are notified via popup about successful attempt.
- You are proposed to create new survey.
