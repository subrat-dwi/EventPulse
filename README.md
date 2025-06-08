
# **Event Pulse - Real-Time Club Event Polling**
### **Author:** Subrat Dwivedi  
### **Technology Stack:** Flutter, Firebase, Firestore  
### **Purpose:** A light-weight app/web tool for clubs to run live polls, Q&As or collect instant feedback during events.

## Visit - [Event Pulse](https://event-pulse-ffa53.web.app/) ↗️



## **📌 Project Overview**
The Event Pulse allows users to:
- **Create Polls** with multiple-choice questions.
- **Join Polls** using a unique Poll ID.
- **Vote on Polls** by selecting an answer.
- **View Results** dynamically updated in Firestore.

---

## **🛠️ Setup & Installation**
### **1️⃣ Prerequisites**
- Install Flutter SDK: [Flutter Installation Guide](https://flutter.dev/docs/get-started/install)
- Configure Firebase:
  - Enable Cloud Firestore for real-time database functionality. 
  - Enable Firestore & Authentication (Anonymous Sign-in)
  - Add Firebase SDKs to `pubspec.yaml`

### **2️⃣ Clone Repository & Install Dependencies**
```sh
git clone https://github.com/subrat-dwi/EventPulse
cd event_pulse
flutter pub get
```

### **3️⃣ Configure Firebase**
Run:
```sh
flutterfire configure
```
Ensure **`firebase_options.dart`** is generated and included.

---

## **📜 Application Structure**
```yaml
lib/
├── main.dart            # Entry point of the app
├── pages/
│   ├── home_page.dart    # Main screen with navigation buttons
│   ├── create_poll.dart  # Poll creation screen
│   ├── join_poll.dart    # Poll voting interface
│   ├── poll_results.dart # Poll results display
│   ├── view_polls.dart   # View user's created polls
```

---

## **🗂️ Firebase Structure**
### **Collections:**
#### **`polls/`**
Stores poll metadata:
```json
{
  "pollId": "abc123",
  "title": "Best Programming Language?",
  "createdBy": "user123",
  "questions": [
    {
      "questionId": "q1",
      "question": "Which language do you prefer?",
      "choices": ["Python", "JavaScript", "C++"]
    }
  ]
}
```

#### **`polls/{pollId}/questions/{questionId}/responses/`**
Stores user responses:
```json
{
  "userId": "xyz456",
  "selectedChoice": "Python"
}
```

---

## **🚀 Features & Functionality**
### **Create Poll**
- Users enter a **poll title** and create questions with multiple choices.
- Data is stored in **Firestore**.

### **Join Poll**
- Users enter a **Poll ID** and select their choices.
- Answers are stored dynamically.

### **View Poll Results**
- Poll results are retrieved in real-time.
- Votes are counted and displayed.

---

## **📅 Future Enhancements**
- 🎨 **UI Improvements** → Advanced button animations, custom theme support.
- 📊 **Analytics & Charts** → Integrate graphs to visualize poll data.
- 🔗 **Sharing Poll Links** → Enable users to copy & share poll links.

---

Absolutely! Based on our conversations, here are the **major issues** you faced during this project and how you tackled them:

### **🚨 Major Issues Faced**
#### **1️⃣ White Screen on Deployment (Flutter Web)**
- **Cause:** Improper Firebase initialization or missing dependencies.
- **Fix:** Ran `flutter clean`, ensured Firebase was properly initialized in `main.dart`, and corrected Web deployment settings.

#### **2️⃣ Firebase Authentication Errors**
- **Cause:** Firebase Auth wasn’t registering listeners properly.
- **Fix:** Ensured `firebase_options.dart` contained correct API keys and re-enabled Anonymous Auth in Firebase Console.

#### **3️⃣ Old Input Persisting in Dialog**
- **Cause:** `TextEditingController` retained previous entries.
- **Fix:** Cleared controllers using `joinPollId.clear()` when opening dialog.

#### **4️⃣ Polls List Showing All Polls Instead of User’s**
- **Cause:** Missing filtering for user-created polls.
- **Fix:** Used `.where('createdBy', isEqualTo: userId)` to fetch only the polls created by the logged-in user.

#### **5️⃣ Poll Results Layout Overflowing**
- **Cause:** `ListView.builder` inside a `Column` caused overflow issues.
- **Fix:** Wrapped the list in `Expanded` to ensure dynamic resizing.

---

### **🔗 Additional Resources**
- [Flutter Docs](https://flutter.dev/docs)
- [Firebase Firestore Docs](https://firebase.google.com/docs/firestore)
- [GitHub Repo](https://github.com/subrat-dwi/EventPulse)
