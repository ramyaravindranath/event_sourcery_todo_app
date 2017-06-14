# Event Sourcery Todo Example App

## Get started

Ensure you have Postgres and Ruby 2.2 or higher installed.

Then run the setup script.

```sh
$ ./scripts/setup
```

## Using the Application

Start the web app and processors.

```sh
$ foreman start
```

Then you can add a todo using the bundled scripts.

```sh
$ ./scripts/add -t "Get to the chopper" -d "It's in the trees" -s dillon@cia.gov -D 2017-01-01
```

## Application Structure

```
app
├── aggregates
│   └── todo.rb
├── commands
│   └── todo
│       └── add.rb
├── events
│   ├── todo_abandoned.rb
│   ├── todo_added.rb
│   ├── todo_amended.rb
│   └── todo_completed.rb
├── projections
│   └── outstanding
│       ├── projector.rb
│       └── query.rb
├── reactors
│   └── notifier.rb
└── web
    └── server.rb
```

## Routes

```
GET /todos/outstanding
GET /todos/completed
GET /todos/scheduled
POST /todo/:id (add)
PUT /todo/:id (amend)
POST /todo/:id/complete
POST /todo/:id/abandon
```

## Events

- TodoAdded
- TodoCompleted
- TodoAbandoned
- TodoAmended

## Aggregates

- Todo
  - title
  - description
  - due_date
  - stakeholder_email

## Projections

- Outstanding
- Completed
- Scheduled (has due date)

## Reactor

- Notifier
  - "sends" email
  - Emits StakeholderNotified event
