# Entities

- Tasks
  - name (text) 1-1
  - order (text) 1-1
  - created_at (timestamp) 1-1
  - due (timestamp | null) 1-1
  - completed_at (timestamp | null) 1-1
  - owner (person) 1-1

- Person
  - name 1-1
  - tasks  many-many

- Project
  - name
  - tasks 1 - many
  - people many - many

## Database

### Table: Tasks
 - id (int) (primary key) 
  - name (text) 
  - order (text)
  - created_at (timestamp)
  - due (timestamp | null) 
  - completed_at (timestamp | null)
  - owner (int) (foreign key)
  - project_id (int | null) (foreign key)

### Table: Persons
 - id (int) (primary key)
 - name (text)

### Table: Projects
 - id (int) (primary key)
 - name (text)

### Table: Assigned_Tasks
 - id (int) (primary key)
 - person_id (int) (foreign key) (index)
 - task_id (int) (foreign key)


### Table: Persons_Projects
 - id (int) (primary key)
 - person_id (int)  (foreign key)
 - project_id (int) (foreign key)


==================

# Actions

- create task
- update / edit task
- delete task
- assign task to user / project
- unassign task from a user / project
- complete task
- get tasks
- get single task
- get users
- get projects
- get tasks by owner
- get tasks by project

## API


Create new task: 

POST /api/tasks 

Body: {
    user_id: int, 
    name: str,
    order: str,
    due: datetime?,
    project: int?
    assigned_to: Array<str>?
}

user_id should really be part of session management

Update task: 

POST /api/tasks/<task_id>

Body {
    name: str?,
    order: str?,
    due: datetime?,
    completed: bool?
    project: int?, 
    assigned_to: Array<str>?
}

Delete task: 

DELETE /api/tasks/<task_id>

get tasks

GET /api/tasks

query parameters: 
owner: int?
assigned: int?
project: int? 

get users: 

GET /api/users

get tasks assigned to user: 

GET /api/users/<user_id>/tasks

get projects: 

GET /api/projects

get tasks in project: 

GET /api/projects/<project_id>/tasks