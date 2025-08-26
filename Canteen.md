### 📱 Digital Canteen Project
A complete and functional application developed in Flutter with a serverless backend on Firebase. The project simulates an ordering system for a school canteen (CantinaSenac), allowing students to place orders and the canteen staff to manage operations in real-time.

### 🚀 Overview
The project was built incrementally, starting with a local mock database and evolving into a complete and robust cloud solution, integrating Firebase's core services. The application distinguishes between two user roles (students and canteen administrators), each with its own dedicated interface and permissions.

### ✨ Key Features
### * **Complete Authentication Flow:**
* **Email & Password Login.**
* **New user registration (with profile creation in the database).**
* **Password recovery via email.**
* **Secure logout functionality.**
* **Role-based access control (student vs. canteen) based on Firestore data.**

### * **Student Experience:**
* **Real-time product menu with name search and category filtering.**
* **Product detail screen with descriptions and user reviews.**
* **Shopping cart with local state management.**
* **Order placement flow with a simulated payment process.**
* **"My Orders" screen to track order status in real-time.**
* **Product review and rating system for delivered orders.**

### * **Admin Panel (Canteen):**
* **Dashboard with access to management features.**
* **Real-time view of all incoming orders.**
* **Order status management (e.g., "Preparing", "Ready for Pickup").**
* **Full product management (CRUD - Create, Read, Update, Delete).**
* **Product image uploads directly from the app to Firebase Storage.**

### * **Backend & Notification System:**
* **Real-time push notifications sent automatically to the customer when the order status is updated to "Ready for Pickup," powered by Firebase Cloud Functions.**
