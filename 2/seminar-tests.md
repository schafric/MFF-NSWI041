# Test cases for the `Surveys` module

## Teacher creates a survey for his subject

### 01, non-existing subject

**Setup**

`Teacher` is logged in and authenticated.

**Steps**

- `Teacher` opens a form for creating new survey by pressing `New survey` button.
- `Teacher` fills in metadata for a non-existing subject identified by unique `id` and time span. Example of malformed triple is `Teacher, XXXX, 12:00:00 12:45:00`, where the subject identifier does not follow naming convention.
- `Teacher` requests for a new survey by pushing the button `Confirm`.
- `Teacher` sees data are accepted and send to the service.
- After a negligible time span, `teacher` is informed about unsuccessful attempt via popup window with the reason of the refusal.

### 02, missing permissions

**Setup**

- Permission to create surveys is removed from the `teacher` user before the test.
- `Teacher` is logged in and authenticated.

**Steps**

- `Teacher` searches for existing subject identity in the `Search module`.
- `Teacher` requests creation of the new survey with `New survey` and identity.
- `Teacher` is informed about unsuccessful attempt via popup with the reason.

### 03, missing survey data

**Setup**

- `Teacher` is logged in, authenticated and has permissions to create surveys. Permissions are checked in the specific module.

**Steps**

- `Teacher` requests new survey with existing subject identity.
- `Teacher` is redirected to the new survey form.
- `Teacher` fills in survey parameters, such as purpose, time span, etc. and does not fill in title parameter.
- `Teacher` confirms that the survey parameters are finalized by pressing the button `Confirm`.
- `Teacher` is notified about missing title via popup.

### 04, teacher creates new survey

**Setup**

- `Teacher` is logged in, authenticated and has permissions to create surveys.

**Steps**

- `Teacher` fills in valid subject identity (a triple) and presses the button `New survey`.
- New survey form opens.
- `Teacher` enters valid survey parameters (title, etc.).
- `Teacher` confirms that survey is finalized by pressing `Confirm` button.
- `Teacher` is notified via popup about successful attempt.
- `Teacher` is proposed to create new survey.
