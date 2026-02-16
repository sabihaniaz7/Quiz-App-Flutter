# 📚 Interactive Quiz Application

A beautiful, feature-rich Flutter quiz application with LaTeX support for mathematical expressions, dynamic JSON-based content management, statistics tracking, and HTML export functionality.

---

## ✨ Features

- 🎨 **Beautiful Material Design UI** with gradient themes
- 📐 **LaTeX Support** for mathematical equations and formulas
- 🌓 **Dark/Light Mode** - Toggle between themes seamlessly
- 📊 **Statistics Dashboard** - Track your quiz history and performance
- 📈 **Detailed Review Screen** with correct/wrong answers highlighted
- 🔄 **Dynamic Content** - Add subjects, topics, and questions without changing code
- 📤 **HTML Export** - Share quiz results with fully rendered LaTeX
- 🎯 **Score Tracking** with percentage calculations
- 🗑️ **History Management** - Long press to delete quiz attempts
- 💾 **Persistent Storage** - Quiz history saved locally

---

## 🚀 Getting Started

### Prerequisites

- Flutter SDK (3.0 or higher)
- Dart SDK
- Android Studio / VS Code
- An Android/iOS device or emulator
  
---
## 📦 Dependencies

```yaml
dependencies:
  flutter:
    sdk: flutter
  shared_preferences: ^2.5.4    # Local data persistence
  provider: ^6.1.5+1            # State management
  path_provider: ^2.1.5         # File system access
  latext: ^0.5.1                # LaTeX rendering
  intl: ^0.20.2                 # Date/time formatting
  font_awesome_flutter: ^10.12.0  # Icon library
  share_plus: ^12.0.1           # Sharing functionality
```
---

## 📁 Project Structure

```
quiz_app/
├── lib/
│   ├── Models/
│   │   ├── subject.dart           # Subject model
│   │   ├── subtopics.dart         # SubTopic and Question models
│   │   └── questions.dart         # Question model
|   |   |__ quiz_data_service.dart # Manage and retrieve quiz data throughout the application
|   |   |__ quiz_history.dart      # Quiz History Model
│   ├── Providers/
│   │   └── statistics_provider.dart   # Manage the state of quiz statistics and history
│   │   └── theme_provider.dart        # Dark/Light theme management
│   ├── Screens/
|   │   ├── home_screen.dart          # Main subjects screen
|   │   ├── sub_topic_screen.dart     # Topics list screen
|   │   ├── quiz_screen.dart          # Quiz interface
|   │   ├── review_screen.dart        # Detailed review with HTML export
|   │   ├── statistics_screen.dart    # Quiz history and statistics
│   ├── theme/
│   │   └── app_theme.dart        # managing application-wide themes and colors
│   ├── Widgets/
│   │   └── bottom_nav_bar.dart   # manages navigation between Statistics and Home Screen
│   │   └── dailogs.dart          #  for displaying custom styled alerts
│   └── main.dart                 # App entry point
├── assets/
│   └── mcqs.json                 # ⭐ ALL QUIZ DATA IS HERE
└── pubspec.yaml
```
---

## 📝 JSON Structure

### Format:

```json
[
  {
    "name": "Mathematics",
    "mcqs": 185,
    "subtopics": [
      {
        "name": "Algebra Basics",
        "mcqs": 25,
        "questions": [
          {
            "question": "Solve for x: $2x + 5 = 15$",
            "options": [
              "$x = 5$",
              "$x = 10$",
              "$x = 7.5$",
              "$x = 2.5$"
            ],
            "answer": "$x = 5$"
          }
        ]
      }
    ]
  }
]
```

---

## 🔧 Field Descriptions

### Root Array Structure

The JSON file contains an **array of subject objects**.

### Subject Object

| Field       | Type    | Description                | Example                      |
|-------------|---------|----------------------------|------------------------------|
| `name`      | String  | Subject display name       | `"Mathematics"`, `"English"` |
| `mcqs`      | Integer | Total questions in subject | `185`                        |
| `subtopics` | Array   | List of subtopics          | See below                    |

### SubTopic Object

| Field       | Type    | Description                     | Example            |
|-------------|---------|---------------------------------|--------------------|
| `name`      | String  | Subtopic display name           | `"Algebra Basics"` |
| `mcqs`      | Integer | Number of questions in subtopic | `25`               |
| `questions` | Array   | List of question objects        | See below          |

### Question Object

| Field      | Type          | Description                                    | Example                             |
|------------|---------------|------------------------------------------------|-------------------------------------|
| `question` | String        | Question text (supports LaTeX)                 | `"What is $\\frac{1}{2}$?"`         |
| `options`  | Array[String] | 4 answer choices (supports LaTeX)              | `["$0.5$", "$2$", "$1$", "$0.25$"]` |
| `answer`   | String        | Correct answer (must match one option exactly) | `"$0.5$"`                           |

**Important:** The `answer` field must **exactly match** one of the options.

---

## 📊 Statistics Screen

### Features:

The **Statistics** screen shows your complete quiz history with:

- 📅 **Date & Time** of each quiz attempt
- 📚 **Subject & Topic** taken
- 🎯 **Score** with percentage
- ✅ **Total Questions** attempted
- 🏆 **Performance** color-coded (Green = Correct, Red = Wrong)

### How to Use:

1. **View History:**
    - Click on the "Statistics" card on the home screen
    - See all your past quiz attempts in Newest / Oldest order.

2. **Review Answers:**
    - **Tap** on any quiz card to review all questions and answers
    - See which questions you got right/wrong

3. **Delete History:**
    - **Long press** (hold) on any quiz card
    - Confirmation dialog appears
    - Tap "Delete" to remove that quiz attempt

4. **Empty State:**
    - If you haven't taken any quizzes yet, you'll see a friendly message
    - Start taking quizzes to build your statistics!

### Statistics Features:

- ✅ **Persistent Storage** - History saved even after closing the app
- 📈 **Performance Tracking** - Monitor your progress over time
- 🔍 **Detailed Review** - Click to see complete answer breakdown
- 🗑️ **Easy Management** - Long press to delete unwanted records
- 🎨 **Color-Coded** - Visual indicators for performance levels
---
## 🌓 Dark Mode

### How to Toggle:

The app supports **system-wide dark mode**. To change themes:

- Look for a theme toggle icon in the app bar
- Tap to switch between light and dark modes
- Your preference is saved automatically

### Theme Features:

- 🌞 **Light Mode:** Bright, clean interface with vibrant colors
- 🌙 **Dark Mode:** Easy on the eyes with dark backgrounds
- 🎨 **Adaptive Colors:** Subject colors adapt to theme
- 💾 **Persistent:** Your theme choice is remembered
- ⚡ **Smooth Transition:** Seamless switching between modes

### Theme Provider:

The app uses Flutter's `provider` package for state management:
- Theme changes are instant across all screens
- No need to restart the app
- Consistent experience throughout

---

## 📤 Sharing Quiz Results

Users can share their quiz results as an **HTML file** with:

- ✅ Fully rendered LaTeX formulas
- ✅ Color-coded correct/wrong answers
- ✅ Complete score summary
- ✅ Subject and topic information
- ✅ Printable format

### How to Share:

1. Complete a quiz
2. View the **Review Answers**
3. Tap the **Share** button (top right)
4. Choose sharing method:
    - WhatsApp
    - Email
    - Messenger
    - Any sharing app

The shared HTML file opens perfectly in any web browser and displays all LaTeX equations beautifully!

---

## 🎓 Complete App Flow

```
┌─────────────────┐
│   Home Screen   │ ← Select Subject (Math, English, etc.)
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ Topic Selection │ ← Choose Subtopic (Algebra, Vocabulary, etc.)
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  Quiz Screen    │ ← Answer questions one by one
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│ Result Screen   │ ← See your score and percentage
└────────┬────────┘
         │
         ├─────────► Review Screen → Share as HTML
         │
┌─────────────────┐
│Statistics Screen|  ← See your All attempt quizzes Statistics
└────────┬────────┘             
         |─────────► Tap: Review answers  
         |─────────► Hold: Delete attempt
```

---

## 📱 Screens Overview

### 1. Home Screen (Quiz Zone)
- List of all subjects
- 
### 2. Topic Selection Screen
- List of subtopics for selected subject
- MCQ count per topic
- 
### 3. Quiz Screen
- One question at a time
- Progress indicator (1/10, 2/10, etc.)
- Next button after selecting answer

### 4. Result Screen
- Final score with percentage
- Performance message
- "Review Answers" button
- "Back to Quiz Zone" option

### 5. Review Screen
- All questions with your answers
- Correct answers highlighted in green
- Wrong answers highlighted in red
- LaTeX rendered perfectly
- Share button to export as HTML

### 6. Statistics Screen
- Dark / Light Mode Toggle
- Oldest / Newest History Toggle
- Statistics Card of all quiz attempts
- Date, subject, topic, score for each attempt
- **Tap** to review that quiz
- **Long press** to delete that attempt
- Empty state if no history

---

## 🎉 Quick Start Checklist

- [ ] Install Flutter and dependencies
- [ ] Run `flutter pub get`
- [ ] Test the app with existing data
- [ ] Take a sample quiz to see Statistics
- [ ] Open `assets/mcqs.json`
- [ ] Add your own subject/questions
- [ ] Test LaTeX rendering
- [ ] Restart the app completely
- [ ] Try dark mode toggle
- [ ] Share your first quiz result!
- [ ] Review past quizzes in Statistics
- [ ] Test long press to delete

---

## 📈 Example: Complete Subject Addition

Here's a full example of adding a "Chemistry" subject:

```json
[
  {
    "name": "Chemistry",
    "mcqs": 50,
    "subtopics": [
      {
        "name": "Periodic Table",
        "mcqs": 25,
        "questions": [
          {
            "question": "What is the atomic number of Carbon?",
            "options": ["6", "12", "14", "8"],
            "answer": "6"
          },
          {
            "question": "Which element has the symbol $Fe$?",
            "options": ["Iron", "Fluorine", "Fermium", "Flerovium"],
            "answer": "Iron"
          },
          {
            "question": "What is $H_2O$ commonly known as?",
            "options": ["Water", "Hydrogen Peroxide", "Heavy Water", "Hydroxy"],
            "answer": "Water"
          }
          // Add 22 more questions to reach mcqs: 25
        ]
      },
      {
        "name": "Chemical Reactions",
        "mcqs": 25,
        "questions": [
          {
            "question": "Balance: $H_2 + O_2 \\rightarrow H_2O$",
            "options": [
              "$2H_2 + O_2 \\rightarrow 2H_2O$",
              "$H_2 + O_2 \\rightarrow H_2O$",
              "$H_2 + 2O_2 \\rightarrow 2H_2O$",
              "$4H_2 + 2O_2 \\rightarrow 4H_2O$"
            ],
            "answer": "$2H_2 + O_2 \\rightarrow 2H_2O$"
          }
          // Add 24 more questions
        ]
      }
    ]
  }
  // Keep existing subjects (Math, English, etc.)
]
```

**Remember:** Total `mcqs` in subject = sum of all subtopic `mcqs`

---

## 🔐 Data Privacy

- ✅ All quiz data stored **locally** on device
- ✅ No internet connection required for quizzes
- ✅ Statistics saved in app's private storage
- ✅ Shared HTML files contain only quiz results
- ✅ No personal information collected

---

## 📞 Support & Resources

### Helpful Links:
- [Flutter Documentation](https://flutter.dev/docs)
- [LaTeX Tutorial](https://www.overleaf.com/learn/latex/Learn_LaTeX_in_30_minutes)
- [JSON Validator](https://jsonlint.com)
- [Material Icons](https://fonts.google.com/icons)
- [Color Picker](https://htmlcolorcodes.com/)

---

**Happy Quizzing! 🎓✨**

Made with ❤️ using Flutter



