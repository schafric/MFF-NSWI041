# Student information system - Scheduling

This system module is intended to be used for creating, modifying and viewing
university schedules.

Module `Scheduling` will be integrated into a larger system with other modules
(such as `Students`, `Enrollment`, `Exams`, `Surveys` and `Theses`) will
perform only tasks specific for scheduling.

## Definitions

`Subject` is a system entity, which identifies educational subject (such
as Combinatorics, Mathematical Analysis, etc.).

`Room` is an entity, which describes and identifies physical room in the
university building or virtual room in any available videotelephony software
program.

`Studying plan` is a list of mandatory subjects, that a student shall
accomplish before submitting thesis.

`Schedule sheet` is a virtual placeholder with unique identifier, which
identifies a pair of subject and student capacity, ex. id <->
(subject, capacity). These entities are created based on estimated
students' interest.

`Schedule triple` is any (schedule sheet, room, time span) triple, where time
span contains two time stamps symbolizing start and finish of an event.

`Schedule` is a finite set of schedule triples. A schedule is considered as
invalid if there is a pair of triples with overlapping time spans.

`Central schedule` is a valid schedule is being purposefully created by
a `planner` for the upcoming semester.

`Standard operations` on a system entity are creating, modifying, removing
and viewing.

## Functional Requirements

This section specifies the functional requirements.

Requirements are divided on two parts, user and system. User requirements
cover users' imminent needs and wishes. Subsequent system requirements discuss
previously introduced in greater detail and also cover constraints arisen from
the problem domain and project constraints (budget, time and people resources).
Then, we identify actors within the system and describe their typical use cases.

Certain requirements might repeatedly appear in different contexts. For
instance, the ability to create and modify subjects is a user requirement as
well as ability of an actor `planner`.

### User requirements

We list user requirements with intention to identify detailed system
requirements and actors. Each item of the list may be read as "The system
should provide ability to..."

- Provide friendly user interface.

- Manage module resources, users and user permissions.

- Perform standard operations on `subjects`, `rooms` and `schedule sheets`.

- Create conflict-free `central schedules` based on `studying plans` and
  other constraints.

- Add constraints on `central schedules`.

- Import and view `central schedules` (weekly, monthly, etc.) and information
  about other module entities in different formats.

### System requirements

In this chapter, we specify user requirements in greater details. We use
approach similar to the previous chapter, group and list requirements based on
semantics and meaning. We assume, that the module user is a `root` profile or
has been authorized via central authorization module before accessing it.

**User interface**

- Provide modern web interface with all functionality necessary for the
  operation.

**Administration**

- Restart and shut down the `Scheduling` module.

- Enrich profiles from central record module with additional information
  associated with module `Scheduling`.

- Modify profile module role. Administrator role can assign roles to other
  profiles. The module is initialized with one `root` administrator profile.

**Planning activities**

- Perform standard operations on `subjects`. By modifying a subject we mean
  updating information (description, sylabus, amount of e-credits, guarantor,
  etc.). Subject can be recommended for a specific semester as students
  progress or `studying plan`.

- Perform standard operations on `rooms`. Room capacity shall be specified
  as a constraint for all physical rooms and might be specified for virtual
  rooms on demand.

- Perform standard operations on `studying plans` after all necessary
  `subjects` are created.

- Perform standard operations on `schedule sheets`. Total capacity for
  a particular `subject` shall reflect `studying plans` as well as estimated
  students' interest in enrolling in the subject. All `schedule sheets`
  created for the current semester must be assigned to some `schedule triple`.
  Impossibility for such assignment is a severe conflict, which prevents
  `central schedule` to be constructed.

- Create `central schedule` in automatic mode by using `schedule sheets` and
  and other constraints.

- Create and modify `central schedule` in manual mode. Manual mode assumes,
  that `schedule triples` will be created, removed or modified one-by-one.
  Correctness could be verified at any time.

- Created `schedule triples` shall ensure, that students are able to visit
  all subjects from `studying plan` planned for the current semester.

- Save created `central schedule`, remove it to start all over, release it
  to other modules and university personnel.

**Student and teacher activities**

- View available information about `subjects`, `rooms` and `schedule sheets`.

- View `central schedule` released by a planner entirely, or filtered by
  various criteria.

**Specific student activities**

- View `studying plan` with additional information about already passed
  mandatory subjects.

- Maintain a bin of `schedule triples` for the current semester with ability
  to add, and remove them without any restrictions. A bin is used for
  constructing preliminary student schedule, actual construction happens
  within `Enrollment` module.

**Specific teacher activities**

- Introduce unavailability constraints into a prepared `central schedule`.
  Such constraints will be considered while creating `schedule triples`, but
  are not mandatory for a `planner`.

- Adjust metadata about `schedule-triples` - for example adding links for student enrolled in that triple (to third parties like moodle, one drive etc.), providing them with further instructions or information.

**Reporting activities**

- Collect and view statistics about room occupation or fulfillment of all
  `studying plans` for the current semester.

- Import the entire `central schedule` or certains parts of it in a data
  format of choice (json, csv, pdf, etc.).

#### Actors

We define several kinds of actors: administrator, planner, student and teacher.

##### Actor: Administrator

`Administrator` is an actor performing module maintenance and administrative
tasks, such as user administration, deployment of new module versions.
Synchronization with other modules is performed automatically and in a daily
basis.

##### Actor: Planner

`Planner` is an actor performing **planning activities**. In general, it is
an authority, who defines `subjects`, `rooms`, `studying plans`,
`schedule sheets` and schedules taking into account introduced constraints.

##### Actor: Student

`Student` is an actor performing **student activities**. The user can view
existing entities, but cannot modify them or intervene planning process.

##### Actor: Teacher

`Teacher` is an actor performing **teacher activities**. The user can introduce
non-mandatory constraints into planning process and can view planning entities.

#### Use cases

We define define the following use cases.

 1. Student can preview schedule.
 2. Student can export schedule to PDF.
 3. Student can open detail of schedule-triple.
 4. Teacher can edit metadata about schedule-triple.
 5. Planner can schedule subjects manually.
 6. Planner can asssign schedule sheet to a schedule triple with check of room availability.
 7. Planner can assign schedule sheet to a schedule triple with check of conflicts with other compulsory subjects.
 8. 
 9. 
10. 
11. 
12. 

The following figure is an integrated diagram containing all use cases
described in the following chapters.

```plantuml
@startuml
left to right direction
actor Student as s
actor Teacher as t
package Scheduler {
  usecase "Show Schedule" as UC1
  usecase "Print schedule for given semester" as UC2
  usecase "Preview schedule-triple detail" as UC3
  usecase "Edit subject-triple detail" as UC4
}
s --> UC1
s --> UC2
s --> UC3
t --> UC4
@enduml
```

##### 1. Student can preview schedule

Student can preview schedule for given semester where he/she can see all
subject triples in which he/she enrolled.

##### 2. Student can export schedule to PDF

Student can export detailed schedule for the whole semester into PDF format - for example for printing it out on paper.

##### 3. Student can open detail of schedule-triple

Student can preview detail of given schedule-triple which can contain additional information about this specific
schedule-triple - for example reading some further description/instruction from teacher.

##### 4. Teacher can edit metadata about schedule-triple

Teacher can edit several metadata about schedule-triple of subject they teach - for example providing students with
further instructions, links to external services (e.g. moodle, one drive) etc.

##### 5. Planner can schedule subjects manually

Planner can create schedule sheets according to the studying plan for current term.
Planner has a subject from studying plan he needs to schedule. He fills in a capacity, thus creating schedule sheet with unique ID. Capacity of various subjects may differ, lectures will usually have greater capacity than tutorials. Schedule sheets don´t need to be scheduled immediately and may be created at any time.

```plantuml
@startuml
left to right direction
actor Planner
package Schedule {
    usecase "Select subject from studying plan" as Plan
    usecase "Create schedule sheet" as Create 
}
Planner --> Create
Create .> Plan : include
@enduml
```

##### 6. Planner can assign schedule sheet to a schedule triple

Planner can assign schedule sheet to a schedule triple and system will automatically check availability of assigned room during specified time slot.
When schedule sheet with unique ID has been created, it can be paired with room. Room may be chosen manually (by planner) or automatically (based on capacity constraint). System will automatically check whether assigned room is available during specified time slot. If the room is not available, schedule triple will not be created.

```plantuml
@startuml
left to right direction
actor Planner
package Schedule {
    usecase "Check room availability" as Check    
    usecase "Create schedule triple" as Triple
    usecase "Create schedule sheet" as Sheet
}
Triple .> Check : include
Sheet <. Triple : include
Planner --> Triple
@enduml
```

##### 7. Planner can assign schedule sheet to a schedule triple

Planner can assign schedule sheet to a schedule triple. There must be no conflicts among subjects taught at the same term which are compulsory according to the studying plan. System will not accept schedule triple, if it is in conflict with already registered schedule triple.

```plantuml
@startuml
left to right direction
actor Planner
package Schedule {
    usecase "Check time slot" as Check
    usecase "Create schedule triple" as Create
    usecase "Create schedule sheet" as Sheet
}
Planner --> Create
Create .> Check : include
Sheet <. Create : include
@enduml
```

##### 8. 



##### 9. 



##### 10. 



##### 11. 



##### 12. 


