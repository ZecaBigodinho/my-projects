🚀 Project: Gamified Learning Platform


### Status: Testing Phase
### Technologies Used: <img src="https://skillicons.dev/icons?i=flutter,firebase&theme=dark" />


## Description:
This project was developed with the goal of creating an educational platform for schools, enabling the digital assignment of tasks, tests, and content delivery. The solution was designed to modernize the classroom, focusing on engagement through gamification and providing real-time feedback for teachers and students.

### Key Features:
Role-Based Access Control (RBAC): Distinct interfaces and functionalities for Teachers and Students, ensuring each has access only to the tools relevant to their role.

## Teacher Panel:
* **Central Dashboard**: Quick access to all management tools.
* **Activity Management**: Create, view, edit, and delete activities.
* **Dynamic Activity Modes**: Support for "Classic" activities (with a final deadline) and "Flash" activities (Kahoot-style, with a timer per question).
* **Question Authoring**: Add multiple-choice or essay-style questions, with support for image uploads.
* **Attendance System**: Register and consult the historical attendance of students by course and date.
* **Performance Dashboard**: Track student progress, view their completed activities, and their scores.

## Student Panel:
* **Activity List**: View all available activities for your course, with icons to differentiate the modes.
* **Interactive Quiz**: Respond to activities in Classic or Flash modes through a clean and reactive interface.
* **Gamification**: The Flash mode includes a real-time timer to create a more dynamic and competitive learning environment.
* **Score Tracking**: The score is calculated and saved automatically at the end of each activity.

## My Role and Key Learnings:
This project was developed individually, with full responsibility for the architectural design, front-end development in Flutter, and the backend implementation on Firebase.
The biggest challenge was creating a flexible data architecture in Cloud Firestore that could support the different functionalities, such as the multiple activity modes and individual score tracking. The decision to add an activityScores map to each user's document, for example, was a crucial learning experience that enabled the efficient creation of the teacher's performance dashboard.
The main technical learning was the management of real-time state in Flutter for the "Flash" quiz functionality. Implementing a Timer that interacts with the widget's lifecycle (StatefulWidget) to control the countdown, automatic advancement between questions, and prevent memory leaks was a challenging and highly valuable experience. The use of Cloud Functions to automate user data cleanup also reinforced the importance of maintaining database integrity.
