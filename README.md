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

### Installation

1. **Clone or extract the project**
   ```bash
   cd quiz_app
   ```

2. **Install dependencies**
   ```bash
   flutter pub get
   ```

3. **Run the app**
   ```bash
   flutter run
   ```
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

**Note:** All dependencies are already included in `pubspec.yaml`

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

## 🎯 How to Add/Modify Quiz Content

### All quiz data is stored in 
`assets/mcqs.json`

The app **automatically reads** this file and generates the UI. You can:
- ✅ Add new subjects
- ✅ Add new subtopics
- ✅ Add / remove questions
- ✅ Modify existing content

**No code changes required!** The UI adapts automatically.

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

## 📐 Using LaTeX in Questions

### Basic Math Syntax

```json
{
  "question": "Solve: $x^2 + 5x + 6 = 0$",
  "options": [
    "$x = -2, -3$",
    "$x = 2, 3$",
    "$x = -1, -6$",
    "$x = 1, 6$"
  ],
  "answer": "$x = -2, -3$"
}
```

### Common LaTeX Commands

| Expression    | LaTeX Code          | Display |
|---------------|---------------------|---------|
| Fraction      | `$\\frac{a}{b}$`    | a/b     |
| Exponent      | `$x^2$`             | x²      |
| Square Root   | `$\\sqrt{x}$`       | √x      |
| Subscript     | `$x_1$`             | x₁      |
| Greek Letters | `$\\alpha, \\beta$` | α, β    |
| Sum           | `$\\sum_{i=1}^{n}$` | Σ       |
| Integral      | `$\\int_0^1 x dx$`  | ∫       |

**Note:** Always escape backslashes in JSON: `\\frac` not `\frac`

---

## 🔄 Adding New Content - Step by Step

### Example: Adding a New Subject

1. **Open** `assets/mcqs.json`

2. **Add a new object** to the root array:

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
            "question": "What is the chemical symbol for Gold?",
            "options": ["Au", "Ag", "Go", "Gd"],
            "answer": "Au"
          },
          {
            "question": "How many elements are in the periodic table?",
            "options": ["118", "108", "92", "100"],
            "answer": "118"
          }
        ]
      },
      {
        "name": "Chemical Reactions",
        "mcqs": 25,
        "questions": [
          {
            "question": "What is the product of $2H_2 + O_2$?",
            "options": ["$2H_2O$", "$H_2O_2$", "$HO_2$", "$H_2O$"],
            "answer": "$2H_2O$"
          }
        ]
      }
    ]
  }
]
```

3. **Update MCQ counts:**
    - Subject `mcqs` = sum of all subtopic `mcqs`
    - Subtopic `mcqs` = number of questions in that subtopic

4. **Save the file**

5. **Restart the app** - Your new subject appears automatically! ✨

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

## 🎨 Customization

### Changing Subject Colors

Colors are **auto-generated** from the subject name for consistency. The app uses a color mapping system.

To customize, edit the color generation logic in `lib/themes/app_theme.dart`:

```dart
Color get color {
  switch (name.toLowerCase()) {
    case 'mathematics':
      return Colors.blue;
    case 'english':
      return Colors.orange;
    case 'physics':
      return Colors.purple;
    // Add your custom colors here
    default:
      return Colors.teal;
  }
}
```

### Changing App Name

1. **Android:** `android/app/src/main/AndroidManifest.xml`
   ```xml
   <application android:label="YourAppName">
   ```

2. **iOS:** `ios/Runner/Info.plist`
   ```xml
   <key>CFBundleName</key>
   <string>YourAppName</string>
   ```

---

## ⚠️ Important Notes

### JSON Validation Rules

1. **Always validate** your JSON: [JSONLint](https://jsonlint.com)
2. **Array Structure:** Root must be an array `[ {...} ]`
3. **MCQ Counts:** Must match actual number of questions
4. **Answer Matching:** `answer` must **exactly** match one option
5. **LaTeX Escaping:** Use `\\` for backslashes in JSON

### Common Mistakes to Avoid

❌ **Wrong:**
```json
"answer": "x = 5"  // Option is "$x = 5$"
```

✅ **Correct:**
```json
"answer": "$x = 5$"  // Exact match with option
```

❌ **Wrong:**
```json
"question": "Solve $\frac{1}{2}$"  // Single backslash
```

✅ **Correct:**
```json
"question": "Solve $\\frac{1}{2}$"  // Escaped backslash
```

### Best Practices

1. ✅ Test LaTeX syntax before adding to JSON
2. ✅ Keep backup of working JSON file
3. ✅ Add questions gradually and test often
4. ✅ Use consistent formatting
5. ✅ Validate JSON after every edit

---

## 🐛 Troubleshooting

### App doesn't show new content
- **Hot reload doesn't work for JSON changes**
- Completely **stop and restart** the app
- Check JSON syntax at [JSONLint](https://jsonlint.com)
- Ensure `assets/mcqs.json` is listed in `pubspec.yaml`

### LaTeX not rendering
- Check backslash escaping: use `\\frac` not `\frac`
- Verify LaTeX syntax at [LaTeX Editor](https://latexeditor.lagrida.com)
- Ensure dollar signs are present: `$...$`
- Check for special characters that need escaping

### Share button not working
- Test on a **real device** (may not work on emulators)
- Check app permissions on Android/iOS
- Ensure `share_plus` package is installed
- Verify internet connection for HTML sharing

### Statistics not saving
- Check if `shared_preferences` is installed
- Ensure app has storage permissions
- Try clearing app data and restarting
- Check device storage availability

### Dark mode not working
- Ensure system dark mode is enabled
- Restart the app after changing system theme
- Check `theme_provider.dart` is properly configured
- Verify `provider` package is installed

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

## 💡 Pro Tips

### For Quiz Creators:

1. **Start Small:** Begin with 10 questions per topic
2. **Test Often:** Restart app after each JSON change
3. **Backup First:** Keep a copy before major edits
4. **LaTeX Preview:** Test formulas in online editor first
5. **Consistent Format:** Follow the same pattern for all subjects

### For Students:

1. **Track Progress:** Use Statistics to monitor improvement
2. **Review Mistakes:** Tap on past quizzes to learn from errors
3. **Share Results:** Export and share with study groups
4. **Dark Mode:** Use at night to reduce eye strain
5. **Clean History:** Long press to delete practice attempts

### For Developers:

1. **State Management:** App uses Provider pattern
2. **Local Storage:** SharedPreferences for persistence
3. **Theme System:** Adaptive colors for dark/light modes
4. **JSON Parsing:** Dynamic model generation
5. **Error Handling:** Graceful fallbacks for invalid data

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

## 🚀 Performance Tips

1. **Optimize JSON:** Don't exceed 500 questions per subject
2. **LaTeX Rendering:** Complex formulas may load slower
3. **Image Assets:** Keep images optimized if added
4. **History Limit:** Consider limiting statistics to last 100 attempts
5. **Regular Cleanup:** Use long press to delete old quiz attempts

---

## 📞 Support & Resources

### Helpful Links:
- [Flutter Documentation](https://flutter.dev/docs)
- [LaTeX Tutorial](https://www.overleaf.com/learn/latex/Learn_LaTeX_in_30_minutes)
- [JSON Validator](https://jsonlint.com)
- [Material Icons](https://fonts.google.com/icons)
- [Color Picker](https://htmlcolorcodes.com/)

### Common Questions:

**Q: Can I add images to questions?**
A: Currently text and LaTeX only. Images require code changes.

**Q: What's the maximum number of questions?**
A: No hard limit, but 1000+ questions may slow down the app.

**Q: Can I export statistics?**
A: Currently no, but you can share individual quiz results.

**Q: Does it work offline?**
A: Yes! Only sharing requires internet.

---

**Happy Quizzing! 🎓✨**

Made with ❤️ using Flutter


