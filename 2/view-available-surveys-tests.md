# Test cases

## Student views available surveys

### 01 Normal

**Setup**
- _test-student_ attends subjects NAAA001 and NABC123
- There is one survey for subject NAAA001 titled "Feedback for practicals"
- There are two surveys for subject NABC123 titled "Programming langnuages" and "Preffered form of exam"
- The user is logged in as `student` _test-student_ and is authenticated

**Steps**
- Click `available surveys`
- [Assert] Valid request is sent to the system
- [Assert] System received the request
- [Assert] System checked that the request is valid
- [Assert] System returns valid response with list of surveys
- [Assert] List of surveys is displayed on screen
- [Assert] Displayed list contains 3 surveys:
   - NAAA: Feedback for practicals
   - NABC: Preffered form of exam
   - NABC: Programming langnuages

### 02 Database server temporarily unavailable

**Setup**
- The user is logged in as `student` _test-student_ and is authenticated
- Database server is shut down

**Steps**
- Click `available surveys`
- [Assert] Valid request is sent to the system
- [Assert] System received the request
- [Assert] System responds with status code 500
- [Assert] Error message is displayed on screen notifying user about error and asking him to try again later

### 03 Invalid request

**Setup**
- `student` _test-student_ is logged in and authenticated

**Steps**
- Using a command-line, send an invalid request to the system
- [Assert] System received the request
- [Assert] System checked the request
- [Assert] System responed with status code 400
- [Assert] Attempt is logged

