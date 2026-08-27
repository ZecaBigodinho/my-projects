# 🎓 Zigurate — Educational Management Platform

<p align="center">
  <strong>Educational Technology • Role-Based Access Control • NoSQL Data Modeling</strong>
</p>

**Status:** Completed

**Technologies:**
`Python` `MongoDB`

---

## 🚀 Project Overview

**Zigurate** is an educational management platform designed to support schools in digitizing classroom activities, learning materials and communication between teachers and students.

The project was created with the goal of reducing reliance on paper-based activities and excessive use of the traditional classroom board by providing a centralized digital environment for:

* Assignments and activities
* Tests and educational content
* Recorded lessons
* Teacher-student communication
* Class interaction
* Digital learning resources

The application was developed as a **team project involving two developers**.

---

# 🎯 Problem

Traditional classroom workflows often require teachers to distribute activities, provide learning materials and communicate with students through several disconnected channels.

The project explores how these workflows could be centralized into a single educational platform.

The core idea was:

```text
Teacher
   │
   ├── Publish learning material
   ├── Create activities
   ├── Share recorded lessons
   └── Communicate with students
           │
           ▼
      Digital Classroom
           │
           ▼
Student
   ├── Access material
   ├── Complete activities
   ├── Watch lessons
   └── Communicate with teacher/class
```

---

# ✨ Key Features

## 💬 Direct Support Channel

A private communication channel between teachers and students.

This provides a dedicated space for individual support and communication related to the learning process.

---

## 👥 Class Community

Each class has its own group communication space where students can interact and collaborate with their classmates.

This creates a digital environment focused specifically on the members of a particular class.

---

## 🎥 Lesson Repository

Teachers can publish links to recorded lessons, including YouTube videos.

The platform centralizes these resources so students can access previously recorded classes from the same educational environment.

---

## 📝 Activity Module

Teachers can create and publish activities for students.

Students can then access and complete the activities directly through the platform.

The module provides a foundation for moving classroom assignments from paper-based workflows into a digital environment.

---

# 🔐 Role-Based Access Control

One of the main technical challenges of the project was implementing different permissions according to the authenticated user's role.

The application distinguishes between:

### 👨‍🏫 Teacher

Teachers have management permissions over educational content.

They can:

* Add content
* Remove content
* Manage educational resources
* Create activities
* Publish learning materials

### 👨‍🎓 Student

Students have more restricted permissions.

They can:

* View published content
* Access learning materials
* Interact with available resources
* Participate in class communication
* Complete activities

The permission model can be represented as:

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
        Management Access     Interaction Access
                │                 │
        ┌───────┼───────┐    ┌────┼────┐
        ▼       ▼       ▼    ▼         ▼
      Create  Update  Delete View    Interact
```

This provided practical experience with **Role-Based Access Control (RBAC)** and the importance of enforcing authorization rules according to the user's responsibilities.

---

# 🗄️ Database Architecture

Another major technical responsibility in this project was designing and managing the application's **MongoDB database architecture**.

The platform handles different types of information, including:

* User data
* Chat messages
* Educational activities
* Images
* Video links
* Learning resources

Because MongoDB is a non-relational database, the project required careful consideration of how different types of data should be structured and accessed.

The experience highlighted the importance of:

* Data modeling
* Document structure
* Relationships between application entities
* Consistent data organization
* Designing around application access patterns

---

# 🧠 My Role

This project was developed by a team of two.

My primary responsibilities were:

### 🔐 Authorization & Permissions

I was responsible for implementing the permission system that differentiates the capabilities of teachers and students.

This included designing the logic necessary to ensure that users received the appropriate level of access after authentication.

### 🗄️ Database Architecture

I was also responsible for designing the database structure using MongoDB.

This required determining how different types of educational and communication data should be represented and accessed by the application.

---

# 🧩 Technical Challenges

## Challenge 1 — Different User Permissions

The system needed to support multiple types of users while preventing students from accessing management functionality intended for teachers.

The solution was based on a role-oriented permission model.

This introduced practical experience with **authorization**, which is distinct from authentication:

```text
Authentication
      ↓
"Who are you?"
      ↓
Authorization
      ↓
"What are you allowed to do?"
```

---

## Challenge 2 — Modeling Heterogeneous Data

The platform stores several different types of information, from chat messages and activities to images and external video links.

Designing a consistent structure for these different entities was one of the main challenges of working with MongoDB.

This reinforced an important lesson:

> A flexible database does not eliminate the need for careful data modeling.

---

# 📚 Key Learnings

This project significantly strengthened my understanding of:

* Role-Based Access Control
* Authentication vs. authorization
* NoSQL database design
* MongoDB data modeling
* Application permissions
* Multi-user software architecture
* Educational software requirements
* Team-based software development

The most important lesson was that **software architecture needs to reflect the responsibilities of the people using the system**.

A teacher and a student may use the same application, but they should not necessarily have the same capabilities.

---

# 📸 Visual Evidence

## 🔐 Login

<img width="950" height="779" alt="Application login screen" src="https://github.com/user-attachments/assets/92337614-8584-4688-9ca1-1f66244d3d4e" />

---

## 👨‍🎓 Student Interface

<img width="934" height="718" alt="Student interface" src="https://github.com/user-attachments/assets/ddf539c4-bf8b-4525-9390-6eba16f58feb" />

---

## 📚 Learning Materials

<img width="919" height="551" alt="Learning materials interface" src="https://github.com/user-attachments/assets/eb3238af-249f-4d59-9263-4a54f5a84013" />

---

## 💬 Teacher Communication

<img width="950" height="775" alt="Teacher communication interface" src="https://github.com/user-attachments/assets/d7338c43-4e3a-474c-af5e-9544600242e2" />

---

## 🏠 Main Interface

<img width="927" height="737" alt="Main application interface" src="https://github.com/user-attachments/assets/09276765-675f-458c-98fa-d11e271ca468" />

---

## 🎫 Support / Ticket System

<img width="924" height="668" alt="Support ticket interface" src="https://github.com/user-attachments/assets/c2bd3f0e-48d6-473d-bdf0-71e0c9417fc0" />

---

## 🎥 Video Lessons

<img width="950" height="462" alt="Video lesson interface" src="https://github.com/user-attachments/assets/36baf026-b8a1-47fa-8bb0-8a222b83ee3c" />

---

# 💻 Technology Stack

| Category                 | Technology                         |
| ------------------------ | ---------------------------------- |
| **Programming Language** | Python                             |
| **Database**             | MongoDB                            |
| **Architecture**         | Multi-user educational application |
| **Access Control**       | Role-Based Access Control (RBAC)   |
| **External Content**     | YouTube                            |

---

# 🎓 Educational Impact

The project explores the use of software to centralize common classroom activities into a digital environment.

Instead of relying on separate channels for assignments, recorded lessons and communication, the platform brings these resources together into a single application.

This project is particularly relevant to my broader interest in **Educational Technology**, combining my software development experience with my work in technology education.

---

# 🔭 Future Possibilities

Although the project is completed, its architecture provides a foundation for future improvements such as:

* More sophisticated assignment workflows
* Automated grading
* Expanded assessment functionality
* Analytics for teachers
* Mobile support
* Richer notification systems
* Integration with additional educational services

These possibilities would allow the platform to evolve from a classroom management application into a broader learning environment.

---

# 📌 Project Summary

**Zigurate** demonstrates practical experience in developing a multi-user educational platform while solving two important engineering problems:

**1. Designing permissions around different user roles.**

**2. Modeling heterogeneous application data using MongoDB.**

The project represents an important step in my development as a software engineer, particularly in **application architecture, authorization, database design and educational technology**.

---

<p align="center">
  <i>Technology should not only automate tasks — it should improve how people learn and collaborate.</i>
</p>
