# Daneshjooyar — AP Project

Daneshjooyar is a student management mobile application built as an Advanced Programming project in Spring 2024. The project combines a **Flutter front-end** with a **Java socket-based back-end** to help students manage assignments, tasks, courses, profile information, rankings, birthdays, and university-related news.

## Team Members

| Name | Role |
|---|---|
| Iman Babajani | Back-end developer |
| Mehdi Karimi | Front-end developer |

## Project Overview

The goal of Daneshjooyar is to provide students with a simple mobile app for organizing academic work. Students can sign up, log in, view their courses, check assignments, track remaining deadlines, update their profile, and see class-related information through a Flutter interface connected to a Java server.

## Main Features

- Student sign-up and login
- Password validation and account authentication
- Student profile page
- Course and class information
- Assignment and task management
- Marking tasks as completed
- Dashboard summary for assignments and grades
- Student rankings based on average grades
- Birthday section for students
- University news page
- Local text-file-based data storage
- Java socket server for communication between the app and back-end

## Tech Stack

### Front-end

- Flutter
- Dart
- Material UI
- Shared Preferences
- HTTP package
- Socket communication using `dart:io`

### Back-end

- Java
- TCP Socket Programming
- Multi-threaded client handling
- Text-file database storage

## Project Structure

```text
AP_project_flutter-main/
├── README.md
├── cli/
│   ├── src/
│   │   ├── Main.java
│   │   ├── database/
│   │   │   ├── databasehandler.java
│   │   │   ├── student.txt
│   │   │   ├── teacher.txt
│   │   │   ├── course.txt
│   │   │   └── assignemnt.txt
│   │   ├── main/
│   │   │   ├── Admin.java
│   │   │   ├── Assignment.java
│   │   │   ├── Course.java
│   │   │   ├── Student.java
│   │   │   └── Teacher.java
│   │   └── server/
│   │       ├── APP.java
│   │       └── server.java
│   └── bin/
│       └── compiled Java files
└── front/
    └── AP_Project/
        ├── lib/
        │   ├── main.dart
        │   ├── screens/
        │   ├── widgets/
        │   ├── model/
        │   ├── theme/
        │   └── utils/
        ├── assets/
        │   └── images/
        └── pubspec.yaml
```

## Back-end Description

The back-end is written in Java and works as a TCP socket server. It listens on port `8888` and handles each connected client using a separate thread.

The server is responsible for:

- Reading and writing student, teacher, course, and assignment data
- Handling user login and registration
- Returning profile information
- Returning courses and assignment data
- Updating passwords
- Returning birthday and ranking data
- Saving updated data back into text files

The main server file is:

```text
cli/src/server/server.java
```

The local database files are stored in:

```text
cli/src/database/
```

## Front-end Description

The front-end is built with Flutter. It provides the mobile user interface for students and communicates with the Java server through sockets.

Important screens include:

- Welcome screen
- Sign-in screen
- Sign-up screen
- Home screen
- Task screen
- Assignment screen
- Classes screen
- News screen
- Birthdays tab
- Rankings tab
- User profile page

The main Flutter source folder is:

```text
front/AP_Project/lib/
```

## Requirements

Make sure these tools are installed before running the project:

- Java JDK 11 or newer
- Flutter SDK compatible with Dart `>=3.3.2 <4.0.0`
- Android Studio or VS Code
- Android emulator or physical Android device

## How to Run the Back-end

Open a terminal in the Java project folder:

```bash
cd cli/src
```

Compile the Java files:

```bash
javac -d ../bin Main.java main/*.java database/*.java server/*.java
```

Run the socket server:

```bash
java -cp ../bin server.server
```

The server will start listening on:

```text
Port: 8888
```

## How to Run the Flutter App

Open another terminal and go to the Flutter project folder:

```bash
cd front/AP_Project
```

Install Flutter dependencies:

```bash
flutter pub get
```

Run the app:

```bash
flutter run
```

## Important Network Configuration

The Flutter app currently connects to the back-end using this IP address:

```dart
Socket.connect('192.168.43.66', 8888)
```

Before running the app, update this IP address based on your environment:

- If you use a real phone, connect the phone and computer to the same network, then replace `192.168.43.66` with your computer's local IP address.
- If you use an Android emulator and the Java server is running on the same computer, use:

```dart
Socket.connect('10.0.2.2', 8888)
```

You can find all current socket connections by searching for:

```text
Socket.connect
```

inside:

```text
front/AP_Project/lib/
```

## Communication Protocol

The Flutter app sends text commands to the Java server through TCP sockets. Commands are separated by `-` and terminated with a null character `\u0000`.

Example login request:

```text
studentId-login-studentId-password\u0000
```

Example sign-up request:

```text
globalUsername-sign-id-password-name-birthDate\u0000
```

The server parses the command and sends a text response back to the client.

## Data Storage

This project uses simple text files instead of a relational database. The main data files are:

```text
student.txt
teacher.txt
course.txt
assignemnt.txt
```

These files are read when the server starts and updated when changes are made.

## Notes

- The project is designed for educational purposes.
- The back-end uses socket programming instead of REST APIs.
- The database is file-based, so it is simple and easy to inspect.
- The server must be running before using login, sign-up, course, assignment, ranking, birthday, and profile features in the Flutter app.

## Future Improvements

Possible improvements for future versions:

- Replace text files with SQLite, MySQL, or PostgreSQL
- Move the hardcoded server IP into a configuration file
- Add better error handling for socket connection failures
- Add encrypted password storage
- Add REST API support
- Improve validation for user input
- Add admin and teacher dashboards to the mobile app
- Add unit and integration tests

## Credits

This project was developed by **Iman Babajani**, **Ali Montazeriyoun**, and **Mehdi Karimi** for the AP course in Spring 2024.

- Back-end development: **Ali Montazeriyoun**
- Front-end development: **Mehdi Karimi**
- Project collaboration: **Iman Babajani**
