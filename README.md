# ⏳ UnVeiled – Life Expectancy Tracker (Vue)

A minimalist, real-time Vue app that calculates your time lived and remaining — visualized in weeks — using your **name**, **birthdate**, and **life expectancy**. It’s a reflective tool to help you live with awareness and intention.

---

## 🧠 What It Does

This app helps visualize your lifespan and includes:

- 🧍 A form to enter **name**, **birthdate**, and **life expectancy**
- 📊 A **progress bar** showing the **percentage of life lived**
- 🟣 A **grid of weekly dots** representing your entire life in weeks
- ⏳ Real-time **countdown clocks** in multiple time units
- 📦 **LocalStorage** for persistent user data
- 🔁 **"Reset Data"** button to start over
- 🔗 **"Copy Link"** button to share the app with others
- 🔮 Displays **expected death year** and total life expectancy
- 💬 A **life quote** by C.S. Lewis

---

## 💡 Features

### 📆 Weekly Life Grid
- 1 dot = 1 week of life (52 per year)
- **Filled** = lived weeks
- **Empty** = future weeks
- **Current week** is highlighted
- **Final week** is marked with a violet circle

### ⏱ Dynamic Countdown Cards
- Live countdown showing remaining:
  - **Years**
  - **Months**
  - **Weeks**
  - **Days**
  - **Hours**
  - **Minutes**
  - **Seconds**
- These values are dynamic and update in real-time.

---

## 🛠 Tech Stack

| Tool | Purpose |
|------|---------|
| **Vue 3** | Frontend framework (Composition API + `<script setup>`) |
| **CSS** | Styling and layout |
| **LocalStorage** | Persistent user data |
| **`utils/index.js`** | Utility functions (e.g. date math, time calculations) |

---

## 🚀 Getting Started

1. **Clone the repo**
   ```bash
   git clone https://github.com/your-username/unveiled-vue-app.git
   cd unveiled-vue-app
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Run the dev server**
   ```bash
   npm run dev
   ```

4. Open in browser:  
   [http://localhost:5173](http://localhost:5173)

---

## 📎 Share It

Tap the **"Copy Link"** button in the app to share your personalized timeline with others.

---

## 📜 Quote

> *“You can’t go back and change the beginning, but you can start where you are and change the ending.”*  
> — C.S. Lewis

---

## 🚀 Live Demo

👉 [UnVeiled](https://unveiled-time.netlify.app/)
