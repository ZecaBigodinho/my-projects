# 📱 Digital Canteen — Senac

A complete cross-platform digital canteen application built with **Flutter and Firebase**, designed to simulate a real-world school food ordering system.

The application, developed for **CantinaSenac**, provides separate experiences for students and canteen administrators, combining authentication, role-based access, real-time data synchronization, order management, product administration and automated notifications.

---

## 🚀 Project Overview

The project was developed incrementally, evolving from an initial **local mock database** into a cloud-based, serverless application using Firebase.

This evolution allowed the project to move from a simple application prototype toward a more complete distributed system capable of handling:

* User authentication and profiles
* Role-based access control
* Real-time product and order data
* Shopping cart and ordering workflows
* Product management
* Customer reviews and ratings
* Cloud-based file storage
* Automated push notifications
* Server-side event processing

The system supports two primary user roles:

| Role                            | Main Responsibilities                                                     |
| ------------------------------- | ------------------------------------------------------------------------- |
| 👨‍🎓 **Student**               | Browse products, place orders, track orders and review delivered products |
| 👨‍💼 **Canteen Administrator** | Manage products, monitor orders and update order statuses                 |

---

# ✨ Key Features

## 🔐 Authentication & Access Control

The application implements a complete authentication flow using Firebase Authentication.

* Email and password login
* New user registration
* User profile creation
* Password recovery via email
* Secure logout
* Role-based access control
* Student and administrator interfaces
* Role determination using Firestore user data

---

## 👨‍🎓 Student Experience

Students have access to a complete digital ordering workflow.

### Product Discovery

* Real-time product menu
* Product search by name
* Category filtering
* Product details
* Product descriptions
* User reviews and ratings

### Ordering

* Shopping cart
* Local cart state management
* Order creation
* Simulated payment flow
* Order history
* Real-time order status tracking

### Reviews

After an order is delivered, students can:

* Rate products
* Submit reviews
* View product reviews

---

## 👨‍💼 Canteen Administration

The application includes a dedicated administrative interface for managing the canteen operation.

### Dashboard

Administrators can access management functionality through a dedicated dashboard.

### Order Management

* Real-time incoming order monitoring
* Order status updates
* Preparation status management
* Ready-for-pickup status

### Product Management

Administrators can perform complete CRUD operations:

```text
Create
Read
Update
Delete
```

Product images can also be uploaded directly from the application to Firebase Storage.

---

# 🔔 Automated Notification System

One of the project's backend components is an automated notification workflow based on **Firebase Cloud Functions**.

The process works as follows:

```text
Administrator
     │
     │ Updates order status
     ▼
Cloud Firestore
     │
     │ Database event
     ▼
Cloud Function
     │
     │ Processes event
     ▼
Firebase Cloud Messaging
     │
     ▼
Student's device
```

When an administrator changes an order status to **"Ready for Pickup"**, a Cloud Function reacts to the database event and sends a push notification to the corresponding customer.

This separates the notification logic from the client application and allows the backend to react automatically to changes in persistent data.

---

# 🏛️ Architecture

The application follows a **client-server architecture with a serverless backend provided by Firebase**.

```text
┌──────────────────────────────┐
│        Flutter Client        │
│                              │
│  Student Interface           │
│  Administrator Interface     │
│  Authentication              │
│  Shopping Cart               │
│  Order Management             │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│           Firebase           │
│                              │
│  Authentication              │
│  Cloud Firestore             │
│  Firebase Storage            │
│  Cloud Messaging             │
└──────────────┬───────────────┘
               │
               │ Database Events
               ▼
┌──────────────────────────────┐
│       Cloud Functions        │
│                              │
│  Event-driven backend logic  │
│  Notification processing     │
└──────────────────────────────┘
```

### Client Layer

The Flutter application is responsible for the user interface and client-side interactions.

It communicates with Firebase services for authentication, persistent data, file storage and real-time updates.

### Data Layer

**Cloud Firestore** acts as the central persistent data source for:

* Users
* Products
* Orders
* Reviews

Firestore streams are used to keep relevant parts of the interface synchronized with real-time database changes.

### Storage Layer

**Firebase Storage** is used to store product images uploaded through the application.

### Backend Logic

**Firebase Cloud Functions** provide reactive backend processing.

Instead of requiring the Flutter application to manually trigger the notification workflow, the backend reacts to changes in Firestore and processes the corresponding event.

---

# 📂 Project Structure

The project follows common Flutter organizational conventions.

```text
cantina/
├── android/
│   └── # Android-specific configuration
│
├── assets/
│   └── icon/
│       └── icon.png
│
├── functions/
│   └── src/
│       └── index.ts
│
├── lib/
│   ├── main.dart
│   ├── firebase_options.dart
│   │
│   ├── models/
│   │   └── # Product, Order, User and other data models
│   │
│   ├── screens/
│   │   └── # Application screens
│   │
│   └── services/
│       └── # Business logic and Firebase communication
│
├── pubspec.yaml
└── cors.json
```

---

# 🧩 Technical Architecture

The project demonstrates several important software engineering concepts:

### Client-side application

Flutter provides the cross-platform application layer and user interfaces for both students and administrators.

### Serverless backend

Firebase provides managed backend infrastructure without requiring a traditional dedicated application server.

### Real-time synchronization

Firestore streams allow application interfaces to react to changes in persistent data.

### Role-based access

The application distinguishes between students and administrators and provides different interfaces and capabilities according to the user's role.

### Event-driven processing

Cloud Functions react to Firestore events, allowing backend operations such as notifications to happen automatically.

### Separation of responsibilities

The project separates UI, data models, services and backend functions into distinct components, making the application easier to organize and evolve.

---

# 💻 Technology Stack

| Category                     | Technology               |
| ---------------------------- | ------------------------ |
| **Cross-Platform Framework** | Flutter                  |
| **Application Language**     | Dart                     |
| **Backend Platform**         | Firebase                 |
| **Authentication**           | Firebase Authentication  |
| **Database**                 | Cloud Firestore          |
| **File Storage**             | Firebase Storage         |
| **Push Notifications**       | Firebase Cloud Messaging |
| **Backend Logic**            | Firebase Cloud Functions |
| **Backend Language**         | TypeScript               |
| **State Management**         | ValueNotifier            |
| **App Icon Generation**      | flutter_launcher_icons   |

---

# 🧠 Engineering Concepts Demonstrated

This project provided practical experience with:

* Cross-platform application development
* Serverless architecture
* NoSQL database design
* Authentication flows
* Role-based access control
* Real-time data synchronization
* CRUD operations
* Cloud file storage
* Event-driven backend logic
* Push notification workflows
* Client/backend separation
* Modular application organization

---

# 📈 Project Evolution

The project was developed incrementally rather than starting directly with a cloud backend.

```text
Local Mock Database
        ↓
Flutter Application
        ↓
Firebase Integration
        ↓
Authentication
        ↓
Firestore Persistence
        ↓
Real-Time Synchronization
        ↓
Administrative Interface
        ↓
Cloud Storage
        ↓
Cloud Functions
        ↓
Push Notifications
```

This progression reflects the transition from a basic application prototype to a more complete cloud-based system.

---

# 🎯 Project Objective

The main objective was to create a realistic digital canteen experience while exploring how a mobile application can interact with a **serverless cloud backend**.

Beyond the user interface, the project focuses on the integration between:

**Application → Authentication → Database → Storage → Backend Events → Notifications**

This makes the project a practical study of modern cloud application architecture using the Firebase ecosystem.

---

# 📝 Project Status

The application implements the core student and administrator workflows described above, including authentication, ordering, product management, real-time order tracking and automated notifications.

The project also serves as part of my broader portfolio in **software engineering, cloud systems and application development**.

---

## 🔗 Related Areas

This project complements my other work in:

* Backend engineering
* Cloud infrastructure
* AI and automation
* Educational technology
* Python application development
* Software architecture

---

<p align="center">
  <i>Building practical software systems while exploring modern application and cloud architectures.</i>
</p>
