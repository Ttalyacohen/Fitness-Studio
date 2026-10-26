# Fitness Studio Management System

A Java system for managing a fitness studio: clients, instructors, a secretary, and group sessions.
Built as part of the Object-Oriented Programming course at Ariel University, with a focus on clean OOP design and classic design patterns.



## Features

- Client registration and removal, with validation (minimum age, duplicates, unregistered clients)
- Four session types (Pilates, Machine Pilates, Thai Boxing, Ninja), each with its own capacity and price
- Instructor hiring with per-session-type qualifications
- Session enrollment with checks for capacity, qualification, audience type (forum) and session date
- Salary payments and a running gym balance
- Notifications to clients by session, by date, or to everyone
- Full action history log

## Design

| Pattern | Where |
|---|---|
| **Singleton** | `Gym` – a single gym instance shared across the system |
| **Factory** | `sessionFactory` – creates the right `Session` subclass from a `SessionType` |
| **Observer** | `Sender` / `NewsletterPublisher` publish to `Member` subscribers (`Client`) |

Other OOP principles used:

- **Inheritance:** `Person` → `Client`, `Instructor`, `Secretary`; abstract `Session` → four session types
- **Encapsulation:** state is changed only through the current `Secretary`; former secretaries are blocked
- **Custom exceptions:** `InvalidAgeException`, `DuplicateClientException`, `ClientNotRegisteredException`, `InstructorNotQualifiedException`

## Project structure

```
gym/
├── customers/    Person, Client, Gender
├── management/   Gym, Secretary, Instructor, Session and its subclasses, sessionFactory, notifications
└── Exception/    custom exceptions
Main.java         demo scenario
```

## Run

```bash
javac -d out Main.java $(find gym -name "*.java")
java -cp out Main
```

The demo in `Main.java` uses session dates in early 2025. Because enrollment is only allowed for future sessions, running it today prints "Session is not in the future" for those enrollments. That is the validation working as intended. To see successful enrollments, change the dates in `Main.java` to future dates.
