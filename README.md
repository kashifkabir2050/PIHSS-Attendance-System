# PIHSS Attendance System
## Pakistan Islamia Higher Secondary School, Sharjah

A complete **Daily Attendance Management System** with:
- 📝 Teacher Submission Form (daily attendance per class)
- 📊 Admin Dashboard (daily / weekly / monthly reports)
- 🚨 Absent Student Register
- 👤 Individual Student Search & Record
- 📈 Trend Graphs (present / absent / authorized)
- ⬇️ PDF Download with graphs
- 🔥 Firebase Firestore database backend

---

## 📁 Project Structure

```
pihss-attendance/
├── index.html          ← Teacher attendance form
├── dashboard.html      ← Admin dashboard & reports
├── css/
│   └── style.css       ← All styles
├── js/
│   └── firebase-config.js  ← (reference only, config is inline)
└── README.md
```

---

## 🔥 Step 1 — Create a Firebase Project

1. Go to **https://console.firebase.google.com**
2. Click **"Add project"** → Name it `pihss-attendance`
3. Disable Google Analytics (optional) → Click **Create project**

---

## 🗄️ Step 2 — Enable Firestore Database

1. In your Firebase project, go to **Build → Firestore Database**
2. Click **Create database**
3. Choose **"Start in test mode"** (for development; secure later)
4. Choose a Cloud Firestore location (e.g., `asia-south1` for UAE/South Asia)
5. Click **Enable**

---

## 🔑 Step 3 — Get Your Firebase Config

1. In Firebase Console → **Project Overview** → Click the **⚙️ gear icon** → **Project settings**
2. Under **"Your apps"**, click **"Add app"** → choose **Web (`</>`)**
3. Register the app (name it `pihss-web`)
4. Copy the `firebaseConfig` object — it looks like:

```js
const firebaseConfig = {
  apiKey:            "AIzaSy...",
  authDomain:        "pihss-attendance.firebaseapp.com",
  projectId:         "pihss-attendance",
  storageBucket:     "pihss-attendance.appspot.com",
  messagingSenderId: "123456789",
  appId:             "1:123456789:web:abc123"
};
```

---

## ⚙️ Step 4 — Add Config to Both HTML Files

Open **`index.html`** and **`dashboard.html`**.

In both files, find this block (near the bottom in the `<script type="module">` section):

```js
// ▶▶ REPLACE WITH YOUR FIREBASE CONFIG ◀◀
const firebaseConfig = {
  apiKey:            "YOUR_API_KEY",
  authDomain:        "YOUR_PROJECT_ID.firebaseapp.com",
  ...
};
```

Replace it with your real config from Step 3. Do this in **both files**.

---

## 🔐 Step 5 — Firestore Security Rules (for production)

Go to **Firestore → Rules** and replace with:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /attendance/{docId} {
      // Allow anyone to write (teachers submit without login)
      allow create: if true;
      // Only allow read/delete from your school's domain (optional - add Firebase Auth for full security)
      allow read, delete: if true;
    }
  }
}
```

For a fully secured setup, add Firebase Authentication (Google Sign-In for admin).

---

## 🐙 Step 6 — Push to GitHub

### First time setup:

```bash
# In your project folder
git init
git add .
git commit -m "Initial commit: PIHSS Attendance System"

# Create a repo on github.com first, then:
git remote add origin https://github.com/YOUR_USERNAME/pihss-attendance.git
git branch -M main
git push -u origin main
```

---

## 🌐 Step 7 — Deploy with GitHub Pages (Free Hosting)

1. Push your code to GitHub (Step 6)
2. Go to your GitHub repo → **Settings → Pages**
3. Under **Source**, select: `Deploy from a branch`
4. Branch: `main`, Folder: `/ (root)`
5. Click **Save**
6. Your site will be live at:
   `https://YOUR_USERNAME.github.io/pihss-attendance/`

📝 **Teacher form:** `https://YOUR_USERNAME.github.io/pihss-attendance/index.html`
📊 **Dashboard:**    `https://YOUR_USERNAME.github.io/pihss-attendance/dashboard.html`

---

## 📊 Firestore Data Structure

Each attendance submission creates one document in the `attendance` collection:

```json
{
  "date":               "2026-04-21",
  "day":                "Tuesday",
  "cycle":              "Primary",
  "grade":              "3",
  "section":            "C",
  "className":          "3C",
  "totalStudents":      32,
  "authorizedAbsent":   4,
  "unauthorizedAbsent": 5,
  "present":            23,
  "attendancePct":      84,
  "authNames":          "Ali Khan, Sara Ahmed",
  "unauthNames":        "Bilal Raza, Hina Malik",
  "teacherName":        "Asra Waqas",
  "submittedAt":        "Timestamp"
}
```

---

## 📋 Dashboard Features

| Feature | Description |
|---------|-------------|
| **Daily Report** | Filter by date, cycle, grade → Class-wise table + 3 charts |
| **Weekly Report** | Day-by-day trend + grade & cycle averages |
| **Monthly Report** | Full month trend line + polar area chart |
| **Student Search** | Search by name → full absence history + bar chart |
| **Absent Register** | All absent students with type (authorized/unauthorized) |
| **All Records** | Full table with delete button per record |
| **PDF Download** | Exports the daily report + absent register as PDF |

---

## 🏫 Supported Classes

**Kindergarten:** KG1, KG2  
**Primary:** Grades 1–5  
**Middle:** Grades 6–9  
**Higher:** Grades 10–12  

**Sections:** A, B, C, D, E, F, AB, BB, BC, BD, AG, BG, CG, DG

---

## 📞 Support

School: Pakistan Islamia Higher Secondary School, Sharjah, UAE  
System built with: HTML, CSS, JavaScript, Firebase Firestore, Chart.js, jsPDF
