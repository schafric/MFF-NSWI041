# Test cases for the `Surveys` module

## Teacher creates a survey for his subject

### 01, non-existing subject

**Setup**

The `teacher` is logged in and authenticated.

**Steps**

- The `teacher` opens a form for creating new survey.
- The `teacher` fills in metadata for a non-existing subject identified by unique `id` and time span.
- The `teacher` requests for a new survey by pushing the button.
- The `Surveys module` receives request data formatted as a `JSON`.
  - Assertion: `JSON` validity is checked.
  - Assertion: `JSON` is validated against `JSON Schema`.
- The `Surveys module` checks whether the triple `(teacher, subject id, time span)` exists in the `central schedule`.
  - `central schedule` responses negative.
- The `Surveys module` logs the unsuccessful attempt in the database.
- The `Surveys module` generates negative response to the teacher.
- The `teacher` is informed about unsuccessful attempt in the message box.

### 02, wrong permissions

**Setup**

- The `teacher` is logged in and authenticated.
- The `teacher` has requested existing subject, which has been confirmed by the `Surveys module`.

**Steps**

- The `Surveys module` requests authentication and administration subsystem to check whether `teacher` could create surveys.
- The subsystem responses negatively.
- The `Surveys module` logs the unsuccessful attempt in the database.
- The `Surveys module` generates negative response to the teacher.
- The `teacher` is informed about unsuccessful attempt in the message box.

### 03, fill in invalid survey data

**Setup**

- The `teacher` is logged in, authenticated and has permissions to create surveys.
- The `Surveys module` validated request successfully.

**Steps**

- The `teacher` is redirected to the new survey form.
- The `teacher` fills in survey parameters such as title, purpose, time span, etc.
- The `teacher` confirms that survey is finalized.
- The `Surveys module` receives survey data serialized into `JSON`.
- The `Surveys module` validates `JSON` against `JSON Schema`.
- The `Surveys module` deserialize data into a structure, verifies the content, and detects invalid parameters.
- The `Surveys module` send a message to the `teacher` regarding wrong parameters.
- The `teacher` is notified via message box and is able to correct the survey data.

### 04, teacher creates new survey

**Setup**

- The `teacher` is logged in, authenticated and has permissions to create surveys.
- The `Surveys module` validated request successfully.

**Steps**

- The `teacher` fills in valid survey parameters.
- The `teacher` confirms that survey is finalized.
- The `Surveys module` receives survey data serialized into `JSON`, deserialize them and verify.
- The `Surveys module` request `database` with survey parameters.
- The `database` response positively, the survey is created.
- The `Surveys module` generate a positive message to the `teacher`.
- The `teacher` is notified via message box.
- The `teacher` is able to create new survey.
