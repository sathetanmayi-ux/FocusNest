📱 DailyDoc – Focus & Productivity App
A distraction-blocking Android app designed to help users stay productive by using timer-based focus sessions, screen pinning, and password-protected emergency exit.

🚀 Overview
DailyDoc is a productivity application that helps users stay focused by temporarily blocking access to other apps during a focus session. It uses:
1.Android Screen Pinning
2.Foreground Services
3.AlarmManager Scheduling
Sh4.aredPreferences for secure local data storage
The app also features a reward system, motivational toasts, and allows users to schedule focus sessions for later.

🎯 Key Features

🔐 1. Login with Password Setup
-When the app is opened for the first time, the user must:
-Enter Name
-Set a Password
-This password is required for the emergency stop feature during a focus session.

🏠 2. Home Screen
-After login, users are greeted with:
-A “Hello, {username}” message
-Buttons for:
   ➕ Add Task / Start Focus
   🔑 Change Password
   🏆 View Rewards
The UI uses a modern Material Design layout.

⏱️ 3. Start Focus Now
-User selects a duration in minutes → focus session starts immediately.
-During a focus session:
    ~The screen becomes pinned
    ~The user cannot press:
        Back
        Home
        Recent Apps
-A stylish countdown timer + progress bar appear
-Motivational toasts pop up periodically
-Emergency Stop requires entering the correct password

🕒 4. Start Focus Later (Scheduled Mode)
User chooses:
-Delay (in minutes)
-Focus Duration
-The app uses AlarmManager to trigger a Foreground Service even if:
   ~The app is closed
   ~The app is killed
   ~The screen is off
-At the scheduled time:
   ✔ The app launches the FocusActivity in the foreground
   ✔ Screen pinning starts automatically

🛡️ 5. Emergency Stop (Password Protected)
-If the user attempts to stop the focus session:
    ~A password prompt appears
    ~Only the correct password stops the session
-If the wrong password is entered:
     ~A warning toast appears
     ~Screen remains locked

🏆 6. Rewards System
-Every completed focus session earns points.
-Users can open the Rewards screen, where colorful cards show:
     ~Completed Sessions
     ~Points Earned
     ~Level Progression

📲 7. Device Unlock Repinning
-If the user:
Locks the phone,Unlocks the phone again.The focus screen is automatically re-pinned using UnlockReceiver.

🧱 Project Architecture
/app
 ├── java/com.example.dailydoc
 │    ├── LoginActivity.java
 │    ├── HomeActivity.java
 │    ├── FocusActivity.java
 │    ├── ChangePasswordActivity.java
 │    ├── RewardsActivity.java
 │    ├── StartFocusScheduler.java
 │    ├── StartFocusReceiver.java
 │    ├── FocusStartService.java
 │    └── UnlockReceiver.java
 │
 └── res/layout
      ├── activity_login.xml
      ├── activity_home.xml
      ├── activity_focus.xml
      ├── activity_rewards.xml
      └── activity_change_password.xml

⚙️ Technical Concepts Used
✔ Screen Pinning

Prevents navigation away from the focus screen.

✔ Foreground Service

Needed to start focus mode from the background (Android 13–15 compliant).

✔ AlarmManager + PendingIntent

Allows scheduled sessions to trigger after minutes/hours.

✔ SharedPreferences
-Stores:
  ~Username
  ~Password
  ~Rewards/Points

✔ BroadcastReceiver
-Detects:
   ~Alarms
   ~Device unlock events

📥 How to Build & Run
-Clone the project
-Open in Android Studio
-Sync Gradle
-Run on real device or emulator
-Grant required permissions:
    ~Foreground service
    ~Exact alarm permission (if needed)

🔮 Future Improvements
-Cloud backup of sessions
-App usage analytics
-Pomodoro insights
-Themes & dark mode
