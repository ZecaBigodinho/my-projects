### Adote+ 🐾
Adote+ is an open-source mobile application developed with Flutter, aiming to build a bridge between animals in need of a home and people willing to adopt them. Beyond adoption, the platform facilitates the search for lost pets and supports partner NGOs, centralizing efforts for animal welfare.

### 📜 Overview
This project was born from the need for an accessible, centralized tool for the animal protection community. The application offers a complete ecosystem where users can:

* **Adopt a Friend: Browse a list of available pets for adoption, with search filters for species, gender, and name.**
* **Find Lost Pets: View posts of lost animals in the area to help find them or publish an alert for your own missing pet.**
* **Support NGOs: Learn about the work of partner organizations and find ways to contribute financially or through volunteering.**
* **Publish and Manage: Users can create posts for adoption or lost pets, as well as edit and remove their own listings.**

### 📂 Directory Structure
The project's core is contained within the lib directory, which follows a feature-oriented architecture to ensure scalability and maintainability.
```

lib/
├── main.dart                 # App entry point and router configuration
├── firebase_options.dart     # Firebase project configuration
├── models/                   # Data models (business objects)
│   ├── ong_model.dart
│   ├── pet_model.dart
│   └── lost_pet_model.dart
├── pages/                    # UI Screens of the application
│   ├── apresentar_page.dart
│   ├── cadastro_login_page.dart
│   ├── criar_perfil_page.dart
│   ├── principal_tela_page.dart
│   ├── pets_lista_page.dart
│   └── ...                   # Remaining screens
├── services/                 # Business logic and communication with external APIs
│   ├── cloudinary_service.dart
│   ├── firebase_auth_service.dart
│   └── firestore_service.dart
└── widgets/                  # Reusable UI components
    ├── app_drawer.dart
    └── nova_publicacao_widget.dart
```
### **main.dart:** The main file that initializes Firebase and defines all the application's navigation routes using the go_router package.
## **/models:** Contains the classes that model the application's data, such as Pet and Ong. It ensures a consistent and strongly-typed data structure.
## **/pages:** Each file represents a complete screen of the application, responsible for composing the interface and managing its local state.
## **/services:** An abstraction layer that handles all business logic and external communication, such as Firebase authentication, Firestore operations, and image uploads to Cloudinary.
## **/widgets:** Stores custom and reusable UI components, like the navigation menu (AppDrawer), to keep the code clean and avoid repetition (DRY principle).

### 🛠️ Technologies Used

| Category | Tecnology |
| :--- | :--- |
| **Cross-Platform** | [Flutter](https://flutter.dev/) |
| **Language (App)** | [Dart](https://dart.dev/) |
| **Back-end** | [Firebase](https://firebase.google.com/) (Serverless) |
| **Authentication** | [Firebase Authentication](https://firebase.google.com/docs/auth) |
| **Database** | [Cloud Firestore](https://firebase.google.com/docs/firestore) (NoSQL) |
| **Media Storage**| [Cloudinary](https://cloudinary.com/) |
| **State (Simple)** | [ValueNotifier](https://api.flutter.dev/flutter/foundation/ValueNotifier-class.html) |
| **Icon Generation** | [flutter_launcher_icons](https://pub.dev/packages/flutter_launcher_icons) |
