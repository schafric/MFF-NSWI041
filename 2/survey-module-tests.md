# Test cases for the `Survey` module

## Student fills in a survey


The person trying to log into the system is a student with valid login/password.



### 1. No survey is available

**Setup**

`Student` is logged in and authenticated.

**Steps**

- Student opens the `Survey` module
    - Assertion: the `Survey` module is displayed

- Student selects a survey to fill
    - Assertion: the preview shows that no survey is currently available
    - Assertion: Student's attempt to display survey is logged
    - Assertion: `Student` is prompted to proceed with next request



### 2. `Student` tries to fill in a survey from subject he is not enrolled in

**Setup**

`Student` is logged in and authenticated.

**Steps**

- Student opens the `Survey` module
    - Assertion: the preview shows all available surveys

- `Student` selects a survey to fill
    - Assertion: request is validated

- `Student` tries to fill in a selected survey
    - Assertion: `Student`'s permissions are checked
	- Assertion: `Student`'s request is denied
	- Assertion: `Student`'s attempt is logged
	- Assertion: `Student` is notified about invalid request



### 3.`Student` tries to fill in an existing survey

**Setup**

`Student` is logged in and authenticated.

**Steps**

- `Student` opens the `Survey` module
	- Assertion: the preview shows all available surveys

- `Student` selects a survey to fill
	- Assertion: request is valid since there are surveys available

- `Student` tries to fill in a selected survey
    - Assertion: `Student`'s permissions are checked
	- Assertion: `Student`'s access is granted

- `Student` fills in a form but doesn't specify level of anonymity
- `Student` submits a form
	- Assertion: form is validated
	- Assertion: validation failed, form is not filled in properly
	- Assertion: form is returned for correction

- `Student` selects a level of anonymity
- `Student` resubmits a survey
	- Assertion: survey is validated
	- Assertion: validation succeeds
	- Assertion: survey is succesfully added to the system
	- Assertion: `Student` is notified about successful submitting of survey into system
