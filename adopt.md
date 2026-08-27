# 🐾 Adote+ — Animal Adoption & Welfare Platform

<p align="center">
  <strong>Mobile Development • Serverless Architecture • Social Impact</strong>
</p>

**Status:** Completed

**Technologies:**
`Flutter` `Dart` `Firebase` `Cloud Firestore` `Cloudinary`

---

## 🚀 Project Overview

**Adote+** is an open-source mobile application developed with Flutter to connect animals in need of a home with people interested in adoption.

The project expands beyond adoption by providing tools for **lost-pet reporting and animal welfare organizations (NGOs)**, bringing these use cases together in a single application.

The platform allows users to:

* 🐕 Discover animals available for adoption
* 🔎 Search for lost pets
* 📢 Publish lost-pet alerts
* ❤️ Learn about and support partner NGOs
* 📝 Create and manage animal listings

The project combines **mobile development, cloud services, authentication, NoSQL data persistence and external media storage** around a practical social problem.

---

# 🎯 Problem

Animal adoption and lost-pet information can be distributed across social networks, messaging groups and different organizations.

This fragmentation makes it harder for people to:

* Discover animals available for adoption
* Find information about missing animals
* Publish adoption or lost-pet notices
* Find organizations working with animal welfare

Adote+ explores how these workflows can be centralized into a mobile application.

```text id="8bpljs"
                     Adote+
                        │
          ┌─────────────┼─────────────┐
          │             │             │
          ▼             ▼             ▼
      Adoption       Lost Pets        NGOs
          │             │             │
          ▼             ▼             ▼
    Find a Home    Help Reunite    Support Animal
     for a Pet       Families         Welfare
```

---

# ✨ Core Features

## 🏠 Pet Adoption

Users can browse animals currently available for adoption.

The application provides filtering capabilities based on:

* Species
* Gender
* Name

This helps users navigate available listings and find animals matching their search criteria.

---

## 🔎 Lost Pet Search

Adote+ also provides a dedicated environment for lost animals.

Users can:

* Browse lost-pet publications
* Help identify missing animals
* Publish alerts for their own missing pets

This expands the platform beyond adoption into a broader animal welfare use case.

---

## ❤️ NGO Support

The application includes information about partner animal welfare organizations.

Users can learn more about their work and discover ways to contribute through:

* Financial support
* Volunteering
* Engagement with the organization's activities

---

## 📝 Publication Management

Users can create publications for:

### Adoption

Animals looking for a new home.

### Lost Pets

Animals that have gone missing and need community assistance.

Users can also manage their own publications by:

* Creating
* Editing
* Removing

their listings.

---

# 🔐 Authentication

Firebase Authentication provides the application's user authentication layer.

Authentication allows publications and user-specific functionality to be associated with registered users.

```text id="avf3qu"
User
  │
  ▼
Firebase Authentication
  │
  ▼
Authenticated Application
  │
  ├── Create Publications
  ├── Manage Publications
  ├── Browse Adoption Listings
  └── Browse Lost Pets
```

---

# 🏛️ Application Architecture

The application's `lib` directory follows a feature-oriented organization that separates different responsibilities into:

```text id="h1myuv"
UI / Pages
     │
     ▼
Reusable Widgets
     │
     ▼
Services
     │
     ├───────────────┐
     ▼               ▼
 Firebase         Cloudinary
     │
     ▼
Authentication
     +
Cloud Firestore
```

The separation between models, pages, services and reusable widgets helps keep the application organized as functionality grows.

---

# 🧩 Architectural Layers

## 📱 Presentation Layer

The `/pages` directory contains the application's main screens.

Each page represents a complete part of the user experience and is responsible for composing the appropriate interface.

Examples include:

* Authentication
* Profile creation
* Main navigation
* Pet listings
* Publication workflows

---

## 🧱 Data Models

The `/models` directory contains classes representing the application's core entities.

Examples include:

```text id="oz5qno"
Pet
ONG
LostPet
```

Using dedicated models provides a consistent representation of application data across the codebase.

---

## ⚙️ Services Layer

The `/services` directory abstracts communication with external systems and backend services.

Examples include:

```text id="48etqf"
firebase_auth_service.dart
        │
        └── Authentication

firestore_service.dart
        │
        └── Database Operations

cloudinary_service.dart
        │
        └── Media Uploads
```

This separation prevents backend communication logic from being unnecessarily mixed with interface code.

---

## 🧩 Reusable Components

The `/widgets` directory contains reusable UI elements.

Examples include:

* Navigation drawer
* Publication components

This helps reduce duplicated interface code and follows the **DRY — Don't Repeat Yourself** principle.

---

# ☁️ Backend Architecture

Adote+ uses a serverless backend architecture based primarily on Firebase.

## Firebase Authentication

Handles user authentication.

## Cloud Firestore

Provides the NoSQL database used to persist application information.

## Cloudinary

Handles media storage and image uploads separately from the main Firebase data layer.

The architecture can be summarized as:

```text id="g9n15d"
                 Flutter Application
                         │
             ┌───────────┴───────────┐
             │                       │
             ▼                       ▼
         Firebase                Cloudinary
             │                       │
      ┌──────┴──────┐                │
      │             │                │
      ▼             ▼                ▼
Authentication   Firestore       Pet Images
                     │
                     ▼
              Application Data
```

---

# 📂 Directory Structure

The main application code is organized inside the `lib` directory.

```text id="8rxdqy"
lib/
├── main.dart
├── firebase_options.dart
│
├── models/
│   ├── ong_model.dart
│   ├── pet_model.dart
│   └── lost_pet_model.dart
│
├── pages/
│   ├── apresentar_page.dart
│   ├── cadastro_login_page.dart
│   ├── criar_perfil_page.dart
│   ├── principal_tela_page.dart
│   ├── pets_lista_page.dart
│   └── ...
│
├── services/
│   ├── cloudinary_service.dart
│   ├── firebase_auth_service.dart
│   └── firestore_service.dart
│
└── widgets/
    ├── app_drawer.dart
    └── nova_publicacao_widget.dart
```

---

# 📁 Directory Responsibilities

### `main.dart`

Application entry point.

It initializes Firebase and defines application navigation using `go_router`.

### `/models`

Contains the application's business objects and data representations, including pets, NGOs and lost animals.

### `/pages`

Contains complete application screens and their local UI behavior.

### `/services`

Provides an abstraction layer between the application interface and external services.

It handles responsibilities such as:

* Firebase Authentication
* Firestore operations
* Cloudinary image uploads

### `/widgets`

Contains reusable interface components to reduce duplication and improve maintainability.

---

# 💻 Technology Stack

| Category                     | Technology              |
| ---------------------------- | ----------------------- |
| **Cross-Platform Framework** | Flutter                 |
| **Application Language**     | Dart                    |
| **Backend**                  | Firebase                |
| **Authentication**           | Firebase Authentication |
| **Database**                 | Cloud Firestore         |
| **Database Model**           | NoSQL                   |
| **Media Storage**            | Cloudinary              |
| **Navigation**               | go_router               |
| **State Management**         | ValueNotifier           |
| **Icon Generation**          | flutter_launcher_icons  |

---

# 🧠 Engineering Concepts Demonstrated

The project provides practical experience with:

* Cross-platform mobile development
* Serverless backend architecture
* User authentication
* NoSQL persistence
* External API/service integration
* Image upload workflows
* Data modeling
* Application routing
* Separation of concerns
* Reusable UI components
* CRUD-style publication management
* Feature-oriented project organization

---

# 🧱 Separation of Concerns

One of the important architectural aspects of the project is avoiding a structure where interface, database communication and business entities are all contained in the same files.

Instead:

```text id="jndux7"
Models
  ↓
Represent data

Pages
  ↓
Present application features

Services
  ↓
Communicate with external systems

Widgets
  ↓
Provide reusable UI components
```

This makes individual responsibilities easier to understand and maintain.

---

# 🌱 Social Impact

Unlike a purely technical demonstration project, Adote+ was designed around a real social problem.

The application connects three groups:

```text id="7c7f83"
Animals needing homes
          ↕
People willing to adopt
          ↕
Animal welfare organizations
```

The lost-pet functionality expands this objective by allowing the community to participate in locating missing animals.

This demonstrates how software development can be applied not only to technical challenges but also to **community-oriented problems**.

---

# 📚 Key Learnings

Developing Adote+ provided practical experience integrating multiple technologies into a single mobile application.

Important areas explored during development include:

* Structuring larger Flutter applications
* Separating UI and service logic
* Firebase integration
* Authentication workflows
* NoSQL data modeling
* External media storage
* Reusable component design
* Navigation between application features
* Managing user-generated publications

The project also reinforced the importance of designing software architecture around the responsibilities of each component rather than simply organizing code by file type.

---

# 🔭 Future Possibilities

The existing architecture provides opportunities for future improvements such as:

* 📍 Location-based lost-pet search
* 🔔 Adoption and lost-pet notifications
* 💬 Communication between adopters and publishers
* 🗺️ Map integration
* 🏥 Veterinary and shelter partnerships
* 🔎 More advanced search filters
* 📊 NGO dashboards
* ❤️ Adoption follow-up features

These features could expand Adote+ from a publication platform into a broader digital ecosystem for animal welfare.

---

# 📌 Project Summary

**Adote+** demonstrates the development of a cross-platform application combining:

**Flutter → Authentication → NoSQL Database → Media Storage → Modular Architecture**

From a software engineering perspective, the project demonstrates my experience integrating multiple cloud services while maintaining separation between **data models, interfaces, reusable components and service communication**.

From a broader perspective, it demonstrates how software can be designed around a practical social challenge.

---

<p align="center">
  <i>Using software engineering to connect technology with real-world social impact.</i>
</p>
