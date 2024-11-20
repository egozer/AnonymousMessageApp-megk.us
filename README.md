# Firebase-Based Messaging System with User Authentication

This project is a simple messaging system built with Firebase, where users can log in with a username and PIN to view their messages. Users can send messages without logging in, but only logged-in users can view their own messages. 

## Features

- **User Authentication**: Users log in with a username and a 4-digit PIN.
- **Personalized Messages**: Messages are only visible to the logged-in user.
- **Anonymous Messaging**: Users can send messages without logging in.
- **Firebase Integration**: Uses Firebase Realtime Database for message storage and authentication.

## Demo

### Login Page
- Users enter their username and PIN to log in. 
- Only valid users can access their personalized messages. Invalid credentials will show an error.

### Messaging Page
- Logged-in users can view their personal messages.
- A message input form is available for sending new messages to any user.

## Installation and Setup

### Prerequisites
- [Firebase Account](https://firebase.google.com/)
- Basic understanding of HTML, JavaScript, and Firebase.

### Steps
1. **Clone the Repository**
   ```bash
   git clone https://github.com/yourusername/firebase-messaging-system.git
   cd firebase-messaging-system
2. **Set Up Firebase**
   - Go to the [Firebase Console](https://console.firebase.google.com/).
   - Create a new project.
   - Enable **Realtime Database** in your Firebase project:
     1. Navigate to **Build** > **Realtime Database** in the Firebase Console.
     2. Click **Create Database** and set the location.
     3. Choose "Start in test mode" for initial testing, which sets public read/write access. Later, secure it by modifying the rules.
   - Update the database rules to secure user-specific access:
     ```json
     {
       "rules": {
         "messages": {
           ".read": "auth != null", // Only logged-in users can read
           ".write": "true" // Anyone can send messages
         },
         "users": {
           "$username": {
             ".read": "auth != null", // Only the logged-in user can read their data
             ".write": "auth != null" // Only the logged-in user can modify their data
           }
         }
       }
     }
     ```
   - Enable **Authentication**:
     1. Navigate to **Build** > **Authentication** > **Sign-in method**.
     2. Enable the **Anonymous** sign-in provider.
   - Retrieve your Firebase configuration:
     1. Go to **Project Settings** in the Firebase Console.
     2. Scroll to the **Your apps** section.
     3. Copy the `firebaseConfig` object and replace the placeholders in your code:
       ```javascript
       const firebaseConfig = {
         apiKey: "YOUR_API_KEY",
         authDomain: "YOUR_AUTH_DOMAIN",
         databaseURL: "YOUR_DATABASE_URL",
         projectId: "YOUR_PROJECT_ID",
         storageBucket: "YOUR_STORAGE_BUCKET",
         messagingSenderId: "YOUR_MESSAGING_SENDER_ID",
         appId: "YOUR_APP_ID"
       };
       ```
