# 🏢 Desk Reservation & Attendance System

![Power Apps](https://img.shields.io/badge/Built%20With-Power%20Apps-blue)
![Power Automate](https://img.shields.io/badge/Automation-Power%20Automate-green)
![SharePoint](https://img.shields.io/badge/Data-SharePoint-orange)
![License](https://img.shields.io/badge/License-MIT-lightgrey)

A scalable, rule-driven workspace management system built using **Microsoft Power Apps, SharePoint, and Power Automate**, designed to solve real-world office overcrowding while enforcing **fair usage, attendance accountability, and system integrity**.

---

## 🚨 The Problem

As teams rapidly scaled, office capacity became a bottleneck:

- Desks were overbooked  
- Employees reserved desks but didn’t show up  
- No visibility into actual usage  
- No enforcement of fairness  

👉 Result: **Overcrowding, inefficiency, and frustration**

---

## 💡 The Solution

I designed and built a **full end-to-end system** that:

- Digitizes desk reservations across multiple floors  
- Enforces strict booking and fairness rules  
- Prevents no-shows through attendance validation  
- Ensures physical presence using geofencing  
- Maintains performance at scale via automated data lifecycle management  

---

## ⚙️ System Overview

The system manages the complete lifecycle:

1. Users browse floors and desks  
2. Users reserve desks based on rules  
3. System enforces limits and permissions  
4. Users confirm attendance via QR + geofencing  
5. No-shows are automatically marked as **Expired**  
6. Past reservations are archived daily  

---

## 📱 Reservation Experience

| | |
|---|---|
| <img src="screenshots/reservation-app-home-mock.png" height="300"/> | <img src="screenshots/reservation-app-section-mock.png" height="300"/> |

<p align="center"><em>Interactive floor navigation and desk-level reservation interface with real-time availability</em></p>

---

## 📱 Attendance Confirmation App

<p align="center">
  <img src="screenshots/attendance-confirmation-app.png" width="55%" />
</p>

<p align="center"><em>Lightweight mobile app for attendance confirmation using desk ID and geofencing validation</em></p>

---

## 🧠 Key Capabilities

<p align="center">

🗺️ <strong>Interactive Floor-Based Reservation</strong><br>
120+ desks across 3 floors mapped into a fully digital system.

<br><br>

📅 <strong>Smart Reservation Rules</strong><br>
Daily limits, active limits, and booking constraints enforce fairness.

<br><br>

👥 <strong>Role-Based Access</strong><br>
SuperUsers can bypass limits and reserve for guests.

<br><br>

⏱️ <strong>Attendance Enforcement</strong><br>
Strict confirmation deadlines prevent desk hoarding.

<br><br>

📍 <strong>Geofencing Validation</strong><br>
Ensures users are physically inside the office before confirming.

<br><br>

⚡ <strong>Scalable Data Design</strong><br>
Automated archival avoids SharePoint delegation issues.

</p>

---

## 🏗️ System Architecture

<p align="center">
  <img src="diagrams/system-architecture.png" width="85%" />
</p>

**Layers:**

- **Application Layer** → Power Apps (Reservation + Attendance apps)  
- **Data Layer** → SharePoint lists  
- **Automation Layer** → Power Automate workflows  
- **Validation Layer** → Geofencing logic  

---

## 🔄 Reservation Status Lifecycle

| Status | Meaning |
|------|--------|
| Active | Reservation created and pending attendance |
| Confirmed | Attendance verified successfully |
| Cancelled | User manually cancelled |
| Expired | User failed to confirm attendance |

---

## 📊 Data Lifecycle Strategy

To maintain performance and scalability:

- Active data → stored in `Active_Reservations`  
- Historical data → moved daily to `Archived_Reservations`  
- Automated cleanup prevents delegation limits  

👉 See: `docs/data-lifecycle-and-archival.md`

---

## 🔐 Security & Confidentiality

This repository intentionally excludes sensitive information:

- No SharePoint screenshots  
- No internal URLs or credentials  
- No employee data  
- Floor layouts only exist inside `.msapp` files  

👉 See: `docs/security-and-confidentiality.md`

---

## 🚀 Why This Project Stands Out

This is not just a Power Apps project — it demonstrates:

- 🧠 System design thinking  
- ⚙️ Real-world business rule enforcement  
- 📉 Performance optimization under platform constraints  
- 🔐 Security awareness  
- 📍 Physical validation using geofencing  
- 📊 Scalable architecture  

---

## ⚠️ Limitations

- Not fully mobile responsive (optimized for desktop/tablet)  
- Manual floor mapping  
- GPS accuracy limitations  
- Single-location deployment  

👉 See: `docs/limitations-and-future-improvements.md`

---

## 🔮 Future Improvements

- Mobile-first redesign  
- Dynamic desk configuration  
- Power BI analytics dashboards  
- Multi-location support  
- Advanced geofencing (WiFi / Bluetooth)  

---

## 🧩 Tech Stack

| Layer | Technology |
|------|------------|
| Frontend | Power Apps |
| Backend | SharePoint |
| Automation | Power Automate |
| Logic | Power Fx |
| Validation | Geofencing (Haversine Formula) |

---

## 🧑‍💻 Author

**Adham Elkhouly**

- Analytics Specialist @ Nestlé  
- Building scalable systems using Power Platform, data, and automation  
---

## 📄 License

This project is licensed under the MIT License.

See the `LICENSE.txt` file for details.

---

## ⭐ Final Note

This system was built to solve a **real operational challenge**.

It reflects how I approach engineering:

> Not just building features — but designing systems that enforce behavior, scale efficiently, and deliver real impact.
