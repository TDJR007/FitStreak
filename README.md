# FitStreak

*Stay consistent, track your progress, and unlock workouts one step at a time — all from your browser.*

FitStreak is an interactive fitness tracking web app built with Vue 3 and Vite, designed to guide users through a structured Push–Pull–Legs (PPL) workout routine over a 30-day challenge.

## 🚀 Features

### 🗓️ 30-Day Push–Pull–Legs Program
Follow a tried-and-tested training split designed for both beginners and seasoned lifters.

### 🧠 Exercise Descriptions with Modals
Each workout includes detailed instructions for correct form and execution.

### ✅ Progress Tracking
Completion is stored in local storage, unlocking the next workout step-by-step.

### 📱 Fully Responsive UI
Built mobile-first for quick access at the gym or on the go.

## 🧱 Tech Stack

- **Framework:** Vue 3 (Composition API)
- **Bundler:** Vite
- **Styling:** Fanta.css
- **State Management:** Reactive components + Local Storage
- **Routing & UI:** Vue directives, modals, and component-based layout

## 🛠️ Getting Started

```bash
# 1. Clone the repository
git clone https://github.com/TDJR007/FitStreak.git
cd FitStreak

# 2. Install dependencies
npm install

# 3. Start development server
npm run dev
```

### 🔨 Build for Production

```bash
npm run build
```

### 🔍 Preview Production Build

```bash
npm run preview
```

## 📁 Project Structure

```
FitStreak/
├── .gitignore              # Git ignore rules
├── README.md               # Project documentation
├── index.html              # Entry HTML file
├── package.json            # Dependencies & scripts
├── package-lock.json       # Locked dependency versions
├── vite.config.js          # Vite configuration
├── public/
└── src/
    ├── App.vue            # Root Vue component
    ├── main.js            # Application entry point
    ├── fanta.css          # Fanta CSS framework
    ├── style.css          # Custom styles
    ├── assets/            # Static assets & icons
    ├── components/        # Vue components
    │   ├── Grid.vue       # Workout grid component
    │   ├── Portal.vue     # Modal portal component
    │   ├── Rules.vue      # Rules display component
    │   ├── Tips.vue       # Tips component
    │   ├── layout/
    │   │   └── Layout.vue # Main layout wrapper
    │   └── pages/
    │       ├── Dashboard.vue # Dashboard page 
    │       ├── Welcome.vue   # Welcome/landing page
    │       └── Workout.vue   # Individual workout page
    └── utils/
        └── index.js       
```

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- Fanta.css for the beautiful styling framework (check out this brilliant repo here: https://github.com/jamezmca/fantacss)
- Vue.js team for the amazing framework
- My friend AJM for workout inspiration

---
