# trAIn

**An AI-powered Android fitness coach that provides real-time form correction and personalized workout guidance.**

COMP 491 · Senior Design Project II · Spring 2026
California State University, Northridge · Department of Computer Science

[![GitHub](https://img.shields.io/badge/GitHub-tabee1024%2FtrAIn-181514?logo=github)](https://github.com/tabee1024/trAIn)

---

## About

trAIn is an Android fitness application designed for individuals who are beginners or have no experience with structured exercise. Using on-device computer vision and AI coaching, it guides users through bodyweight workouts with real-time form correction, automatic rep counting, and personalized post-workout feedback — making quality fitness coaching accessible to anyone with a smartphone.

The app combines pose estimation through MediaPipe, a motivational AI coach called Doctor Dopamine, and Firebase-backed progress tracking to create a complete training experience from onboarding to long-term improvement.

### What Users Can Do

- Create a profile through a short onboarding survey
- Log personal fitness goals and motivations
- Read and view a workout guide with tips on effective exercise
- Select from beginner-friendly bodyweight workouts
- Get real-time feedback on form throughout a workout via the phone's camera
- Receive a post-workout assessment aligned with personal goals
- Get personalized motivational coaching through AI (Doctor Dopamine)
- View workout history and statistics in a private profile

---

## Team

| Name | Role | GitHub | LinkedIn |
|------|------|--------|----------|
| Christian Estrada | Team Lead · Implementation Support | [@ChristianE-L4D](https://github.com/ChristianE-L4D) | [LinkedIn](https://www.linkedin.com/in/christian-estrada-1a93a71b9) |
| Jesus Ramirez | Backend · AI Coach · Pose Logic | [@IRetroCoderI](https://github.com/IRetroCoderI) | [LinkedIn](https://www.linkedin.com/in/jesus-ramirez-88846b248/) |
| Tabitha Sulaiman | Front-End Development | [@tabee1024](https://github.com/tabee1024) | [LinkedIn](https://www.linkedin.com/in/tabithasulaiman/) |
| Vishal Chaudhari | Front-End · Back-End | [@vishalchaudhari2002](https://github.com/vishalchaudhari2002) | [LinkedIn](https://www.linkedin.com/in/vishal-chaudhari-7b5748224) |
| Brian Bonilla | Back-End · Live Feed Camera | [@Brian-Bonilla](https://github.com/Brian-Bonilla) | — |
| Reenu Mohan | Front-End Development · UI/UX | [@ReenuMohan2022](https://github.com/ReenuMohan2022) | [LinkedIn](https://www.linkedin.com/in/reenu-m-551074355/) |

### Responsibilities

**Christian Estrada** — User body overlay visualization, user data storage design (SQL), AI Coach implementation and motivational response generation.

**Jesus Ramirez** — Dynamic user data display system (Firebase retrieval, structuring, and presentation of profile info, workout stats, and progress metrics). Workout performance metrics integration into the profile dashboard. AI Coach feedback module (goal data organization, contextual prompt formatting, personalized post-workout responses). Pose estimation threshold alignment for rep detection across push-ups, squats, crunches, and lunges. Movement state conditions and edge-case handling for incomplete reps and improper joint positioning.

**Tabitha Sulaiman** — Front-end development and application structure.

**Vishal Chaudhari** — User Signup/Login page, Firebase database architecture, user data storage (emails, passwords, profile data).

**Brian Bonilla** — Camera API implementation, live feed view for body outline and pose tracking, workout form correction visualization.

**Reenu Mohan** — Home screen design and navigation, Workouts screen with organized workout lists, Workout Detail screen with instructions and tutorials, Profile and About screens.

---

## Technologies

| Technology | Purpose | Link |
|------------|---------|------|
| Kotlin | Android development language | [kotlinlang.org](https://kotlinlang.org/) |
| Jetpack Compose | Declarative UI framework | [developer.android.com](https://developer.android.com/jetpack/compose) |
| CameraX | Camera pipeline for live frame streaming | [developer.android.com](https://developer.android.com/training/camerax) |
| MediaPipe / MoveNet | On-device pose estimation and landmark detection | [ai.google.dev](https://ai.google.dev/edge/mediapipe/solutions/vision/pose_landmarker) |
| Firebase | Authentication, Firestore database, user data storage | [firebase.google.com](https://firebase.google.com/) |
| Android Studio | Primary IDE and emulator environment | [developer.android.com](https://developer.android.com/studio) |
| Figma | UI/UX design and prototyping | [figma.com](https://www.figma.com/) |
| GitHub | Version control and team collaboration | [github.com](https://github.com/tabee1024/trAIn) |

---

## Architecture

### App Structure

```
com.train.app/
├── data/
│   ├── model/
│   │   ├── User.kt                  # User profile schema (Firestore)
│   │   └── WorkoutSession.kt        # Session, exercise, set, form warning schemas
│   └── repository/
│       └── TrainRepository.kt       # Firebase CRUD for users + sessions + metrics
│
├── domain/
│   ├── coach/
│   │   └── DoctorDopamineService.kt # AI coach: post-workout feedback + live chat
│   ├── exercises/
│   │   └── ExerciseCatalog.kt       # Exercise definitions, pose thresholds, form rules
│   └── session/
│       └── WorkoutSessionEngine.kt  # Session state machine, rep detection, form scoring
│
├── ui/
│   └── chat/
│       └── ChatScreen.kt            # Doctor Dopamine chat UI (Jetpack Compose)
│
└── viewmodel/
    ├── ChatViewModel.kt             # Chat screen state management
    ├── ProfileViewModel.kt          # Profile dashboard data display
    └── WorkoutViewModel.kt          # Active workout orchestration
```

### Real-Time Vision Pipeline

```
Camera Feed → Pose Model → Exercise Logic → Rep Detection → Live Feedback → Summary
   (CameraX)   (MediaPipe)   (Angle rules)   (Phase FSM)    (On-screen)   (Report)
```

1. **CameraX** streams live frames to the inference engine
2. **MediaPipe** extracts 33 body landmarks per frame
3. **Exercise Logic** analyzes joint angles against exercise-specific rules
4. **Rep Detection** uses a finite state machine to count reps via phase transitions
5. **Live Feedback** displays form corrections on-screen in real time
6. **Summary** aggregates metrics into a post-workout report with AI coaching

### Database Schema

**Firestore: `users/{uid}`** — User profile with onboarding survey data, physical stats, fitness goals, motivations, coach tone preference, streak counters, and timestamps.

**Firestore: `users/{uid}/sessions/{id}`** — Workout session with nested exercise results, set data, form warnings, timing, fatigue estimation, and Doctor Dopamine's coach feedback.

### Doctor Dopamine (AI Coach)

An AI persona that generates personalized motivational feedback. Two modes:
- **Post-workout** — Structured feedback with highlights, improvements, and next-session suggestions
- **Live chat** — Conversational coaching with full conversation history

Uses an OpenAI-compatible API (configurable endpoint and model). Includes offline fallback so the app never leaves users without a response.

---

## Skills Applied

Kotlin Programming · Android Development · Jetpack Compose · UI/UX Design · Computer Vision · Pose Estimation · Machine Learning · Firebase / Firestore · User Authentication · REST API Integration · MVVM Architecture · Real-Time Data Processing · Git & Version Control · Agile Collaboration · Figma Prototyping · Prompt Engineering · Camera APIs · Database Schema Design

---

## Showcase Website

The project showcase is a single-page website (`index.html`) built for the COMP 491 Senior Design course submission.

### File Structure

```
trAIn/
├── index.html            # Main showcase website
├── README.md             # This file
├── CSUNS.png             # CSUN seal logo
├── trAIn_1.png           # trAIn app logo
├── chris_pic.png         # Christian Estrada photo
├── profilePhoto.jpg      # Jesus Ramirez photo
├── tabitha_pic.png       # Tabitha Sulaiman photo
├── vishal_pic.jpg        # Vishal Chaudhari photo
├── brian_pic.jpg         # Brian Bonilla photo
└── reemu_pic.jpg         # Reenu Mohan photo
```

### Website Sections

| Section | ID | Description |
|---------|----|-------------|
| Navigation | *(fixed)* | CSUN seal + trAIn logo + anchor links |
| Hero | — | Full-viewport landing with logo, title, stats |
| Introduction | `#about` | Project purpose and feature checklist |
| Problem | `#problem` | Four pain-point cards |
| Features | `#features` | Six feature cards (CV, AI, UX, Data) |
| Pipeline | `#pipeline` | Six-step vision system flow |
| Screenshots | `#screens` | App screen previews |
| Demo Video | `#demo` | YouTube embed (placeholder) |
| Technologies | `#tech` | Eight tech cards with links |
| Skills | `#skills` | 18 skill pills |
| Doctor Dopamine | `#coach` | AI coach spotlight |
| Team | `#team` | Six member cards with photos and links |
| Footer | — | CSUN branding, social links, copyright |

### Design System

**Palette:** Emperor (`#564e4d`), Swirl (`#cfc7bf`), Edward (`#aeb2b2`), Santas Gray (`#959eae`)

**Fonts:** Bebas Neue (headings), DM Sans (body), JetBrains Mono (labels/code)

**Theme:** Dark, warm, athletic — all CSS inline, no external stylesheets

### Embedding the Demo Video

Upload your 3–5 minute demo to YouTube, then in `index.html` find the `#demo` section and replace the placeholder:

```html
<!-- Delete the <div class="video-placeholder">...</div> -->
<!-- Add: -->
<iframe src="https://www.youtube.com/embed/YOUR_VIDEO_ID"
        title="trAIn Demo" allowfullscreen></iframe>
```

### COMP 491 Requirements

| # | Requirement | Status |
|---|-------------|--------|
| 1 | Project logo and name in page title | ✅ |
| 2 | Members with photos, roles, GitHub, LinkedIn | ✅ |
| 3 | Project introduction with purpose and features | ✅ |
| 4 | Technologies with links | ✅ |
| 5 | Skills used | ✅ |
| 6 | Project screenshots | ✅ |
| 7 | Demo video (3–5 min) | ⏳ Placeholder ready |
| 8 | Background reflecting project purpose | ✅ |
| 9 | CSUN logo, website link, social links, copyright | ✅ |
| 10 | Link to course page | ✅ |

---

## Submission

```bash
# From the parent directory of the trAIn folder
$ tar cvzf trAIn.tgz ./trAIn
```

---

## Links

- **GitHub:** [github.com/tabee1024/trAIn](https://github.com/tabee1024/trAIn)
- **Course Page:** [csun.edu/~xjiang/SeniorDesign/](https://www.csun.edu/~xjiang/SeniorDesign/)
- **CSUN:** [csun.edu](https://www.csun.edu)

---

*© California State University, Northridge · COMP 491 Senior Design Project II · Spring 2026*
