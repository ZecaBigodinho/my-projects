# 🎮 Gamified Learning Platform

<p align="center">
  <strong>Educational Technology • Gamification • Real-Time Interaction • Serverless Backend</strong>
</p>

**Status:** Testing Phase

**Technologies:**
`Flutter` `Dart` `Firebase` `Cloud Firestore` `Cloud Functions`

---

## 🚀 Project Overview

This project is a gamified educational platform designed for schools, combining digital activity management, real-time interaction and performance tracking in a single application.

The platform supports two primary user roles:

* 👨‍🏫 **Teachers**
* 👨‍🎓 **Students**

Each role has its own interface, permissions and workflows.

The system was designed to modernize common classroom processes such as activity distribution, assessment, attendance and performance monitoring while increasing student engagement through gamification.

---

# 🎯 Project Goals

The platform was created around four main objectives:

* Digitize classroom activities and assessments
* Provide teachers with centralized management tools
* Give students a more interactive learning experience
* Provide immediate and structured performance feedback

The application combines traditional educational workflows with more dynamic assessment modes.

```text
Teacher
   │
   ├── Creates activities
   ├── Adds questions
   ├── Tracks attendance
   └── Reviews performance
           │
           ▼
     Learning Platform
           │
           ▼
Student
   ├── Receives activities
   ├── Completes assessments
   ├── Participates in Flash quizzes
   └── Receives scores
```

---

# 🔐 Role-Based Access Control

The platform implements **Role-Based Access Control (RBAC)** to separate teacher and student capabilities.

After authentication, the system determines the user's role and exposes only the appropriate functionality.

```text
               Authentication
                     │
                     ▼
                Identify Role
                /           \
               /             \
          Teacher           Student
             │                 │
             ▼                 ▼
       Management Tools   Learning Tools
```

This provides a clear separation between content management and content consumption.

---

# 👨‍🏫 Teacher Panel

The teacher interface acts as the administrative and analytical side of the application.

---

## 📊 Central Dashboard

Teachers have access to a centralized dashboard containing the main management tools.

The dashboard provides access to:

* Activities
* Question creation
* Attendance
* Student performance
* Course-related information

---

## 📝 Activity Management

Teachers can manage activities through complete CRUD operations.

They can:

* Create activities
* View existing activities
* Edit activities
* Delete activities

Each activity can be configured according to one of the supported interaction modes.

---

# ⚡ Dynamic Activity Modes

One of the main features of the platform is support for multiple assessment modes.

## 📘 Classic Mode

Classic activities behave like traditional assignments.

They can include a final deadline and allow students to complete the activity within the available period.

---

## ⚡ Flash Mode

Flash activities are designed to provide a faster, more dynamic quiz experience inspired by classroom quiz platforms such as Kahoot.

Each question has its own countdown timer.

```text
Question Displayed
       │
       ▼
Timer Starts
       │
       ├── Student Answers
       │
       └── Timer Reaches Zero
               │
               ▼
        Next Question
```

This creates a more competitive and interactive learning environment.

---

# ✍️ Question Authoring

Teachers can build activities containing different types of questions.

Supported question formats include:

* Multiple-choice questions
* Essay-style questions

Questions can also include images uploaded through the application.

This allows activities to support both objective assessments and more open-ended evaluation formats.

---

# 🗓️ Attendance System

The application includes an attendance management system.

Teachers can:

* Register student attendance
* Associate attendance with courses
* Associate attendance with specific dates
* Consult previous attendance records

This brings another common classroom workflow into the same digital environment.

---

# 📈 Student Performance Dashboard

Teachers can monitor student progress through a dedicated performance interface.

The dashboard allows teachers to inspect:

* Completed activities
* Individual student results
* Activity scores
* Progress across available assessments

This functionality required the application to persist score information in a way that could be efficiently accessed for reporting.

---

# 👨‍🎓 Student Panel

The student experience is focused on activity discovery, participation and performance feedback.

---

## 📚 Activity List

Students can view activities available for their course.

The interface uses visual indicators to distinguish activity modes.

For example:

```text
📘 Classic Activity
⚡ Flash Activity
```

This helps students quickly understand the expected interaction format.

---

# 🧠 Interactive Quiz Experience

Students can respond to both Classic and Flash activities through an interactive Flutter interface.

The application handles:

* Question navigation
* User answers
* Activity mode behavior
* Score calculation
* Activity completion

---

# ⏱️ Real-Time Flash Quiz Logic

The Flash mode introduced one of the main technical challenges of the project.

Each question requires a countdown timer that interacts with the Flutter widget lifecycle.

The application manages:

```text
Display Question
      ↓
Start Timer
      ↓
Update Interface
      ↓
Check Remaining Time
      ↓
Advance Automatically
      ↓
Cancel / Restart Timer
```

This required careful handling of `StatefulWidget` lifecycle behavior.

Timers need to be correctly initialized and disposed to avoid unnecessary callbacks or resource leaks after a widget is no longer active.

---

# 🏆 Gamification

Gamification is primarily implemented through the Flash activity mode.

The countdown-based question flow introduces:

* Time pressure
* Faster interactions
* Immediate progression
* More dynamic classroom participation

Rather than replacing traditional assessments, the platform supports both:

```text
Traditional Assessment
        +
Gamified Assessment
```

This allows teachers to choose the interaction model that better fits each activity.

---

# 📊 Automatic Score Tracking

Student scores are calculated and persisted automatically at the end of an activity.

The application stores activity performance so that results can later be displayed in the teacher dashboard.

One important architectural decision was introducing an `activityScores` map inside each user document.

Conceptually:

```text
Student
   │
   └── activityScores
          │
          ├── activity_001 → score
          ├── activity_002 → score
          └── activity_003 → score
```

This structure made it possible to retrieve a student's activity history efficiently for the performance dashboard.

---

# ☁️ Firebase Architecture

The application uses Firebase as its serverless backend.

Cloud Firestore stores the main application data, while Cloud Functions support automated backend operations.

```text
┌─────────────────────────────┐
│       Flutter Client        │
│                             │
│ Teacher Interface           │
│ Student Interface           │
│ Quiz Logic                  │
│ Timer / State               │
└──────────────┬──────────────┘
               │
               ▼
┌─────────────────────────────┐
│          Firebase           │
│                             │
│ Authentication              │
│ Cloud Firestore             │
│ Cloud Functions             │
└─────────────────────────────┘
```

---

# 🗄️ Firestore Data Modeling

One of the main challenges was creating a flexible Firestore architecture capable of supporting several different educational workflows.

The database needs to represent information such as:

* Users
* Roles
* Courses
* Activities
* Questions
* Scores
* Attendance records

The challenge was not simply storing the data, but structuring it in a way that supported the application's access patterns.

---

# 🧩 Flexible Activity Architecture

The platform supports multiple activity modes within the same broader activity system.

Conceptually:

```text
Activity
   │
   ├── Metadata
   ├── Questions
   ├── Course
   ├── Activity Type
   │
   ├── Classic
   │     └── Deadline
   │
   └── Flash
         └── Question Timer
```

This approach allows activity behavior to change while maintaining a common overall structure.

---

# ⚙️ Automated Data Maintenance

Cloud Functions are also used to automate user-data cleanup.

This introduced practical experience with backend operations that happen independently of the Flutter client.

```text
Database / User Event
         │
         ▼
    Cloud Function
         │
         ▼
 Automated Cleanup
         │
         ▼
Database Integrity
```

This reinforced the importance of keeping data maintenance responsibilities on the backend when appropriate.

---

# 🏛️ Application Architecture

The overall system separates client interaction from persistent backend services.

```text
             Flutter Application
                    │
          ┌─────────┴─────────┐
          │                   │
          ▼                   ▼
     Teacher UI           Student UI
          │                   │
          └─────────┬─────────┘
                    │
                    ▼
             Application Logic
                    │
                    ▼
                Firebase
          ┌─────────┼─────────┐
          │         │         │
          ▼         ▼         ▼
        Auth    Firestore   Functions
```

---

# 💻 Technology Stack

| Category                     | Technology                     |
| ---------------------------- | ------------------------------ |
| **Cross-Platform Framework** | Flutter                        |
| **Application Language**     | Dart                           |
| **Backend Platform**         | Firebase                       |
| **Database**                 | Cloud Firestore                |
| **Database Model**           | NoSQL                          |
| **Backend Automation**       | Firebase Cloud Functions       |
| **Access Control**           | Role-Based Access Control      |
| **UI State**                 | StatefulWidget / Flutter State |
| **Real-Time Logic**          | Dart Timer                     |

---

# 🧠 My Role

This project was developed **individually**.

I was responsible for the full development lifecycle, including:

* Application architecture
* Flutter frontend development
* Firebase integration
* Firestore data modeling
* Role-based access logic
* Activity system design
* Quiz behavior
* Score persistence
* Attendance functionality
* Teacher dashboards
* Cloud Function integration

Developing the project independently required making both frontend and backend architectural decisions.

---

# 🧩 Main Technical Challenges

## 1. Flexible Firestore Architecture

The database needed to support several different use cases without becoming difficult to query or maintain.

This included:

* Multiple activity types
* Student scores
* Teacher dashboards
* Attendance history
* Course-specific data

The `activityScores` structure was an important architectural decision because it directly supported the performance dashboard.

---

## 2. Flash Quiz State Management

The Flash quiz required real-time countdown behavior.

The timer needed to interact correctly with the widget lifecycle while:

* Updating the interface
* Advancing questions
* Handling time expiration
* Avoiding callbacks after widget disposal

This provided practical experience with asynchronous UI behavior in Flutter.

---

## 3. Automated Data Integrity

Cloud Functions were introduced to automate user-related cleanup operations.

This reinforced the principle that certain data-integrity operations should not depend exclusively on actions performed by the client.

---

# 📚 Key Learnings

The project strengthened my understanding of:

* Flutter application architecture
* Serverless systems
* Cloud Firestore
* NoSQL data modeling
* Role-Based Access Control
* Real-time UI state
* StatefulWidget lifecycle management
* Timer lifecycle management
* Automated backend operations
* Student performance tracking
* Educational software design
* Gamification
* Full individual project ownership

One of the most important lessons was that the database architecture must be designed around the information the application will need to retrieve later.

The performance dashboard is a clear example: the way scores were stored directly influenced how efficiently student performance could be displayed.

---

# 🎓 Educational Technology

This project combines software engineering with educational design.

Instead of implementing only a digital version of traditional activities, the platform supports different learning interactions.

```text
Traditional Classroom Workflows
              +
      Digital Activities
              +
         Gamification
              +
      Performance Data
              =
   Interactive Learning Platform
```

The project reflects my broader interest in using software to support teaching, learning and classroom management.

---

# 🧪 Current Status

The platform is currently in the **testing phase**.

The core functionality has been implemented, while testing focuses on validating the behavior of the different activity modes, data flows and user interactions.

---

# 🔭 Future Possibilities

Potential future improvements include:

* Real-time classroom sessions
* Live teacher-controlled quizzes
* Leaderboards
* Achievements and badges
* Student progress analytics
* More detailed performance reports
* Question banks
* Automated activity generation
* Richer notification workflows
* Offline support
* Automated testing
* CI/CD
* Expanded accessibility support

---

# 📌 Project Summary

The **Gamified Learning Platform** demonstrates the design and implementation of a multi-role educational system combining:

```text
Flutter
   ↓
Role-Based Interfaces
   ↓
Educational Workflows
   ↓
Real-Time Quiz Logic
   ↓
Firebase
   ↓
NoSQL Data Modeling
   ↓
Performance Tracking
```

From an engineering perspective, the project demonstrates experience with **application architecture, state management, cloud databases, backend automation and role-oriented software design**.

From an educational perspective, it explores how traditional classroom workflows can be combined with interactive and gamified learning experiences.

---

<p align="center">
  <i>Combining software engineering, education and gamification to build more interactive learning experiences.</i>
</p>
